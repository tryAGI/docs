# CustomProviders

Many hosted APIs are OpenAI-compatible. `tryAGI.OpenAI.CustomProviders` wraps those endpoints in the same `OpenAiClient` MEAI adapters, so you can reuse the `IChatClient` pattern across providers and the `IEmbeddingGenerator<string, Embedding<float>>` pattern where the provider exposes embeddings.

There are currently **27** factory methods in `CustomProviders`.

## Installation

```bash
dotnet add package tryAGI.OpenAI
```

## Provider Table

The factory methods do not hardcode model IDs. The values below are the typical models used in the current docs and tests.

| Provider | Factory method | Typical chat model |
|----------|----------------|--------------------|
| GitHub Models | `CustomProviders.GitHubModels(token)` | `gpt-4o` |
| Azure OpenAI | `CustomProviders.Azure(key, endpoint)` | `gpt-4o-mini` |
| DeepInfra | `CustomProviders.DeepInfra(key)` | `Qwen/Qwen2.5-72B-Instruct` |
| Groq | `CustomProviders.Groq(key)` | `llama-3.3-70b-versatile` |
| xAI | `CustomProviders.XAi(key)` | `grok-3-mini` |
| DeepSeek | `CustomProviders.DeepSeek(key)` | `deepseek-chat` |
| Fireworks | `CustomProviders.Fireworks(key)` | `accounts/fireworks/models/llama-v3p3-70b-instruct` |
| OpenRouter | `CustomProviders.OpenRouter(key)` | `meta-llama/llama-3.2-3b-instruct:free` |
| Together | `CustomProviders.Together(key)` | `meta-llama/Llama-3.3-70B-Instruct-Turbo` |
| Perplexity | `CustomProviders.Perplexity(key)` | `sonar` |
| SambaNova | `CustomProviders.SambaNova(key)` | `Meta-Llama-3.3-70B-Instruct` |
| Mistral | `CustomProviders.Mistral(key)` | `mistral-large-latest` |
| Codestral | `CustomProviders.Codestral(key)` | `codestral-latest` |
| Hyperbolic | `CustomProviders.Hyperbolic(key)` | `meta-llama/Llama-3.3-70B-Instruct` |
| Cohere | `CustomProviders.Cohere(key)` | `command-r-08-2024` |
| Ollama | `CustomProviders.Ollama()` | `llama3.2` |
| LM Studio | `CustomProviders.LmStudio()` | user-selected |
| Cerebras | `CustomProviders.Cerebras(key)` | `llama3.1-70b` |
| Nebius | `CustomProviders.Nebius(key)` | `Qwen/Qwen2.5-72B-Instruct` |
| Nvidia NIM | `CustomProviders.Nvidia(key)` | `meta/llama-3.3-70b-instruct` |
| Ollama Cloud | `CustomProviders.OllamaCloud(key)` | `llama3.2` |
| MiniMax | `CustomProviders.Minimax(key)` | `MiniMax-M1` |
| Novita AI | `CustomProviders.NovitaAI(key)` | user-selected |
| Qwen | `CustomProviders.Qwen(key)` | user-selected |
| Lepton AI | `CustomProviders.LeptonAI(key)` | user-selected |
| Cleanlab TLM | `CustomProviders.Cleanlab(key)` | user-selected |
| SiliconFlow | `CustomProviders.SiliconFlow(key)` | user-selected |

## Usage

### Basic chat

```csharp
using Microsoft.Extensions.AI;
using tryAGI.OpenAI;

IChatClient chatClient = CustomProviders.DeepSeek(apiKey);

var response = await chatClient.GetResponseAsync(
    "Hello!",
    new ChatOptions { ModelId = "deepseek-chat" });
```

### Embeddings

```csharp
using Microsoft.Extensions.AI;
using tryAGI.OpenAI;

IEmbeddingGenerator<string, Embedding<float>> generator =
    CustomProviders.DeepInfra(apiKey);

var embeddings = await generator.GenerateAsync(
    ["Hello, world!"],
    new EmbeddingGenerationOptions { ModelId = "BAAI/bge-en-icl" });
```

### Local runtimes

```csharp
using Microsoft.Extensions.AI;
using tryAGI.OpenAI;

IChatClient ollama = CustomProviders.Ollama();
IChatClient lmStudio = CustomProviders.LmStudio();
```

## CustomProviders vs Dedicated SDKs

| Aspect | `CustomProviders` | Dedicated SDK |
|--------|-------------------|---------------|
| Installation | `tryAGI.OpenAI` | `tryAGI.{Provider}` |
| Coverage | OpenAI-compatible chat and embedding paths | Full provider API surface |
| MEAI support | Reuses OpenAI MEAI adapters | Provider-specific MEAI surface |
| Provider-specific extras | Limited to OpenAI-compatible endpoints | Provider-native features, auth quirks, and non-chat APIs |

Use `CustomProviders` when the OpenAI-compatible path is enough.

Use a dedicated SDK when you need provider-native capabilities such as:

- non-OpenAI endpoints
- custom auth semantics
- speech, document, or media APIs
- provider-specific `AIFunction` wrappers
