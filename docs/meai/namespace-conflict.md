# Alias Guidance

The old docs treated every collision as a generic "namespace conflict". In practice there are two different cases:

- **Interface collisions**: the SDK generates its own `IChatClient` or `ISpeechToTextClient`
- **Model-type collisions**: the SDK generates types such as `ChatMessage`, `ChatResponse`, or `Embedding`

In both cases, the safest pattern is:

```csharp
using Meai = Microsoft.Extensions.AI;
```

## SDKs Where an Alias Is Recommended

| SDK | Collision type | Why the alias helps |
|-----|----------------|---------------------|
| OpenAI | `IChatClient`, `Embedding` | The SDK generates its own `IChatClient` interface and `Embedding` model |
| Mistral | `IChatClient` | Generated `IChatClient` shadows MEAI |
| Together | `IChatClient` | Generated `IChatClient` shadows MEAI |
| Reka | `IChatClient` | Generated `IChatClient` shadows MEAI |
| Upstage | `IChatClient`, `ChatMessage` | Both the interface and common message types collide |
| ElevenLabs | `ISpeechToTextClient` | Generated `ISpeechToTextClient` shadows MEAI |
| Cohere | `ChatMessage`, `ChatResponse` | Common chat model names overlap with MEAI concepts |
| Writer | `ChatMessage`, `ChatResponse` | Common chat model names overlap with MEAI concepts |
| Mixedbread | `Embedding` | Generated `Embedding` model shadows `Embedding<T>` |
| Pinecone | `Embedding` | Generated `Embedding` struct shadows `Embedding<T>` |

## Full Pattern

```csharp
using Meai = Microsoft.Extensions.AI;

Meai.IChatClient chatClient = /* provider */;
var response = await chatClient.GetResponseAsync(
    [new Meai.ChatMessage(Meai.ChatRole.User, "Hello!")],
    new Meai.ChatOptions { ModelId = "provider-model" });
```

## Example: Upstage

```csharp
using Upstage;
using Meai = Microsoft.Extensions.AI;

Meai.IChatClient chatClient = new UpstageClient(apiKey);

var response = await chatClient.GetResponseAsync(
    [new Meai.ChatMessage(Meai.ChatRole.User, "Summarize this image.")],
    new Meai.ChatOptions { ModelId = "solar-pro" });
```

## Example: Pinecone

```csharp
using Pinecone;
using Meai = Microsoft.Extensions.AI;

Meai.IEmbeddingGenerator<string, Meai.Embedding<float>> generator =
    new PineconeClient(apiKey).Inference;

var embeddings = await generator.GenerateAsync(["Hello, world!"]);
```

## When You Can Skip the Alias

You usually do **not** need the alias for SDKs such as:

- `Anthropic`
- `AI21`
- `AssemblyAI`
- `Cartesia`
- `Deepgram`
- `Gladia`
- `Google.Gemini`
- `HuggingFace`
- `Jina`
- `Nomic`
- `Ollama`
- `RevAI`
- `SarvamAI`
- `Speechmatics`
- `TwelveLabs`
- `VoyageAI`

If you prefer, you can also avoid aliases by fully qualifying the MEAI types instead of importing them.
