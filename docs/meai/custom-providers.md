# CustomProviders

Many AI providers offer OpenAI-compatible APIs. Instead of maintaining separate SDKs for each, `tryAGI.OpenAI` includes `CustomProviders` factory methods that return a pre-configured `OpenAiClient` pointing to the correct base URL and with the right defaults.

## Installation

```bash
dotnet add package tryAGI.OpenAI
```

## Provider table

| Provider | Factory Method | Default Chat Model |
|----------|---------------|-------------------|
| Azure | `CustomProviders.Azure(key, endpoint)` | `gpt-4o-mini` |
| DeepInfra | `CustomProviders.DeepInfra(key)` | `Qwen/Qwen2.5-72B-Instruct` |
| DeepSeek | `CustomProviders.DeepSeek(key)` | `deepseek-chat` |
| Groq | `CustomProviders.Groq(key)` | `llama-3.3-70b-versatile` |
| XAi | `CustomProviders.XAi(key)` | `grok-3-mini` |
| Fireworks | `CustomProviders.Fireworks(key)` | `llama-v3p3-70b-instruct` |
| OpenRouter | `CustomProviders.OpenRouter(key)` | `meta-llama/llama-3.2-3b-instruct:free` |
| Together | `CustomProviders.Together(key)` | `Llama-3.3-70B-Instruct-Turbo` |
| Perplexity | `CustomProviders.Perplexity(key)` | `sonar` |
| SambaNova | `CustomProviders.SambaNova(key)` | `Meta-Llama-3.3-70B-Instruct` |
| Mistral | `CustomProviders.Mistral(key)` | `mistral-large-latest` |
| Codestral | `CustomProviders.Codestral(key)` | `codestral-latest` |
| Cerebras | `CustomProviders.Cerebras(key)` | `llama3.1-70b` |
| Cohere | `CustomProviders.Cohere(key)` | `command-r-08-2024` |
| Nebius | `CustomProviders.Nebius(key)` | `Qwen/Qwen2.5-72B-Instruct` |
| Hyperbolic | `CustomProviders.Hyperbolic(key)` | `Llama-3.3-70B-Instruct` |
| GitHub Models | `CustomProviders.GitHubModels(token)` | `gpt-4o` |
| Ollama | `CustomProviders.Ollama()` | `llama3.2` |
| LM Studio | `CustomProviders.LmStudio()` | *(user-selected)* |

## Usage

### Basic chat

```csharp
using OpenAI;
using Microsoft.Extensions.AI;

var client = CustomProviders.DeepSeek(apiKey);
IChatClient chatClient = client.AsChatClient("deepseek-chat");

var response = await chatClient.GetResponseAsync("Hello!");
Console.WriteLine(response);
```

### Streaming

```csharp
var client = CustomProviders.Groq(apiKey);
IChatClient chatClient = client.AsChatClient("llama-3.3-70b-versatile");

await foreach (var update in chatClient.GetStreamingResponseAsync("Tell me a joke."))
{
    Console.Write(update.Text);
}
```

### Embeddings

```csharp
var client = CustomProviders.DeepInfra(apiKey);
IEmbeddingGenerator<string, Embedding<float>> generator =
    client.AsEmbeddingGenerator("BAAI/bge-en-icl");

var embeddings = await generator.GenerateAsync(["Hello, world!"]);
```

### Local providers

Ollama and LM Studio require no API key:

```csharp
// Ollama (default: http://localhost:11434)
var ollamaClient = CustomProviders.Ollama();
IChatClient chat = ollamaClient.AsChatClient("llama3.2");

// LM Studio (default: http://localhost:1234)
var lmStudioClient = CustomProviders.LmStudio();
IChatClient chat2 = lmStudioClient.AsChatClient("your-model-name");
```

## CustomProviders vs dedicated SDKs

| Aspect | CustomProviders | Dedicated SDK |
|--------|----------------|---------------|
| Installation | `tryAGI.OpenAI` (one package) | `tryAGI.{Provider}` (per provider) |
| API coverage | OpenAI-compatible endpoints only | Full provider API |
| MEAI support | `IChatClient` + `IEmbeddingGenerator` | Provider-specific interfaces |
| Provider-specific features | Limited to OpenAI compatibility | Full access |

**Use CustomProviders** when you only need chat/embeddings and the provider is OpenAI-compatible.
**Use a dedicated SDK** when you need the provider's full API or unique features.
