# IChatClient Feature Matrix

The `IChatClient` interface provides a unified API for chat completions across all supported providers.

## Feature comparison

| Feature | Anthropic | Ollama | OpenAI | Gemini | Mistral | Cohere | Together | AI21 | Reka | HuggingFace |
|---------|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| Text | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y |
| Streaming | Y | Y | Y | Y | Y | ~[^1] | Y | Y | Y | Y |
| Tool calling | Y | Y | Y | Y | Y | Y | Y | Y | Y[^2] | Y |
| Images | Y | Y | Y | Y | Y | - | - | - | Y | - |
| PDFs | Y | - | - | - | - | - | - | - | Y | - |
| Audio/Video | - | - | - | - | - | - | - | - | Y | - |
| Thinking | Y | Y | - | Y | - | - | - | - | - | - |
| Structured output | - | - | Y | - | - | - | - | - | Y | - |
| Reasoning | - | - | - | - | - | - | Y | Y | - | - |

[^1]: Cohere uses simulated streaming (not true SSE).
[^2]: Reka sends tool results as user text due to API limitations.

## Universal code example

The power of MEAI is that this code works identically across all providers:

```csharp
using Microsoft.Extensions.AI;

IChatClient client = /* any provider */;

// Simple text completion
var response = await client.GetResponseAsync("Explain quantum computing briefly.");
Console.WriteLine(response);

// Streaming
await foreach (var update in client.GetStreamingResponseAsync("Tell me a story."))
{
    Console.Write(update.Text);
}
```

## Provider-specific initialization

=== "Anthropic"

    ```csharp
    IChatClient client = new AnthropicClient(apiKey)
        .AsChatClient("claude-sonnet-4-20250514");
    ```

=== "OpenAI"

    ```csharp
    // Note: namespace conflict — use Meai alias if needed
    IChatClient client = new OpenAiClient(apiKey)
        .AsChatClient("gpt-4o");
    ```

=== "Ollama"

    ```csharp
    IChatClient client = new OllamaApiClient()
        .AsChatClient("llama3.2");
    ```

=== "Google Gemini"

    ```csharp
    IChatClient client = new GoogleGeminiClient(apiKey)
        .AsChatClient("gemini-2.0-flash");
    ```

=== "Mistral"

    ```csharp
    // Note: namespace conflict — use Meai alias
    using Meai = Microsoft.Extensions.AI;
    Meai.IChatClient client = new MistralClient(apiKey)
        .AsChatClient("mistral-large-latest");
    ```

## Tool calling

All `IChatClient` implementations support function/tool calling via MEAI's `AIFunction` abstraction:

```csharp
using Microsoft.Extensions.AI;

// Define tools using CSharpToJsonSchema
[GenerateJsonSchema]
public interface IMyTools
{
    [Description("Gets the current weather for a location")]
    string GetWeather(string city);
}

// Use with any IChatClient
var tools = new MyToolsService().AsTools();
var options = new ChatOptions { Tools = tools };

var response = await client.GetResponseAsync(
    "What's the weather in Tokyo?",
    options);
```

## Per-SDK documentation

Each SDK has a detailed MEAI guide with provider-specific examples:

| SDK | Documentation |
|-----|--------------|
| Anthropic | [tryagi.github.io/Anthropic/guides/meai/](https://tryagi.github.io/Anthropic/guides/meai/) |
| Ollama | [tryagi.github.io/Ollama/guides/meai/](https://tryagi.github.io/Ollama/guides/meai/) |
| OpenAI | [tryagi.github.io/OpenAI/guides/meai/](https://tryagi.github.io/OpenAI/guides/meai/) |
| Google.Gemini | [tryagi.github.io/Google_Generative_AI/guides/meai/](https://tryagi.github.io/Google_Generative_AI/guides/meai/) |
| Mistral | [tryagi.github.io/Mistral/guides/meai/](https://tryagi.github.io/Mistral/guides/meai/) |
| Cohere | [tryagi.github.io/Cohere/guides/meai/](https://tryagi.github.io/Cohere/guides/meai/) |
| Together | [tryagi.github.io/Together/guides/meai/](https://tryagi.github.io/Together/guides/meai/) |
| AI21 | [tryagi.github.io/AI21/guides/meai/](https://tryagi.github.io/AI21/guides/meai/) |
| Reka | [tryagi.github.io/Reka/guides/meai/](https://tryagi.github.io/Reka/guides/meai/) |
| HuggingFace | [tryagi.github.io/HuggingFace/guides/meai/](https://tryagi.github.io/HuggingFace/guides/meai/) |
