# AIFunction Tools

Some tryAGI SDKs expose `AIFunction` tool wrappers from [Microsoft.Extensions.AI](https://learn.microsoft.com/en-us/dotnet/ai/microsoft-extensions-ai). These let you add specialized capabilities (search, translation, observability) to any `IChatClient` conversation.

## Available Tool SDKs

| SDK | Tools | Description |
|-----|-------|-------------|
| [DeepL](https://tryagi.github.io/DeepL/guides/meai/) | `AsTranslateTool()`, `AsRephraseTool()`, `AsTranslateDocumentTool()` | Translation, rephrasing, document translation |
| [Exa](https://tryagi.github.io/Exa/guides/meai/) | `AsSearchTool()`, `AsGetContentsTool()`, `AsAnswerTool()` | AI-powered web search, content extraction, RAG answers |
| [Serper](https://tryagi.github.io/Serper/guides/meai/) | `AsSearchTool()`, `AsNewsTool()` | Google Search and Google News |
| [Tavily](https://tryagi.github.io/Tavily/guides/meai/) | `AsSearchTool()`, `AsExtractTool()` | Web search and content extraction |
| [Phoenix](https://tryagi.github.io/Phoenix/guides/meai/) | `AsGetPromptTool()`, `AsListPromptsTool()`, `AsAnnotateSpanTool()`, `AsListTracesTool()` | Observability — prompt management, trace annotation |

## Usage Pattern

All tool SDKs follow the same pattern — call an `As*Tool()` extension method on the client, then add the resulting `AIFunction` to `ChatOptions.Tools`:

```csharp
using Microsoft.Extensions.AI;

var options = new ChatOptions
{
    Tools = [client.AsSearchTool(numResults: 5)],
};

var response = await chatClient.GetResponseAsync(
    "What are the latest developments in quantum computing?",
    options);
```

## Combining Tools from Multiple SDKs

The key advantage of the `AIFunction` pattern is composability — tools from different SDKs work together in a single conversation:

```csharp
using Microsoft.Extensions.AI;
using DeepL;
using Exa;
using Serper;

var deepLClient = new DeepLClient(apiKey: deeplKey);
var exaClient = new ExaClient(apiKey: exaKey);
var serperClient = new SerperClient(apiKey: serperKey);

var options = new ChatOptions
{
    Tools =
    [
        // Search
        exaClient.AsSearchTool(numResults: 5),
        exaClient.AsGetContentsTool(),
        serperClient.AsNewsTool(numResults: 5),

        // Translation & writing
        deepLClient.AsTranslateTool(),
        deepLClient.AsRephraseTool(),
    ],
};

var response = await chatClient.GetResponseAsync(
    "Find recent EU AI regulations, translate key points to Japanese, " +
    "and rephrase them in a business-friendly tone.",
    options);
```

## Installation

Each SDK is independent — add only the ones you need:

```bash
dotnet add package DeepL        # Translation tools
dotnet add package Exa          # AI search tools
dotnet add package Serper       # Google search tools
dotnet add package tryAGI.Tavily   # Web search tools
dotnet add package tryAGI.Phoenix  # Observability tools
```

## How It Works

Under the hood, each `As*Tool()` method uses `AIFunctionFactory.Create()` from `Microsoft.Extensions.AI` to wrap an async method as an `AIFunction`. The LLM sees the tool's name, description, and JSON Schema parameters, and can invoke it during a conversation. The tool executes the SDK's API call and returns the result as structured text.

!!! tip "See also"
    - [DeepL Combined Tools Guide](https://tryagi.github.io/DeepL/guides/combined-tools/) — full examples of search + translation workflows
    - [IChatClient Guide](chat-client.md) — how chat clients work with tools
