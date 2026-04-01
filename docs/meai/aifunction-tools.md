# AIFunction Tools

Many tryAGI SDKs expose `AIFunction` wrappers built on top of [Microsoft.Extensions.AI](https://learn.microsoft.com/en-us/dotnet/ai/microsoft-extensions-ai). These wrappers let any `IChatClient` call provider-specific capabilities such as search, translation, prompt management, browser automation, moderation, or media generation.

## Usage Pattern

Every tool SDK follows the same pattern: create a client, call `As*Tool()`, and pass the result into `ChatOptions.Tools`.

```csharp
using Microsoft.Extensions.AI;

var options = new ChatOptions
{
    Tools =
    [
        searchClient.AsSearchTool(),
        translateClient.AsTranslateTool(),
    ],
};

var response = await chatClient.GetResponseAsync(
    "Find the latest updates and translate the summary to Japanese.",
    options);
```

## Coverage By Category

The current tool-wrapper inventory spans far beyond the original shortlist.

### Search, Retrieval, Vector, and Memory

- `Algolia`
- `BraveSearch`
- `Browserbase`
- `Exa`
- `GroundX`
- `LlamaParse`
- `Milvus`
- `Nomic`
- `Pinecone`
- `Recombee`
- `ScrapeGraphAI`
- `Serper`
- `Tavily`
- `Vectara`
- `Zep`

Typical methods in this group include `AsSearchTool()`, `AsExtractTool()`, `AsRerankTool()`, `AsSearchMemoryTool()`, `AsParseUrlTool()`, and `AsSearchVectorsTool()`.

### Translation, Transcription, and Document/Media Processing

- `Creatomate`
- `DeepL`
- `DId`
- `FishAudio`
- `HumeAI`
- `KlingAI`
- `LalalAI`
- `Loudly`
- `MagicHour`
- `Meshy`
- `ModernMT`
- `Murf`
- `Nanonets`
- `Photoroom`
- `Picsart`
- `Reducto`
- `RevAI`
- `SarvamAI`
- `Shotstack`
- `SiliconFlow`
- `Speechmatics`
- `Synthesia`
- `Tavus`
- `Upstage`
- `WaveSpeedAI`

Typical methods in this group include `AsTranslateTool()`, `AsTranscribeUrlTool()`, `AsTextToSpeechTool()`, `AsTextToVideoTool()`, `AsGenerateImageTool()`, `AsDocumentParseTool()`, and `AsParseDocumentTool()`.

### Agents, Prompts, Observability, and App Workflows

- `Apify`
- `Baseten`
- `Botpress`
- `Braintrust`
- `CursorAgents`
- `Dust`
- `Gretel`
- `HammingAI`
- `Helicone`
- `Humanloop`
- `JasperAI`
- `Julep`
- `Martian`
- `Novu`
- `OpenRouter`
- `Opik`
- `Phoenix`
- `Predibase`
- `PromptLayer`
- `RetellAI`
- `Resend`
- `Vapi`
- `Vellum`
- `Weave`
- `Writesonic`

Typical methods in this group include `AsCreateAgentTool()`, `AsGetPromptTool()`, `AsListTracesTool()`, `AsGetTotalCostTool()`, `AsExecutePromptTool()`, `AsCreateConversationTool()`, and `AsSendEmailTool()`.

### Security, Moderation, Evaluation, Data, and Platform Ops

- `Composio`
- `CVAT`
- `Dataloop`
- `EdenAI`
- `Greptile`
- `Guardrails`
- `Lakera`
- `LabelStudio`
- `ModerationAPI`
- `NightfallAI`
- `Nixtla`
- `PredictionGuard`
- `Roboflow`
- `ScaleAI`
- `Sightengine`

Typical methods in this group include `AsExecuteToolTool()`, `AsValidateTool()`, `AsGuardTool()`, `AsModerateTextTool()`, `AsForecastTool()`, `AsObjectDetectionTool()`, and `AsGetBatchStatusTool()`.

## Representative SDK Map

This table is intentionally representative, not exhaustive. It shows the breadth of the current surface while keeping the page readable.

| SDK | Representative methods | Best for |
|-----|------------------------|----------|
| [Tavily](https://tryagi.github.io/Tavily/guides/meai/) | `AsSearchTool()`, `AsExtractTool()` | Web search and page extraction |
| [Exa](https://tryagi.github.io/Exa/guides/meai/) | `AsSearchTool()`, `AsGetContentsTool()`, `AsAnswerTool()` | Search + content fetch + answer generation |
| [Serper](https://tryagi.github.io/Serper/guides/meai/) | `AsSearchTool()`, `AsNewsTool()` | Google-style search and news |
| [Pinecone](https://tryagi.github.io/Pinecone/guides/meai/) | `AsEmbedTool()`, `AsRerankTool()`, `AsListIndexesTool()` | Embeddings, reranking, index discovery |
| [Zep](https://tryagi.github.io/Zep/guides/meai/) | `AsAddMemoryTool()`, `AsSearchMemoryTool()`, `AsGetContextTool()` | Conversational memory |
| [DeepL](https://tryagi.github.io/DeepL/guides/meai/) | `AsTranslateTool()`, `AsRephraseTool()`, `AsTranslateDocumentTool()` | Translation and rewriting |
| [SarvamAI](https://tryagi.github.io/SarvamAI/guides/meai/) | `AsTranslateTool()`, `AsTransliterateTool()`, `AsDetectLanguageTool()` | Indian-language tooling |
| [Upstage](https://tryagi.github.io/Upstage/guides/meai/) | `AsGroundednessCheckTool()`, `AsTranslateTool()`, `AsDocumentParseTool()` | Groundedness checks and document parsing |
| [FishAudio](https://tryagi.github.io/FishAudio/guides/meai/) | `AsTextToSpeechTool()`, `AsListModelsTool()` | Speech synthesis and model inspection |
| [KlingAI](https://tryagi.github.io/KlingAI/guides/meai/) | `AsTextToVideoTool()`, `AsImageToVideoTool()`, `AsImageGenerationTool()` | Video and image generation |
| [Braintrust](https://tryagi.github.io/Braintrust/guides/meai/) | `AsListPromptsTool()`, `AsGetPromptTool()`, `AsListExperimentsTool()` | Prompt and experiment management |
| [Phoenix](https://tryagi.github.io/Phoenix/guides/meai/) | `AsGetPromptTool()`, `AsListPromptsTool()`, `AsListTracesTool()` | LLM observability |
| [Opik](https://tryagi.github.io/Opik/guides/meai/) | `AsCreateProjectTool()`, `AsCreateTraceTool()`, `AsCreateSpanTool()` | Projects, traces, and spans |
| [CursorAgents](https://tryagi.github.io/CursorAgents/guides/meai/) | `AsCreateAgentTool()`, `AsListAgentsTool()`, `AsGetAgentTool()` | Agent lifecycle management |
| [Vapi](https://tryagi.github.io/Vapi/guides/meai/) | `AsCreateAssistantTool()`, `AsListCallsTool()`, `AsListPhoneNumbersTool()` | Voice assistants and call operations |
| [Resend](https://tryagi.github.io/Resend/guides/meai/) | `AsSendEmailTool()`, `AsListDomainsTool()`, `AsListTemplatesTool()` | Transactional email workflows |
| [Composio](https://tryagi.github.io/Composio/guides/meai/) | `AsExecuteToolTool()`, `AsListToolsTool()`, `AsListConnectedAccountsTool()` | External app/tool execution |
| [Guardrails](https://tryagi.github.io/Guardrails/guides/meai/) | `AsValidateTool()`, `AsListGuardsTool()`, `AsGetGuardTool()` | Output validation and policy checks |
| [PredictionGuard](https://tryagi.github.io/PredictionGuard/guides/meai/) | `AsFactualityCheckTool()`, `AsToxicityCheckTool()`, `AsPiiDetectionTool()` | Safety and evaluation |
| [Reducto](https://tryagi.github.io/Reducto/guides/meai/) | `AsParseDocumentTool()`, `AsExtractDataTool()`, `AsClassifyDocumentTool()` | Document parsing and extraction |

## Installation

Each tool SDK is independent. Add only the packages you need, using the package ID shown in the provider's own guide page.

## Notes

- Some SDKs combine direct MEAI interfaces and tool wrappers. Important examples are `FishAudio`, `Nomic`, `Pinecone`, `RevAI`, `SarvamAI`, `Speechmatics`, and `Upstage`.
- Tool wrappers are especially useful when a provider is not itself an LLM but still exposes functionality that an `IChatClient` can orchestrate.
- The dedicated SDK guide remains the best place to find the exact `As*Tool()` methods and parameter details for a given provider.
