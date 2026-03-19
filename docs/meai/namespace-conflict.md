# Namespace Conflict Pattern

Some auto-generated SDKs have their own `IChatClient` interface in the SDK namespace that shadows `Microsoft.Extensions.AI.IChatClient`. This causes compilation errors when trying to use MEAI interfaces directly.

## Affected SDKs

| SDK | Has Conflict | Resolution |
|-----|:---:|------------|
| OpenAI | Yes | Use `Meai` alias |
| Mistral | Yes | Use `Meai` alias |
| Cohere | Yes | Use `Meai` alias |
| Together | Yes | Use `Meai` alias |
| Reka | Yes | Use `Meai` alias |
| Anthropic | No | Direct `using` works |
| Ollama | No | Direct `using` works |
| Google.Gemini | No | Direct `using` works |
| AI21 | No | Direct `using` works |
| HuggingFace | No | Direct `using` works |
| Jina | No | Direct `using` works |
| VoyageAI | No | Direct `using` works |

## Common errors

Without the alias, you'll see errors like:

- **CS0029**: Cannot implicitly convert type `TogetherClient` to `Together.IChatClient`
- **CS0308** / **CS1929**: `GetService<T>()` resolves to the non-generic SDK method instead of the MEAI extension

## The `Meai` alias pattern

Add a namespace alias at the top of your file:

```csharp
using Meai = Microsoft.Extensions.AI;
```

Then use the alias to explicitly reference MEAI types:

```csharp
using Meai = Microsoft.Extensions.AI;

// Explicit MEAI interface reference
Meai.IChatClient chatClient = client;

// Explicit extension method calls (not extension syntax)
var metadata = Meai.ChatClientExtensions.GetService<Meai.ChatClientMetadata>(chatClient);
var self = Meai.ChatClientExtensions.GetService<TogetherClient>(chatClient);
```

## Full example with Together

```csharp
using Together;
using Meai = Microsoft.Extensions.AI;

var client = new TogetherClient(apiKey);

// Must use Meai prefix — Together has its own IChatClient
Meai.IChatClient chatClient = client.AsChatClient("meta-llama/Llama-3.3-70B-Instruct-Turbo");

var response = await chatClient.GetResponseAsync(
    [new Meai.ChatMessage(Meai.ChatRole.User, "Hello!")],
    new Meai.ChatOptions { ModelId = "meta-llama/Llama-3.3-70B-Instruct-Turbo" });
Console.WriteLine(response);
```

## Full example with IEmbeddingGenerator

The same pattern applies to `IEmbeddingGenerator`:

```csharp
using Cohere;
using Meai = Microsoft.Extensions.AI;

var client = new CohereClient(apiKey);

// Explicit interface reference
Meai.IEmbeddingGenerator<string, Meai.Embedding<float>> generator =
    client.AsEmbeddingGenerator("embed-english-v3.0");

var metadata = Meai.EmbeddingGeneratorExtensions
    .GetService<Meai.EmbeddingGeneratorMetadata>(generator);
```

## SDKs without conflicts

For SDKs without namespace conflicts, you can use `Microsoft.Extensions.AI` directly:

```csharp
using Microsoft.Extensions.AI;

var client = new AnthropicClient(apiKey);
IChatClient chatClient = client.AsChatClient("claude-sonnet-4-20250514");

var response = await chatClient.GetResponseAsync("Hello!");
```
