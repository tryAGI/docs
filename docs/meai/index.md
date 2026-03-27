# Microsoft.Extensions.AI (MEAI) Overview

All tryAGI SDKs with MEAI support use **Microsoft.Extensions.AI.Abstractions 10.4.1**.

## Quick reference

| SDK | `IChatClient` | `IEmbeddingGenerator` | `ISpeechToTextClient` | `AIFunction` | Namespace Conflict |
|-----|:---:|:---:|:---:|:---:|:---:|
| [Anthropic](https://tryagi.github.io/Anthropic/guides/meai/) | Y | - | - | - | No |
| [Ollama](https://tryagi.github.io/Ollama/guides/meai/) | Y | Y | - | - | No |
| [OpenAI](https://tryagi.github.io/OpenAI/guides/meai/) | Y | Y | - | - | Yes |
| [Google.Gemini](https://tryagi.github.io/Google_Generative_AI/guides/meai/) | Y | Y | - | - | No |
| [Mistral](https://tryagi.github.io/Mistral/guides/meai/) | Y | - | - | - | Yes |
| [Cohere](https://tryagi.github.io/Cohere/guides/meai/) | Y | Y | - | - | Yes |
| [Together](https://tryagi.github.io/Together/guides/meai/) | Y | Y | - | - | Yes |
| [AI21](https://tryagi.github.io/AI21/guides/meai/) | Y | - | - | - | No |
| [Reka](https://tryagi.github.io/Reka/guides/meai/) | Y | - | Y | - | Yes |
| [HuggingFace](https://tryagi.github.io/HuggingFace/guides/meai/) | Y | Y | - | - | No |
| [Writer](https://tryagi.github.io/Writer/guides/meai/) | Y | - | - | - | Yes |
| [Jina](https://tryagi.github.io/Jina/guides/meai/) | - | Y | - | - | No |
| [VoyageAI](https://tryagi.github.io/VoyageAI/guides/meai/) | - | Y | - | - | No |
| [TwelveLabs](https://tryagi.github.io/TwelveLabs/guides/meai/) | - | Y | - | - | No |
| [Mixedbread](https://tryagi.github.io/Mixedbread/guides/meai/) | - | Y | - | - | Yes |
| [ElevenLabs](https://tryagi.github.io/ElevenLabs/guides/meai/) | - | - | Y | - | No |
| [AssemblyAI](https://tryagi.github.io/AssemblyAI/guides/meai/) | - | - | Y | - | No |
| [Deepgram](https://tryagi.github.io/Deepgram/guides/meai/) | - | - | Y | - | No |
| [Gladia](https://tryagi.github.io/Gladia/guides/meai/) | - | - | Y | - | No |
| [Cartesia](https://tryagi.github.io/Cartesia/guides/meai/) | - | - | Y | - | No |
| [DeepL](https://tryagi.github.io/DeepL/guides/meai/) | - | - | - | Y | No |
| [Exa](https://tryagi.github.io/Exa/guides/meai/) | - | - | - | Y | No |
| [Serper](https://tryagi.github.io/Serper/guides/meai/) | - | - | - | Y | No |
| [Tavily](https://tryagi.github.io/Tavily/guides/meai/) | - | - | - | Y | No |
| [Phoenix](https://tryagi.github.io/Phoenix/guides/meai/) | - | - | - | Y | No |

Additionally, **21 OpenAI-compatible providers** get MEAI support via [`CustomProviders`](custom-providers.md) in `tryAGI.OpenAI`.

## Interfaces

| Interface | Purpose | Guide |
|-----------|---------|-------|
| `IChatClient` | Chat completions — text, streaming, tool calling, images | [Chat Client](chat-client.md) |
| `IEmbeddingGenerator<string, Embedding<float>>` | Text embeddings | [Embedding Generator](embedding-generator.md) |
| `ISpeechToTextClient` | Speech-to-text transcription | [Speech to Text](speech-to-text.md) |
| `AIFunction` | Tool/function wrappers for use with any `IChatClient` | [AIFunction Tools](aifunction-tools.md) |

## Implementation pattern

MEAI implementations are hand-written partial classes in each SDK, located outside the `Generated/` directory:

```
src/libs/{SdkName}/Extensions/
  {ClientName}.ChatClient.cs          # IChatClient
  {ClientName}.EmbeddingGenerator.cs  # IEmbeddingGenerator
  {ClientName}.SpeechToTextClient.cs  # ISpeechToTextClient
```

The reference implementation is [AnthropicClient.ChatClient.cs](https://github.com/tryAGI/Anthropic/blob/main/src/libs/Anthropic/Extensions/AnthropicClient.ChatClient.cs).
