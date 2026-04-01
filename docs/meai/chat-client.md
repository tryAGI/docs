# IChatClient Coverage

`IChatClient` is the widest MEAI surface across the tryAGI SDKs. There are currently **14** direct chat implementations, plus **27** OpenAI-compatible factories via `tryAGI.OpenAI.CustomProviders`.

## Capability Matrix

| SDK | Streaming | Tool calling | Multimodal input | Reasoning / thinking | Structured output | Notes |
|-----|-----------|--------------|------------------|----------------------|-------------------|-------|
| Anthropic | Native | Y | Images, PDFs | Thinking | - | Reference implementation |
| Ollama | Native | Y | Images | Thinking | - | Local-first models |
| OpenAI | Native | Y | Images | - | JSON object + JSON schema | Also powers `CustomProviders` |
| Google.Gemini | Native | Y | Images | Thinking | - | Thought-signature support in provider API |
| Mistral | Native | Y | Images | - | - | Alias recommended |
| Cohere | Simulated | Y | - | - | - | `GetStreamingResponseAsync()` emits the full response as one update |
| Together | Native | Y | - | Reasoning | - | Alias recommended |
| AI21 | Native | Y | - | Reasoning text | JSON object | Jamba chat models |
| Reka | Native | Y | Images, audio, video, PDFs | - | JSON schema | Tool results are sent back as user text |
| HuggingFace | Native | Y | Model-dependent | Model-dependent | - | Serverless feature set depends on backend model |
| Writer | Native | Y | - | - | - | Alias recommended |
| SarvamAI | Simulated | Y | - | `reasoning_effort`, `wiki_grounding` | - | SSE exists in the provider API, but the current adapter is post-hoc |
| Upstage | Native | Y | Images | - | - | Also exposes groundedness, translation, and document tools |
| Coze | Native | Y* | - | Reasoning text | - | Requires `bot_id`; provider tool calls are not yet emitted as `FunctionCallContent` |

## Universal Usage

```csharp
using Microsoft.Extensions.AI;

IChatClient client = /* any supported provider */;

var response = await client.GetResponseAsync(
    [new ChatMessage(ChatRole.User, "Explain vector databases in two sentences.")],
    new ChatOptions { ModelId = "provider-specific-model" });

Console.WriteLine(response.Text);
```

## Initialization Patterns

### Standard direct SDK

```csharp
using Anthropic;
using Microsoft.Extensions.AI;

IChatClient client = new AnthropicClient(apiKey);
```

### Alias-sensitive SDK

```csharp
using Upstage;
using Meai = Microsoft.Extensions.AI;

Meai.IChatClient client = new UpstageClient(apiKey);
```

### Bot-centric SDK

```csharp
using Coze;
using Microsoft.Extensions.AI;

IChatClient client = new CozeClient(apiKey)
    .WithBotId("your-bot-id")
    .WithUserId("demo-user");
```

`Coze` also accepts `bot_id`, `user_id`, and `conversation_id` through `ChatOptions.AdditionalProperties`.

### OpenAI-compatible provider

```csharp
using Microsoft.Extensions.AI;
using tryAGI.OpenAI;

IChatClient client = CustomProviders.Groq(apiKey);

var response = await client.GetResponseAsync(
    "Hello!",
    new ChatOptions { ModelId = "llama-3.3-70b-versatile" });
```

## Tool Calling Pattern

Most current `IChatClient` implementations support full MEAI tool calling:

```csharp
using CSharpToJsonSchema;
using Microsoft.Extensions.AI;

[GenerateJsonSchema]
public interface IWeatherTools
{
    [Description("Gets the current weather for a location.")]
    string GetWeather([Description("The city name")] string city);
}

IChatClient client = /* any supported provider */;

var options = new ChatOptions
{
    ModelId = "provider-specific-model",
    Tools = new WeatherToolsService().AsTools().AsAITools(),
};

var response = await client.GetResponseAsync("What's the weather in Tokyo?", options);
```

`Coze` is the current exception in the direct adapters: it can signal `ChatFinishReason.ToolCalls` and send tool results back to the provider, but it does not yet surface provider-issued tool calls back as `FunctionCallContent`.

## Structured Output

Structured output currently exists in the direct adapters for:

- `OpenAI`: JSON object and JSON schema output
- `AI21`: JSON object output
- `Reka`: JSON schema output

## Multimodal Notes

- `Anthropic` supports text, images, and PDFs.
- `OpenAI`, `Google.Gemini`, `Mistral`, `Ollama`, and `Upstage` support image input.
- `Reka` is the broadest direct multimodal adapter and accepts images, audio, video, and PDF URLs.
- `Coze`, `Writer`, `SarvamAI`, `Together`, and `AI21` are currently text-first in their MEAI adapters.

## SDK Guides

Per-provider details live in the SDK docs:

- [Anthropic](https://tryagi.github.io/Anthropic/guides/meai/)
- [Ollama](https://tryagi.github.io/Ollama/guides/meai/)
- [OpenAI](https://tryagi.github.io/OpenAI/guides/meai/)
- [Google.Gemini](https://tryagi.github.io/Google_Generative_AI/guides/meai/)
- [Mistral](https://tryagi.github.io/Mistral/guides/meai/)
- [Cohere](https://tryagi.github.io/Cohere/guides/meai/)
- [Together](https://tryagi.github.io/Together/guides/meai/)
- [AI21](https://tryagi.github.io/AI21/guides/meai/)
- [Reka](https://tryagi.github.io/Reka/guides/meai/)
- [HuggingFace](https://tryagi.github.io/HuggingFace/guides/meai/)
- [Writer](https://tryagi.github.io/Writer/guides/meai/)
- [SarvamAI](https://tryagi.github.io/SarvamAI/guides/meai/)
- [Upstage](https://tryagi.github.io/Upstage/guides/meai/)
- [Coze](https://tryagi.github.io/Coze/guides/meai/)
