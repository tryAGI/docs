# Microsoft.Extensions.AI (MEAI) Overview

This overview reflects the MEAI implementations that currently exist in the tryAGI SDKs.

tryAGI currently ships:

- 14 direct `IChatClient` implementations
- 13 direct `IEmbeddingGenerator<string, Embedding<float>>` implementations
- 10 direct `ISpeechToTextClient` implementations
- dozens of SDKs with `AIFunction` wrappers
- 27 OpenAI-compatible factories in `tryAGI.OpenAI.CustomProviders`

All current implementations target **Microsoft.Extensions.AI.Abstractions 10.4.1**.

## Direct Interface Coverage

| SDK | `IChatClient` | `IEmbeddingGenerator` | `ISpeechToTextClient` | `AIFunction` | Alias recommended |
|-----|:---:|:---:|:---:|:---:|:---:|
| [AI21](https://tryagi.github.io/AI21/guides/meai/) | Y | - | - | - | No |
| [Anthropic](https://tryagi.github.io/Anthropic/guides/meai/) | Y | - | - | - | No |
| [AssemblyAI](https://tryagi.github.io/AssemblyAI/guides/meai/) | - | - | Y | - | No |
| [Cartesia](https://tryagi.github.io/Cartesia/guides/meai/) | - | - | Y | - | No |
| [Cohere](https://tryagi.github.io/Cohere/guides/meai/) | Y | Y | - | - | Yes |
| [Coze](https://tryagi.github.io/Coze/guides/meai/) | Y | - | - | - | No |
| [Deepgram](https://tryagi.github.io/Deepgram/guides/meai/) | - | - | Y | - | No |
| [ElevenLabs](https://tryagi.github.io/ElevenLabs/guides/meai/) | - | - | Y | - | Yes |
| [FishAudio](https://tryagi.github.io/FishAudio/guides/meai/) | - | - | Y | Y | No |
| [Gladia](https://tryagi.github.io/Gladia/guides/meai/) | - | - | Y | - | No |
| [Google.Gemini](https://tryagi.github.io/Google_Generative_AI/guides/meai/) | Y | Y | - | - | No |
| [HuggingFace](https://tryagi.github.io/HuggingFace/guides/meai/) | Y | Y | - | - | No |
| [Jina](https://tryagi.github.io/Jina/guides/meai/) | - | Y | - | - | No |
| [Mistral](https://tryagi.github.io/Mistral/guides/meai/) | Y | - | - | - | Yes |
| [Mixedbread](https://tryagi.github.io/Mixedbread/guides/meai/) | - | Y | - | - | Yes |
| [Nomic](https://tryagi.github.io/Nomic/guides/meai/) | - | Y | - | Y | No |
| [Ollama](https://tryagi.github.io/Ollama/guides/meai/) | Y | Y | - | - | No |
| [OpenAI](https://tryagi.github.io/OpenAI/guides/meai/) | Y | Y | - | - | Yes |
| [Pinecone](https://tryagi.github.io/Pinecone/guides/meai/) | - | Y | - | Y | Yes |
| [Reka](https://tryagi.github.io/Reka/guides/meai/) | Y | - | Y | - | Yes |
| [RevAI](https://tryagi.github.io/RevAI/guides/meai/) | - | - | Y | Y | No |
| [SarvamAI](https://tryagi.github.io/SarvamAI/guides/meai/) | Y | - | Y | Y | No |
| [Speechmatics](https://tryagi.github.io/Speechmatics/guides/meai/) | - | - | Y | Y | No |
| [Together](https://tryagi.github.io/Together/guides/meai/) | Y | Y | - | - | Yes |
| [TwelveLabs](https://tryagi.github.io/TwelveLabs/guides/meai/) | - | Y | - | - | No |
| [Upstage](https://tryagi.github.io/Upstage/guides/meai/) | Y | Y | - | Y | Yes |
| [VoyageAI](https://tryagi.github.io/VoyageAI/guides/meai/) | - | Y | - | - | No |
| [Writer](https://tryagi.github.io/Writer/guides/meai/) | Y | - | - | - | Yes |

## Tool Wrapper Coverage

The centralized docs previously listed only a small subset of tool-enabled SDKs. The current coverage is much broader:

- Search, retrieval, vector, and memory: `Algolia`, `BraveSearch`, `Browserbase`, `Exa`, `GroundX`, `LlamaParse`, `Milvus`, `Nomic`, `Pinecone`, `Recombee`, `ScrapeGraphAI`, `Serper`, `Tavily`, `Vectara`, `Zep`
- Translation, speech, and media generation: `Creatomate`, `DeepL`, `DId`, `FishAudio`, `HumeAI`, `KlingAI`, `LalalAI`, `Loudly`, `MagicHour`, `ModernMT`, `Murf`, `Photoroom`, `Picsart`, `RevAI`, `SarvamAI`, `Shotstack`, `SiliconFlow`, `Speechmatics`, `Synthesia`, `Tavus`, `Upstage`, `WaveSpeedAI`
- Agents, prompts, observability, and workflows: `Apify`, `Baseten`, `Botpress`, `Braintrust`, `CursorAgents`, `Dust`, `Gretel`, `HammingAI`, `Helicone`, `Humanloop`, `JasperAI`, `Julep`, `Martian`, `Novu`, `OpenRouter`, `Opik`, `Phoenix`, `Predibase`, `PromptLayer`, `RetellAI`, `Resend`, `Vapi`, `Vellum`, `Weave`, `Writesonic`
- Security, moderation, document AI, and data operations: `Composio`, `CVAT`, `Dataloop`, `EdenAI`, `Greptile`, `Guardrails`, `Lakera`, `LabelStudio`, `ModerationAPI`, `Nanonets`, `NightfallAI`, `PredictionGuard`, `Reducto`, `Roboflow`, `ScaleAI`, `Sightengine`

See [AIFunction Tools](aifunction-tools.md) for the organized inventory and usage pattern.

## OpenAI-Compatible Coverage

`tryAGI.OpenAI` exposes **27** `CustomProviders` factory methods. That covers hosted providers such as `DeepInfra`, `Groq`, `DeepSeek`, `Together`, `OpenRouter`, `Nebius`, `Nvidia`, `Minimax`, `Qwen`, `SiliconFlow`, and local runtimes such as `Ollama` and `LM Studio`.

See [CustomProviders](custom-providers.md) for the full table.

## Interfaces

| Interface | Purpose | Guide |
|-----------|---------|-------|
| `IChatClient` | Chat completions, streaming, tool calling, multimodal input, and structured output where the provider supports it | [Chat Client](chat-client.md) |
| `IEmbeddingGenerator<string, Embedding<float>>` | Text embeddings | [Embedding Generator](embedding-generator.md) |
| `ISpeechToTextClient` | Speech-to-text transcription | [Speech to Text](speech-to-text.md) |
| `AIFunction` | Tool/function wrappers for use with any `IChatClient` | [AIFunction Tools](aifunction-tools.md) |

## Implementation Pattern

MEAI implementations are hand-written partial classes in each SDK, located outside generated code:

```text
src/libs/{SdkName}/Extensions/
  {ClientName}.ChatClient.cs
  {ClientName}.EmbeddingGenerator.cs
  {ClientName}.SpeechToTextClient.cs
  {ClientName}.AsTool.cs / {ClientName}.Tools.cs
```

The reference chat implementation is [AnthropicClient.ChatClient.cs](https://github.com/tryAGI/Anthropic/blob/main/src/libs/Anthropic/Extensions/AnthropicClient.ChatClient.cs).

## Gaps Worth Fixing Next

- `Coze` now has a published MEAI guide page, but its adapter still needs full `FunctionCallContent` round-tripping for provider-issued tool calls.
- `PredictionGuard` is still tool-only even though it is a realistic candidate for a dedicated `IChatClient` adapter.
- Only `Deepgram` currently provides truly incremental `ISpeechToTextClient.GetStreamingTextAsync()` updates. Several other STT SDKs expose the method but return the final transcript after processing completes.
- `OpenRouter` and the standalone `Xai` SDK do not need urgent dedicated MEAI adapters because `tryAGI.OpenAI.CustomProviders` already covers the common chat and embedding path.
