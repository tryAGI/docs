# IEmbeddingGenerator Coverage

There are currently **13** direct `IEmbeddingGenerator<string, Embedding<float>>` implementations in the tryAGI SDKs, plus the `tryAGI.OpenAI.CustomProviders` surface for OpenAI-compatible providers.

## Capability Matrix

| SDK | Batch | Custom dimensions | Token usage | Notes |
|-----|:---:|:---:|:---:|-------|
| Ollama | Y | Y | Y | Local embeddings |
| OpenAI | Y | Y | Y | Also powers `CustomProviders` |
| Google.Gemini | Y | - | - | Native Gemini embeddings |
| Cohere | Y | - | - | Alias recommended in mixed namespaces |
| Together | Y | - | - | Open-source embedding models |
| HuggingFace | Y | Y | Y | Also has multimodal extensions outside the core MEAI interface |
| Jina | Y | Y | Y | Strong custom-dimension support |
| VoyageAI | Y | Y | Y | Text embeddings only in the direct MEAI adapter |
| TwelveLabs | ~ | - | - | Batch calls are processed sequentially under the hood |
| Mixedbread | Y | Y | Y | Matryoshka embeddings |
| Nomic | Y | Y | Y | Default text embedding model plus image embedding tools |
| Pinecone | Y | - | Y | Inference API; also exposes rerank and index tools |
| Upstage | Y | - | Y | Solar embedding models |

`~` means the MEAI adapter accepts multiple values but the provider does not expose a native batch endpoint for that path.

## Universal Usage

```csharp
using Microsoft.Extensions.AI;

IEmbeddingGenerator<string, Embedding<float>> generator = /* any provider */;

var embeddings = await generator.GenerateAsync(
    ["First document", "Second document"],
    new EmbeddingGenerationOptions { ModelId = "provider-specific-model" });

Console.WriteLine(embeddings[0].Vector.Length);
```

## Initialization Patterns

### Standard direct SDK

```csharp
using Jina;
using Microsoft.Extensions.AI;

IEmbeddingGenerator<string, Embedding<float>> generator = new JinaClient(apiKey);
```

### Alias-sensitive SDK

```csharp
using Pinecone;
using Meai = Microsoft.Extensions.AI;

Meai.IEmbeddingGenerator<string, Meai.Embedding<float>> generator =
    new PineconeClient(apiKey).Inference;
```

### OpenAI-compatible provider

```csharp
using Microsoft.Extensions.AI;
using tryAGI.OpenAI;

IEmbeddingGenerator<string, Embedding<float>> generator =
    CustomProviders.DeepInfra(apiKey);

var embeddings = await generator.GenerateAsync(
    ["Hello, world!"],
    new EmbeddingGenerationOptions { ModelId = "BAAI/bge-en-icl" });
```

## Provider-Specific Notes

- `Mixedbread` and `Nomic` expose matryoshka-style dimension reduction.
- `Pinecone` is the direct MEAI adapter for the inference surface, not the vector database CRUD APIs.
- `TwelveLabs` is currently the most constrained adapter in this group: text-only, sequential batching, and no custom dimensions.
- `Upstage` and `OpenAI` both expose token usage in the generated embedding responses.

## SDK Guides

- [Ollama](https://tryagi.github.io/Ollama/guides/meai/)
- [OpenAI](https://tryagi.github.io/OpenAI/guides/meai/)
- [Google.Gemini](https://tryagi.github.io/Google_Generative_AI/guides/meai/)
- [Cohere](https://tryagi.github.io/Cohere/guides/meai/)
- [Together](https://tryagi.github.io/Together/guides/meai/)
- [HuggingFace](https://tryagi.github.io/HuggingFace/guides/meai/)
- [Jina](https://tryagi.github.io/Jina/guides/meai/)
- [VoyageAI](https://tryagi.github.io/VoyageAI/guides/meai/)
- [TwelveLabs](https://tryagi.github.io/TwelveLabs/guides/meai/)
- [Mixedbread](https://tryagi.github.io/Mixedbread/guides/meai/)
- [Nomic](https://tryagi.github.io/Nomic/guides/meai/)
- [Pinecone](https://tryagi.github.io/Pinecone/guides/meai/)
- [Upstage](https://tryagi.github.io/Upstage/guides/meai/)
