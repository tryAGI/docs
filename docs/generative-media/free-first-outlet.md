# Free-First LLM Outlet

This page is for one specific goal: build a single internal "electrical outlet" that prefers free providers, respects rate limits, and relaxes to weaker models when the best free capacity is exhausted.

The important distinction is not just "free vs paid". It is:

| Type | Good backbone for an outlet? | Meaning |
|------|:----------------------------:|---------|
| Recurring free tier | Yes | Resets daily/minutely and can power ongoing traffic. |
| Trial or evaluation tier | Sometimes | Still useful, but often low-capacity or explicitly non-production. |
| One-time signup credits | No | Fine for testing, bad as a permanent backbone. |
| Local/self-hosted | Yes | Free in API-spend terms, but you pay with your own hardware. |

## Verified providers that can actually help

These are the providers that are currently useful for a free-first text outlet in practice.

| Provider | What is actually free | Fit for the outlet | tryAGI entry point |
|----------|-----------------------|--------------------|--------------------|
| **Google Gemini** | Google exposes a Free tier for selected Gemini API models. Exact live quotas are model-specific and shown in AI Studio. | **Primary** if you accept Google free-tier data terms. | [`tryAGI.Google.Gemini`](https://www.nuget.org/packages/tryAGI.Google.Gemini) |
| **SambaNova** | Free tier without a payment method. Docs publish concrete limits, for example 20 RPM, 20 RPD, and 200K tokens/day on listed free-tier models. | **Primary**. Strongest published OpenAI-compatible free contract. | `CustomProviders.SambaNova(key)` |
| **Cerebras** | Free access to all Cerebras-powered models. Model pages publish free-tier limits; example: 30 RPM, 60K input TPM, 1M daily tokens. | **Primary**. Very strong reasoning/coding candidate. | `CustomProviders.Cerebras(key)` |
| **OpenRouter** | Free `:free` models and the `openrouter/free` router. Official limits page currently documents 20 RPM and 50 free-model requests/day by default, or 1,000/day after buying at least $10 of credits. | **Secondary**. Excellent abstraction/fallback layer, but too capped to be the only backbone. | `CustomProviders.OpenRouter(key)` |
| **GitHub Models** | Included, rate-limited access to many models. The catalog API exposes model metadata including `rate_limit_tier`. | **Secondary**. Good overflow and experimentation capacity. | `CustomProviders.GitHubModels(token)` |
| **NVIDIA Build / NIM** | Many models are available under NVIDIA trial-service terms on `build.nvidia.com`. This is real free usage for evaluation, but NVIDIA does not publish one universal free quota table across all models. | **Opportunistic**. Useful extra capacity, not a clean contract. | `CustomProviders.Nvidia(key)` |
| **Groq** | Groq still offers a free API key and "get started for free", but the public docs do not currently publish one stable universal free-tier quota table. | **Opportunistic**. Excellent latency, but discover quotas from the console instead of hard-coding assumptions. | `CustomProviders.Groq(key)` |
| **Cohere Trial** | Trial keys are free, and Cohere documents that a trial key is limited to 40 API calls per minute. | **Overflow only**. Good for dev, weak as a main backbone. | `CustomProviders.Cohere(key)` |
| **Ollama / LM Studio** | Always free locally. No remote quota, but bounded by your own machine. | **Hard floor**. Best last fallback if local inference is acceptable. | `CustomProviders.Ollama()` / `CustomProviders.LmStudio()` |

## Providers that are not good backbone candidates

These can still be useful, but they should not be treated as the permanent base of a free-first outlet:

| Provider group | Why not a backbone |
|----------------|--------------------|
| **OpenAI / Anthropic** | Any free usage is temporary credit-style access, not a recurring public free tier. |
| **xAI / Together / Fireworks / Nebius** | Usually signup credits, promos, or payment-linked tiers. Good for overflow, not for a stable free outlet. |
| **Perplexity API** | The consumer product has free usage, but the API is not a real recurring free-tier backbone. |
| **DeepSeek** | Extremely cheap, but I could not verify a currently published recurring free API tier from official docs today. |
| **Mistral Experiment** | Attractive for experimentation, but public quota terms are not published cleanly enough to make it your automatic backbone without manual verification in the console. |

## Recommended quality ladder

If your goal is "use the smartest thing available, then relax when quotas are gone", this is the practical order:

### Tier A: Best free quality first

1. **Gemini free-tier flagship model** if available for your account and region.
2. **Cerebras flagship reasoning model**.
3. **SambaNova flagship reasoning model**.
4. **NVIDIA Build trial flagship model**.

Use this tier for coding, hard reasoning, structured outputs, and agent steps that actually matter.

### Tier B: Strong but more available

1. **Gemini Flash / Flash-Lite**.
2. **Groq** 70B-class chat model.
3. **SambaNova** 70B-class Llama.
4. **GitHub Models** high-tier chat model.

Use this tier for most conversational traffic, summarization, and lightweight tool orchestration.

### Tier C: Cheap resilient fallback

1. **OpenRouter `openrouter/free`**.
2. **Explicit OpenRouter `:free` model ids**.
3. **Local Ollama / LM Studio** 8B to 14B model.

Use this tier when everything else is cooling down, daily limits are gone, or you need the outlet to stay alive at all costs.

## Routing policy that actually works

The workspace already gives you provider factories through [`CustomProviders`](../meai/custom-providers.md). What it does **not** give you yet is the policy layer. That layer should do the following:

1. Filter candidates by capability first.
   Only compare models that support what the request needs: tool calling, JSON/schema output, vision, long context, or streaming.

2. Prefer recurring-free providers over credit-based providers.
   One-time credits should sit below your recurring free tiers, not above them.

3. Degrade inside a provider before leaving it.
   Example: Gemini Pro -> Gemini Flash -> Gemini Flash-Lite is usually cleaner than immediately jumping to a totally different provider.

4. Treat `429` as quota exhaustion, not provider failure.
   Put the model/provider on cooldown until reset instead of marking it unhealthy.

5. Treat `5xx`, timeouts, and transport failures as health failures.
   Trip a short circuit breaker and retry a different provider quickly.

6. Persist quota and health state outside process memory.
   If multiple workers share the same outlet, store cooldowns and quota state in Redis or SQLite so they do not stampede the same provider.

7. Keep separate ladders per workload class.
   Coding/reasoning, general chat, embeddings, and tool-heavy agent turns should not all share the same exact fallback order.

8. Reserve some best-tier capacity.
   Do not let trivial requests burn your entire Tier A budget.

## Minimal outlet shape

```csharp
public sealed record OutletCandidate(
    string Id,
    string ModelId,
    int QualityScore,
    bool SupportsTools,
    bool SupportsVision,
    bool IsRecurringFree,
    Func<IChatClient> CreateClient);

public interface IOutletStateStore
{
    bool IsCoolingDown(string candidateId, DateTimeOffset now);
    void Cooldown(string candidateId, DateTimeOffset until);
    void NoteSuccess(string candidateId, TimeSpan latency);
    void NoteFailure(string candidateId, Exception exception);
}

public sealed class FreeFirstOutlet
{
    public async Task<ChatResponse> SendAsync(
        IReadOnlyList<OutletCandidate> candidates,
        Func<OutletCandidate, Task<ChatResponse>> invoke,
        DateTimeOffset now,
        IOutletStateStore state)
    {
        foreach (var candidate in candidates
            .Where(x => !state.IsCoolingDown(x.Id, now))
            .OrderByDescending(x => x.QualityScore)
            .ThenByDescending(x => x.IsRecurringFree))
        {
            try
            {
                var response = await invoke(candidate).ConfigureAwait(false);
                state.NoteSuccess(candidate.Id, TimeSpan.Zero);
                return response;
            }
            catch (Exception ex) when (IsRateLimit(ex))
            {
                state.Cooldown(candidate.Id, now.AddMinutes(1));
            }
            catch (Exception ex)
            {
                state.NoteFailure(candidate.Id, ex);
                state.Cooldown(candidate.Id, now.AddSeconds(30));
            }
        }

        throw new InvalidOperationException("No provider is currently available.");
    }

    private static bool IsRateLimit(Exception ex) =>
        ex.Message.Contains("429", StringComparison.OrdinalIgnoreCase) ||
        ex.Message.Contains("rate limit", StringComparison.OrdinalIgnoreCase);
}
```

This is intentionally simple. The important part is the policy:

- best model first
- recurring free preferred
- quota cooldowns tracked explicitly
- cross-provider fallback after capability filtering

## A practical default ladder for tryAGI

If you want a starting point today, use this:

1. `tryAGI.Google.Gemini` flagship free-tier model
2. `CustomProviders.Cerebras(key)` flagship reasoning model
3. `CustomProviders.SambaNova(key)` flagship reasoning model
4. `CustomProviders.Groq(key)` 70B-class model
5. `CustomProviders.OpenRouter(key)` with `openrouter/free`
6. `CustomProviders.Ollama()` local 14B/8B model

That gives you:

- one high-quality non-OpenAI-compatible primary path
- two strong OpenAI-compatible remote backups
- one very fast opportunistic provider
- one universal free-model router
- one local last-resort floor

## Official references

- [Gemini API pricing](https://ai.google.dev/pricing)
- [Gemini API rate limits](https://ai.google.dev/gemini-api/docs/rate-limits)
- [SambaNova model rate limits](https://docs.sambanova.ai/docs/en/models/rate-limits)
- [Cerebras pricing](https://www.cerebras.ai/pricing)
- [Cerebras example model page with free-tier limits](https://inference-docs.cerebras.ai/models/qwen-3-235b-thinking)
- [OpenRouter Free Models Router](https://openrouter.ai/openrouter/free)
- [OpenRouter limits](https://openrouter.ai/docs/api-reference/limits)
- [GitHub Models marketplace](https://github.com/marketplace/models)
- [GitHub Models catalog API](https://docs.github.com/en/rest/models/catalog)
- [NVIDIA Build model card example](https://build.nvidia.com/openai/gpt-oss-20b/modelcard)
- [Groq pricing](https://groq.com/pricing)
- [Cohere error docs with trial-key limit note](https://docs.cohere.com/v2/reference/errors)
