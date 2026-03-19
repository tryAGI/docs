# Getting Started

## Ecosystem overview

The tryAGI ecosystem consists of three layers:

1. **Auto-generated SDKs** — Typed C# clients generated from OpenAPI specs via [AutoSDK](https://github.com/HavenDV/AutoSDK). Each SDK wraps a provider's full REST API.
2. **MEAI implementations** — Hand-written extensions that implement `Microsoft.Extensions.AI` interfaces (`IChatClient`, `IEmbeddingGenerator`, `ISpeechToTextClient`) on top of the generated clients.
3. **CustomProviders** — Factory methods in `tryAGI.OpenAI` for providers with OpenAI-compatible APIs, giving you MEAI support without a standalone SDK.

## Choosing the right approach

### Decision guide

```
Does the provider have an OpenAI-compatible API?
├── Yes → Use CustomProviders (see table below)
│         Install: tryAGI.OpenAI
│
└── No  → Does tryAGI have a dedicated SDK?
          ├── Yes → Install the dedicated SDK (e.g., tryAGI.Anthropic)
          └── No  → Consider creating one with AutoSDK
```

### When to use a dedicated SDK

Use a dedicated SDK when the provider has a **unique API** (not OpenAI-compatible) or has **provider-specific features** beyond basic chat/embeddings:

| SDK | Why dedicated? |
|-----|---------------|
| `tryAGI.Anthropic` | Unique API with thinking, PDFs, prompt caching |
| `tryAGI.Google.Gemini` | Google's own REST API with grounding, thought signatures |
| `tryAGI.ElevenLabs` | Speech synthesis + transcription, unique API |
| `tryAGI.AssemblyAI` | Transcription-focused API with async processing |
| `tryAGI.Tavily` | Search/extract API exposed as `AIFunction` tools |

### When to use CustomProviders

Use `CustomProviders` when the provider offers an **OpenAI-compatible chat/embeddings API**:

```csharp
using OpenAI;

// One line to get a fully-configured client
var client = CustomProviders.DeepSeek(apiKey);

// Use standard MEAI interfaces
IChatClient chatClient = client.AsChatClient("deepseek-chat");
```

See the [full CustomProviders table](meai/custom-providers.md) for all 19 supported providers.

## Installation

All SDKs are published as NuGet packages under the `tryAGI.*` prefix:

=== "Dedicated SDK"

    ```bash
    dotnet add package tryAGI.Anthropic
    dotnet add package tryAGI.Ollama
    dotnet add package tryAGI.Google.Gemini
    ```

=== "CustomProviders"

    ```bash
    # Single package covers 19 providers
    dotnet add package tryAGI.OpenAI
    ```

## Basic usage pattern

All SDKs follow the same pattern:

```csharp
// 1. Create the native client
var client = new AnthropicClient(apiKey);

// 2. Use the provider-specific API directly
var response = await client.Messages.CreateAsync(new CreateMessageRequest
{
    Model = "claude-sonnet-4-20250514",
    MaxTokens = 1024,
    Messages = [new InputMessage { Role = "user", Content = "Hello!" }]
});

// 3. Or use the MEAI abstraction for provider-agnostic code
IChatClient chatClient = client.AsChatClient("claude-sonnet-4-20250514");
var meaiResponse = await chatClient.GetResponseAsync("Hello!");
```

## MEAI integration

Microsoft.Extensions.AI provides unified interfaces for AI services. All tryAGI SDKs with MEAI support implement these on version **10.4.0** of the abstractions.

See the [MEAI section](meai/index.md) for feature matrices and per-interface guides.

## Target frameworks

Most SDKs multi-target for broad compatibility:

| Framework | Support |
|-----------|---------|
| `net10.0` | All SDKs |
| `net9.0` | Most SDKs |
| `net8.0` | Most SDKs |
| `netstandard2.0` | Mature SDKs |
| `net4.6.2` | Mature SDKs |

Newer SDKs may target `net10.0` only. Check the individual SDK's `.csproj` for exact targets.
