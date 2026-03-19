# tryAGI — .NET SDKs for AI Services

tryAGI is an open-source organization building production-ready .NET SDKs for AI and ML service APIs. All SDKs are auto-generated from official OpenAPI specifications using [AutoSDK](https://github.com/HavenDV/AutoSDK), ensuring they stay current as APIs evolve.

## Key features

- **40+ SDKs** covering LLMs, image/video generation, audio, search, embeddings, and vector databases
- **Microsoft.Extensions.AI** — unified `IChatClient`, `IEmbeddingGenerator`, and `ISpeechToTextClient` interfaces across 15+ providers
- **Source-generated** — AOT/trimming compatible, no reflection, JSON serialization via `JsonSerializerContext`
- **Auto-updated** — CI fetches the latest OpenAPI specs every 3 hours and opens PRs for changes
- **Multi-target** — supports `netstandard2.0`, `net4.6.2`, `net8.0`, `net9.0`, and `net10.0`

## Quick navigation

<div class="grid cards" markdown>

- :material-rocket-launch: **[Getting Started](getting-started.md)**

    Ecosystem overview, installation guide, and decision tree for choosing the right SDK

- :material-puzzle: **[MEAI Integration](meai/index.md)**

    Microsoft.Extensions.AI feature matrices — see which SDKs support chat, embeddings, speech-to-text, and tool calling

- :material-view-list: **[SDK Catalog](sdks/index.md)**

    Complete listing of all SDKs organized by category, with NuGet, GitHub, and docs links

</div>

## Quick example

Install any SDK via NuGet and use it through the standard MEAI interface:

```csharp
using Microsoft.Extensions.AI;

// Works with Anthropic, OpenAI, Ollama, Gemini, Mistral, and more
IChatClient client = new AnthropicClient(apiKey).AsChatClient("claude-sonnet-4-20250514");

var response = await client.GetResponseAsync("What is .NET?");
Console.WriteLine(response);
```

Or use `CustomProviders` for OpenAI-compatible APIs without a dedicated SDK:

```csharp
using OpenAI;

var client = CustomProviders.DeepSeek(apiKey);
IChatClient chatClient = client.AsChatClient("deepseek-chat");
```

## Links

- **GitHub:** [github.com/tryAGI](https://github.com/tryAGI)
- **NuGet:** All packages are published under the `tryAGI.*` prefix
- **AutoSDK:** [github.com/HavenDV/AutoSDK](https://github.com/HavenDV/AutoSDK) — the engine behind all SDKs
