# Free Tier Comparison

Which AI providers can you use **for free via API**? This guide compares free tiers across all tryAGI SDKs, ranked by generosity — covering LLMs, speech-to-text, image generation, video generation, 3D, and OpenAI-compatible CustomProviders.

!!! tip "Last updated: March 2026"
    Free tier details change frequently. Check each provider's pricing page for the latest information.

---

## LLM / Text Generation

### Comparison

| Provider | Free Tier | CC Required? | Key Models | SDK |
|----------|-----------|:------------:|------------|-----|
| **Google Gemini** | **Free tier**: 10–15 RPM, 250K TPM, 1.5K req/day | No | Gemini 2.5 Pro, Flash, Flash-Lite | [tryAGI.Google.Gemini](https://www.nuget.org/packages/tryAGI.Google.Gemini) |
| **Mistral** | **Free Experiment**: all models, ~1B tokens/month | No (phone required) | Mistral Large, Codestral, all models | [tryAGI.Mistral](https://www.nuget.org/packages/tryAGI.Mistral) |
| **Groq** | **Free tier**: all models, 30 RPM, 14.4K req/day | No | Llama 4, Qwen3, Kimi K2, all models | via [CustomProviders](../meai/custom-providers.md) |
| **xAI** | **$25 signup** + $150/mo (data sharing opt-in) | No | Grok 4, Grok 4.1 Fast | [tryAGI.Xai](https://www.nuget.org/packages/tryAGI.Xai) |
| **DeepSeek** | **5M free tokens** on signup (30-day expiry) | No | DeepSeek V3.2, R1 | via [CustomProviders](../meai/custom-providers.md) |
| **Cohere** | **1,000 API calls/month** (trial key, all models) | No | Command R+, Rerank 3.5, Embed 4 | [tryAGI.Cohere](https://www.nuget.org/packages/tryAGI.Cohere) |
| **SambaNova** | **Free tier**: 10–30 RPM, persistent | No | Llama 3.3 70B, Llama 3.1 405B, Qwen 2.5 | via [CustomProviders](../meai/custom-providers.md) |
| **Cerebras** | **1M tokens/day**, 1B TPM | No | Llama, Qwen (fastest inference) | via [CustomProviders](../meai/custom-providers.md) |
| **HuggingFace** | **Free credits/month** (limited) | No | Thousands of open models | [tryAGI.HuggingFace](https://www.nuget.org/packages/tryAGI.HuggingFace) |
| Anthropic | $5 signup credits (30-day expiry) | Yes | Claude Opus/Sonnet/Haiku | [tryAGI.Anthropic](https://www.nuget.org/packages/tryAGI.Anthropic) |
| OpenAI | $5 signup credits (3-month expiry) | Yes | GPT-4o, GPT-4.1, o3 | [tryAGI.OpenAI](https://www.nuget.org/packages/tryAGI.OpenAI) |
| Together AI | Signup credits (~$1–5) | Yes | Llama, DeepSeek, Qwen, 200+ models | [tryAGI.Together](https://www.nuget.org/packages/tryAGI.Together) |
| Ollama | **Always free** (self-hosted) | No | Any open model (Llama, Mistral, Qwen, etc.) | [tryAGI.Ollama](https://www.nuget.org/packages/tryAGI.Ollama) |

!!! success "Best free LLM APIs"
    - **Google Gemini** — Most generous: free access to Gemini 2.5 Pro/Flash with high rate limits, no CC
    - **Mistral** — All models free including Mistral Large, ~1B tokens/month (phone verification only)
    - **Groq** — Blazing fast inference, all models free, generous daily limits
    - **xAI** — $25 free on signup + up to $150/mo with data sharing
    - **Ollama** — Unlimited, free forever (self-hosted, requires GPU)

### Notes

- **Groq**, **SambaNova**, and **Cerebras** are accessible via `CustomProviders` in [tryAGI.OpenAI](https://www.nuget.org/packages/tryAGI.OpenAI) — no separate SDK needed
- **Mistral Experiment** requests may be used for training — avoid sending sensitive data
- **Anthropic** and **OpenAI** have small one-time credits that expire; no persistent free tier
- **DeepSeek** is extremely cheap even after free credits ($0.14/M input tokens)
- **Cohere** trial keys are for non-commercial development only

---

## Speech-to-Text

### Comparison

| Provider | Free Tier | CC Required? | Languages | SDK |
|----------|-----------|:------------:|-----------|-----|
| **Deepgram** | **$200 free credits** (no expiry) | No | 36+ | [tryAGI.Deepgram](https://www.nuget.org/packages/tryAGI.Deepgram) |
| **AssemblyAI** | **$50 free credits** (~185 hrs) | No | 99+ | [tryAGI.AssemblyAI](https://www.nuget.org/packages/tryAGI.AssemblyAI) |
| **Gladia** | **10 hours/month** (refreshing) | No | 100+ | [Gladia](https://www.nuget.org/packages/Gladia) |
| **Speechmatics** | **8 hours/month** (refreshing) | No | 55+ | [tryAGI.Speechmatics](https://www.nuget.org/packages/tryAGI.Speechmatics) |
| Rev AI | 5 hours free (one-time) | No | English + others | [tryAGI.RevAI](https://www.nuget.org/packages/tryAGI.RevAI) |
| Cartesia | 10K–20K credits/month | No | 15+ | [Cartesia](https://www.nuget.org/packages/Cartesia) |
| ElevenLabs | 10K credits/month (~10 min STT) | No | 29+ | [tryAGI.ElevenLabs](https://www.nuget.org/packages/tryAGI.ElevenLabs) |
| FishAudio | 8K credits/month (~7 min) | No | 14+ | [tryAGI.FishAudio](https://www.nuget.org/packages/tryAGI.FishAudio) |

!!! success "Best free option: Deepgram"
    Deepgram offers **$200 in free credits** with no expiry and no credit card — enough for thousands of hours of transcription. Full API access to all models including real-time streaming.

### Notes

- **Deepgram** stands out with $200 free credits that never expire — the most generous STT free tier by far
- **AssemblyAI** gives $50 free (~185 hours of Universal model) — excellent for audio intelligence features (sentiment, summarization)
- **Gladia** and **Speechmatics** offer refreshing monthly hours — good for ongoing development
- **ElevenLabs** and **FishAudio** are primarily TTS platforms; their STT free tiers are limited
- **Cartesia** is primarily TTS; STT (Ink) is billed per second of audio from the same credit pool

---

## Image Generation

### Comparison

| Provider | Free Tier | Free API? | CC Required? | Key Models | SDK |
|----------|-----------|:---------:|:------------:|------------|-----|
| **Google Gemini** | **500 images/day** | Yes | No | Gemini 2.5 Flash Image | [tryAGI.Google.Gemini](https://www.nuget.org/packages/tryAGI.Google.Gemini) |
| StabilityAI | Non-commercial free + 25–200 signup credits | Yes | No | SD 3.5, Stable Image Core/Ultra | [tryAGI.StabilityAI](https://www.nuget.org/packages/tryAGI.StabilityAI) |
| Leonardo.AI | 150 tokens/day (web) + $5 one-time API credit | Yes | No | Phoenix, Kino XL | [tryAGI.Leonardo](https://www.nuget.org/packages/tryAGI.Leonardo) |
| Replicate | Limited free runs (select models) | Yes | No | FLUX Schnell, Stable Diffusion | [tryAGI.Replicate](https://www.nuget.org/packages/tryAGI.Replicate) |
| Fal.ai | Signup credits (~$10 with promos) | Yes | No | FLUX, SD, 1000+ models | [tryAGI.Fal](https://www.nuget.org/packages/tryAGI.Fal) |
| Recraft | 30 credits/day + 35 on signup | Web only | No | Recraft V3, V3 SVG | [tryAGI.Recraft](https://www.nuget.org/packages/tryAGI.Recraft) |
| Ideogram | 10 prompts/day (~40 images, web) | Unclear | No | Ideogram v3, v2a | [tryAGI.Ideogram](https://www.nuget.org/packages/tryAGI.Ideogram) |
| Photoroom | 10 API calls/month | Yes | No | BG removal, AI backgrounds | [tryAGI.Photoroom](https://www.nuget.org/packages/tryAGI.Photoroom) |
| BlackForestLabs | None | No | Yes | FLUX.2 Pro, FLUX 1.1 Pro | [BlackForestLabs](https://www.nuget.org/packages/BlackForestLabs) |

!!! success "Best free option: Google Gemini"
    Google Gemini offers **500 images per day** via API with no credit card — by far the most generous free image generation API. The model (Gemini 2.5 Flash Image, aka "Nano Banana") produces high-quality 1024x1024 images. Daily quota resets at midnight PT.

### Quick Start — Google Gemini Image Generation

```csharp
using tryAGI.Google.Gemini;

var apiKey = Environment.GetEnvironmentVariable("GOOGLE_API_KEY")
    ?? throw new InvalidOperationException("Set GOOGLE_API_KEY");

using var client = new GeminiClient(apiKey);

var response = await client.Models.GenerateContent(
    model: "gemini-2.5-flash-preview-native-audio-dialog",
    text: "Generate an image of a futuristic city skyline at sunset",
    responseModalities: [
        GenerateContentRequestResponseModalitie.IMAGE,
        GenerateContentRequestResponseModalitie.TEXT,
    ]);
```

### Notes

- **Google Gemini** is the clear winner — 500 img/day with full API access, no strings attached
- **StabilityAI** offers free non-commercial API use (rate-limited) plus signup credits
- **Leonardo.AI** gives a $5 one-time API credit on signup — good for testing
- **Fal.ai** is a meta-platform hosting 1000+ models (FLUX, SD, etc.) — use promo codes for extra free credits
- **Recraft** and **Ideogram** have generous web free tiers but limited/no free API access
- **BlackForestLabs** has no free tier but FLUX Schnell is open-source and can be self-hosted

---

## Video Generation

### Comparison

| Provider | Free Tier | Free API? | CC Required? | Key Capabilities | SDK |
|----------|-----------|:---------:|:------------:|-----------------|-----|
| KlingAI | 66 credits/day (~6 clips) | No (enterprise only) | No | Text/image-to-video, lip sync | [tryAGI.KlingAI](https://www.nuget.org/packages/tryAGI.KlingAI) |
| Hedra | 300–400 credits/month (~50s 720p) | No ($24/mo min) | No | Character video, lip sync | [tryAGI.Hedra](https://www.nuget.org/packages/tryAGI.Hedra) |
| Luma | 500 credits/month (draft quality) | No (separate billing) | Unclear | Dream Machine | [tryAGI.Luma](https://www.nuget.org/packages/tryAGI.Luma) |
| Runway | 125 credits (one-time, never replenishes) | No ($12/mo min) | No | Gen-3, Gen-4 | [tryAGI.Runway](https://www.nuget.org/packages/tryAGI.Runway) |
| HeyGen | 3 videos/month, 3 min max, 720p | No ($5 min API purchase) | No | AI avatars, lip sync, voice | [tryAGI.HeyGen](https://www.nuget.org/packages/tryAGI.HeyGen) |
| D-ID | 14-day trial: 3 min video | Yes (trial) | No | Talking head, 100+ avatars | [tryAGI.DId](https://www.nuget.org/packages/tryAGI.DId) |
| Tavus | 3 min gen + 3 min conversational | Yes | No | Personalized video, digital twins | [tryAGI.Tavus](https://www.nuget.org/packages/tryAGI.Tavus) |
| Shotstack | 20 credits (20 min video) | Yes | No | Programmatic video editing | [tryAGI.Shotstack](https://www.nuget.org/packages/tryAGI.Shotstack) |
| Synthesia | 3–10 min/month, 9 avatars | No ($89/mo min) | No | Enterprise AI avatars, 160+ langs | [tryAGI.Synthesia](https://www.nuget.org/packages/tryAGI.Synthesia) |
| Descript | 60 min processing + 100 AI credits | Yes (limited) | No | AI video/audio editing | [tryAGI.Descript](https://www.nuget.org/packages/tryAGI.Descript) |

!!! warning "Video generation: no provider offers generous free API access"
    Unlike image generation, **no video provider** has a truly generous free API tier. Most offer free web credits but lock API access behind paid plans. The best options for API testing are **D-ID** (14-day trial with API), **Tavus** (3 min free with API), and **Shotstack** (20 credits with API).

### Free API Access Highlights

- **D-ID** — Only 14-day trial, but includes full API access with 3 min of video and 100+ stock avatars
- **Tavus** — API-first platform, free tier includes API access (3 min video generation + 3 min conversational)
- **Shotstack** — Developer-focused video editing API, 20 free credits on signup
- **KlingAI** — Most generous web free tier (66 credits/day!) but API is enterprise-only ($4,200/3 months)

### Notes

- **KlingAI** and **Hedra** have decent web free tiers for manual experimentation
- **Runway** free credits are one-time and never refresh — use them wisely
- **Fal.ai** (listed under Image) also hosts video models (Kling, Hailuo) accessible through one API
- Most providers separate web and API billing — free web credits do NOT grant API access

---

## 3D Generation

### Comparison

| Provider | Free Tier | Free API? | CC Required? | Key Capabilities | SDK |
|----------|-----------|:---------:|:------------:|-----------------|-----|
| **Tripo** | 300/mo (web) + **2,000 one-time API credits** | Yes | No | Text-to-3D, image-to-3D, mesh | [tryAGI.Tripo](https://www.nuget.org/packages/tryAGI.Tripo) |
| Meshcapade | 2,500 credits/month, 10s video limit | Limited | No | Photo-to-avatar, motion capture | [Meshcapade](https://www.nuget.org/packages/Meshcapade) |
| Meshy | 100 credits/month (web, no download for v6) | No ($16/mo min) | No | Text/image-to-3D, AI texturing | [Meshy](https://www.nuget.org/packages/Meshy) |

!!! success "Best free option: Tripo"
    Tripo gives **2,000 free API credits on signup** (one-time) plus 300 web credits/month. Full API access with no credit card required. Game Hub Developer program offers an additional 5,000 free credits.

### Notes

- **Tripo** has the best free API offering for 3D generation — 2,000 credits is enough for substantial testing
- **Meshcapade** is generous with web credits (2,500/mo) but narrowly focused on human avatars/motion
- **Meshy** has free web generation but API requires a paid Pro plan ($16/mo)

---

## Search / RAG / Embeddings

### Comparison

| Provider | Free Tier | CC Required? | Type | SDK |
|----------|-----------|:------------:|------|-----|
| **Jina** | **10M free tokens** (shared across all APIs) | No | Embeddings, Reader, Reranker | [tryAGI.Jina](https://www.nuget.org/packages/tryAGI.Jina) |
| **Serper** | **2,500 free queries** (one-time) | No | Google SERP data | [Serper](https://www.nuget.org/packages/Serper) |
| **Tavily** | **1,000 credits/month** (refreshing) | No | AI search + extract | [tryAGI.Tavily](https://www.nuget.org/packages/tryAGI.Tavily) |
| **Exa** | **1,000 credits** (~2K searches) | No | Semantic web search | [Exa](https://www.nuget.org/packages/Exa) |
| BraveSearch | $5/mo credits (~1K queries) | Yes | Web search | [tryAGI.BraveSearch](https://www.nuget.org/packages/tryAGI.BraveSearch) |

!!! success "Best free option: Jina"
    Jina gives **10 million free tokens** on signup, shared across embedding, reader, reranking, and classification APIs — no CC required. At 100 RPM free tier, that's plenty for development.

### Notes

- **Jina** tokens are shared across all APIs (embeddings, reader, reranker, classifier) — great value
- **Tavily** is the most popular AI search API with 1,000 refreshing monthly credits — standard for AI agent development
- **Serper** gives 2,500 one-time queries to Google's SERP data — good for prototyping
- **Exa** offers semantic search with ~2,000 free searches including content extraction
- **BraveSearch** removed its free tier in 2026 — now requires CC with $5/mo credits

---

## OpenAI-Compatible CustomProviders

Many providers with free tiers are accessible via [`CustomProviders`](../meai/custom-providers.md) in `tryAGI.OpenAI` — one NuGet package, one API shape, full `IChatClient` + `IEmbeddingGenerator` support.

```bash
dotnet add package tryAGI.OpenAI
```

| Provider | Factory Method | Free Tier | CC Required? |
|----------|---------------|-----------|:------------:|
| **Groq** | `CustomProviders.Groq(key)` | All models free, 30 RPM, 14.4K req/day | No |
| **SambaNova** | `CustomProviders.SambaNova(key)` | Persistent free, 10–30 RPM (up to 405B) | No |
| **Cerebras** | `CustomProviders.Cerebras(key)` | 1M tokens/day, fastest inference | No |
| **DeepSeek** | `CustomProviders.DeepSeek(key)` | 5M tokens on signup (30-day) | No |
| **xAI** | `CustomProviders.XAi(key)` | $25 signup + $150/mo data sharing | No |
| **OpenRouter** | `CustomProviders.OpenRouter(key)` | Free models (Llama, Gemma, etc.) | No |
| **GitHub Models** | `CustomProviders.GitHubModels(token)` | Free tier: 50 req/day (GPT-4o), rate-limited | No |
| **Fireworks** | `CustomProviders.Fireworks(key)` | 10 RPM free (no CC), 6K RPM with CC | No |
| **Nebius** | `CustomProviders.Nebius(key)` | $1 free credits, 60+ models | No |
| **Perplexity** | `CustomProviders.Perplexity(key)` | 5 Pro searches/day (web); API is paid | Yes |
| **Ollama** | `CustomProviders.Ollama()` | Always free (local, no key needed) | No |
| **LM Studio** | `CustomProviders.LmStudio()` | Always free (local, no key needed) | No |

!!! success "Best free CustomProviders"
    - **Groq** — All models, generous limits, blazing fast LPU inference
    - **SambaNova** — Persistent free tier with Llama 3.1 405B (!), no expiry
    - **Cerebras** — 1M tokens/day, world's fastest inference chip
    - **OpenRouter** — Several free models available (Llama, Gemma), no CC

### Quick Start — Groq via CustomProviders

```csharp
using OpenAI;
using Microsoft.Extensions.AI;

var apiKey = Environment.GetEnvironmentVariable("GROQ_API_KEY")
    ?? throw new InvalidOperationException("Set GROQ_API_KEY");

var client = CustomProviders.Groq(apiKey);
IChatClient chatClient = client.AsChatClient("llama-3.3-70b-versatile");

var response = await chatClient.GetResponseAsync("Explain quantum computing briefly.");
Console.WriteLine(response);
```

---

## Summary — Best Free APIs by Category

| Category | Provider | What You Get Free |
|----------|----------|-------------------|
| **LLM / Text** | Google Gemini | Free tier with 2.5 Pro/Flash, 250K TPM, no CC |
| **LLM / Text** | Mistral | All models free, ~1B tokens/month, no CC |
| **LLM / Text** | Groq (CustomProviders) | All models free, 30 RPM, fastest inference, no CC |
| **Speech-to-Text** | Deepgram | $200 free credits, no expiry, no CC |
| **Speech-to-Text** | AssemblyAI | $50 free credits (~185 hrs), no CC |
| **Search / RAG** | Jina | 10M free tokens across all APIs, no CC |
| **Search / RAG** | Tavily | 1,000 credits/month refreshing, no CC |
| **Image Generation** | Google Gemini | 500 images/day, full API, no CC |
| **Video Generation** | D-ID / Tavus / Shotstack | Limited free API trials (3–20 min) |
| **3D Generation** | Tripo | 2,000 one-time API credits, no CC |

!!! info "Fal.ai as a meta-platform"
    [Fal.ai](https://fal.ai) hosts 1000+ models across image, video, and 3D generation from many providers. With a single API key and free signup credits, you can access FLUX, Stable Diffusion, Kling video models, and more — making it a convenient one-stop-shop for testing multiple generative media APIs.

---

## Getting Free API Keys

Direct links to sign up and get an API key for each provider — no credit card required unless noted.

### LLM / Text Generation

| Provider | Signup Link | Env Variable |
|----------|------------|-------------|
| Google Gemini | [aistudio.google.com](https://aistudio.google.com/apikey) | `GOOGLE_API_KEY` |
| Mistral | [console.mistral.ai](https://console.mistral.ai/) | `MISTRAL_API_KEY` |
| Groq | [console.groq.com](https://console.groq.com/keys) | `GROQ_API_KEY` |
| xAI | [console.x.ai](https://console.x.ai/) | `XAI_API_KEY` |
| DeepSeek | [platform.deepseek.com](https://platform.deepseek.com/api_keys) | `DEEPSEEK_API_KEY` |
| Cohere | [dashboard.cohere.com](https://dashboard.cohere.com/api-keys) | `COHERE_API_KEY` |
| SambaNova | [cloud.sambanova.ai](https://cloud.sambanova.ai/) | `SAMBANOVA_API_KEY` |
| Cerebras | [cloud.cerebras.ai](https://cloud.cerebras.ai/) | `CEREBRAS_API_KEY` |
| HuggingFace | [huggingface.co/settings/tokens](https://huggingface.co/settings/tokens) | `HUGGINGFACE_API_KEY` |
| Anthropic | [console.anthropic.com](https://console.anthropic.com/) (CC required) | `ANTHROPIC_API_KEY` |
| OpenAI | [platform.openai.com](https://platform.openai.com/api-keys) (CC required) | `OPENAI_API_KEY` |

### Speech-to-Text

| Provider | Signup Link | Env Variable |
|----------|------------|-------------|
| Deepgram | [console.deepgram.com](https://console.deepgram.com/signup) | `DEEPGRAM_API_KEY` |
| AssemblyAI | [assemblyai.com](https://www.assemblyai.com/dashboard/signup) | `ASSEMBLYAI_API_KEY` |
| Gladia | [app.gladia.io](https://app.gladia.io/) | `GLADIA_API_KEY` |
| Speechmatics | [portal.speechmatics.com](https://portal.speechmatics.com/) | `SPEECHMATICS_API_KEY` |

### Search / RAG / Embeddings

| Provider | Signup Link | Env Variable |
|----------|------------|-------------|
| Jina | [jina.ai/api-dashboard](https://jina.ai/api-dashboard/) | `JINA_API_KEY` |
| Tavily | [app.tavily.com](https://app.tavily.com/) | `TAVILY_API_KEY` |
| Serper | [serper.dev](https://serper.dev/) | `SERPER_API_KEY` |
| Exa | [dashboard.exa.ai](https://dashboard.exa.ai/) | `EXA_API_KEY` |

### Image / Video / 3D Generation

| Provider | Signup Link | Env Variable |
|----------|------------|-------------|
| Google Gemini (images) | [aistudio.google.com](https://aistudio.google.com/apikey) | `GOOGLE_API_KEY` |
| StabilityAI | [platform.stability.ai](https://platform.stability.ai/) | `STABILITY_API_KEY` |
| Leonardo.AI | [app.leonardo.ai](https://app.leonardo.ai/) | `LEONARDO_API_KEY` |
| Fal.ai | [fal.ai/dashboard](https://fal.ai/dashboard) | `FAL_KEY` |
| Replicate | [replicate.com](https://replicate.com/) | `REPLICATE_API_TOKEN` |
| Tripo (3D) | [platform.tripo3d.ai](https://platform.tripo3d.ai/) | `TRIPO_API_KEY` |
