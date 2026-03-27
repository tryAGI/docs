# IEmbeddingGenerator Feature Matrix

The `IEmbeddingGenerator<string, Embedding<float>>` interface provides a unified API for text embeddings across all supported providers.

## Feature comparison

| Feature | Ollama | OpenAI | Gemini | Cohere | Together | HuggingFace | Jina | VoyageAI | TwelveLabs | Mixedbread |
|---------|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| Single input | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y |
| Batch input | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y |
| Custom dimensions | Y | Y | - | - | - | Y | Y | Y | - | Y |
| Token usage | Y | Y | - | - | - | Y | Y | Y | - | Y |

## Universal code example

```csharp
using Microsoft.Extensions.AI;

IEmbeddingGenerator<string, Embedding<float>> generator = /* any provider */;

// Single embedding
var embedding = await generator.GenerateAsync("Hello, world!");
float[] vector = embedding[0].Vector.ToArray();

// Batch embeddings
var embeddings = await generator.GenerateAsync([
    "First document",
    "Second document",
    "Third document"
]);
```

## Provider-specific initialization

=== "OpenAI"

    ```csharp
    IEmbeddingGenerator<string, Embedding<float>> generator =
        new OpenAiClient(apiKey)
            .AsEmbeddingGenerator("text-embedding-3-small");
    ```

=== "Ollama"

    ```csharp
    IEmbeddingGenerator<string, Embedding<float>> generator =
        new OllamaApiClient()
            .AsEmbeddingGenerator("nomic-embed-text");
    ```

=== "Jina"

    ```csharp
    IEmbeddingGenerator<string, Embedding<float>> generator =
        new JinaClient(apiKey)
            .AsEmbeddingGenerator("jina-embeddings-v3");
    ```

=== "VoyageAI"

    ```csharp
    IEmbeddingGenerator<string, Embedding<float>> generator =
        new VoyageAiClient(apiKey)
            .AsEmbeddingGenerator("voyage-3");
    ```

=== "TwelveLabs"

    ```csharp
    // Direct cast — TwelveLabsClient implements IEmbeddingGenerator
    IEmbeddingGenerator<string, Embedding<float>> generator =
        new TwelveLabsClient(apiKey);
    ```

=== "Mixedbread"

    ```csharp
    // Note: namespace conflict — use Meai alias
    using Meai = Microsoft.Extensions.AI;
    Meai.IEmbeddingGenerator<string, Meai.Embedding<float>> generator =
        new MixedbreadClient(apiKey);
    ```

## Per-SDK documentation

| SDK | Documentation |
|-----|--------------|
| Ollama | [tryagi.github.io/Ollama/guides/meai/](https://tryagi.github.io/Ollama/guides/meai/) |
| OpenAI | [tryagi.github.io/OpenAI/guides/meai/](https://tryagi.github.io/OpenAI/guides/meai/) |
| Google.Gemini | [tryagi.github.io/Google_Generative_AI/guides/meai/](https://tryagi.github.io/Google_Generative_AI/guides/meai/) |
| Cohere | [tryagi.github.io/Cohere/guides/meai/](https://tryagi.github.io/Cohere/guides/meai/) |
| Together | [tryagi.github.io/Together/guides/meai/](https://tryagi.github.io/Together/guides/meai/) |
| HuggingFace | [tryagi.github.io/HuggingFace/guides/meai/](https://tryagi.github.io/HuggingFace/guides/meai/) |
| Jina | [tryagi.github.io/Jina/guides/meai/](https://tryagi.github.io/Jina/guides/meai/) |
| VoyageAI | [tryagi.github.io/VoyageAI/guides/meai/](https://tryagi.github.io/VoyageAI/guides/meai/) |
| TwelveLabs | [tryagi.github.io/TwelveLabs/guides/meai/](https://tryagi.github.io/TwelveLabs/guides/meai/) |
| Mixedbread | [tryagi.github.io/Mixedbread/guides/meai/](https://tryagi.github.io/Mixedbread/guides/meai/) |
