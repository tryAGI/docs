# Official SDK Comparison Inventory

Last updated: 2026-05-07.

This page tracks first-party or provider-endorsed SDKs for the generated tryAGI SDK workspace. The goal is to make AutoSDK quality work concrete: for each provider, compare the generated C# client against the best official client surface available, then file focused AutoSDK issues for recurring gaps.

Scope is the local SDK inventory detected from `*/src/libs/*/generate.sh`. When no official SDK was found in this pass, the row says so explicitly and should be rechecked before filing a provider-specific issue.

## How to Use This

1. Start with rows marked `.NET`; these give the most direct C# ergonomics comparison.
2. For rows marked `SDK`, compare against the provider's official Python, TypeScript, Java, Go, or CLI SDK and extract language-neutral generator gaps.
3. For rows marked `Docs`, compare against the official API docs and OpenAPI source instead of assuming a client exists.
4. File AutoSDK issues only when the gap is reusable across providers, such as pagination, builders, streaming, file upload ergonomics, retries, auth hooks, error models, nullable annotations, or discriminated unions.

## Issue Template

```markdown
## Provider and official client
- tryAGI SDK:
- Official SDK/docs:
- AutoSDK-generated surface:

## Gap
Describe the smallest developer-experience or correctness gap.

## Expected generator behavior
Describe the reusable AutoSDK behavior, not a one-off provider patch.

## Evidence
- Official SDK code/docs link:
- Generated code path:
- Minimal failing or awkward usage sample:
```

## Filed AutoSDK Gap Issues

| Issue | Gap | Comparison evidence |
|-------|-----|---------------------|
| [#298](https://github.com/tryAGI/AutoSDK/issues/298) | Cloud credential and request-signing adapters | AWS SDK for .NET, Azure AI Inference, Tencent Cloud .NET, Anthropic cloud-provider clients |
| [#299](https://github.com/tryAGI/AutoSDK/issues/299) | Opt-in raw JSON preservation | Official C# SDKs preserve unknown model data for forward compatibility |
| [#300](https://github.com/tryAGI/AutoSDK/issues/300) | Richer union accessors and result-returning match helpers | Official OpenAI/Anthropic-style clients provide more ergonomic union handling than `Value1`/`Value2` |
| [#301](https://github.com/tryAGI/AutoSDK/issues/301) | AWS EventStream typed streaming methods | AWS Bedrock runtime and Cohere cloud-provider streaming clients |
| [#302](https://github.com/tryAGI/AutoSDK/issues/302) | Environment-backed client factories and credential defaults | Groq, Cohere, ElevenLabs, Replicate, and Mistral official SDKs |
| [#303](https://github.com/tryAGI/AutoSDK/issues/303) | Webhook signature verification helpers | Replicate webhook validation and HMAC webhook settings in provider SDKs |
| [#304](https://github.com/tryAGI/AutoSDK/issues/304) | High-level create-wait-result workflow helpers | Replicate `run`/prediction helpers and Apify actor-run workflows |
| [#305](https://github.com/tryAGI/AutoSDK/issues/305) | Observability ingestion lifecycle helpers | LangSmith, Langfuse, Braintrust, and Helicone batching, tracing, flush/shutdown, and queue workers |
| [#306](https://github.com/tryAGI/AutoSDK/issues/306) | Dynamic multipart part names and attachment payload helpers | LangSmith multipart ingest, Braintrust attachments, and Helicone stream log bodies |
| [#307](https://github.com/tryAGI/AutoSDK/issues/307) | Prompt template manager helpers | Helicone prompt manager plus Langfuse, Braintrust, and LangSmith prompt workflows |
| [#308](https://github.com/tryAGI/AutoSDK/issues/308) | Dataset evaluation and experiment workflow helpers | Opik, Phoenix, and Weave dataset-backed eval, scorer, experiment, and feedback workflows |

## Observability Comparison Notes

| tryAGI SDK | Official SDKs checked | Captured gaps | Key SDK-quality signals |
|------------|-----------------------|---------------|-------------------------|
| `LangSmith` | [Python/JS SDK repo](https://github.com/langchain-ai/langsmith-sdk) | [#305](https://github.com/tryAGI/AutoSDK/issues/305), [#306](https://github.com/tryAGI/AutoSDK/issues/306), [#307](https://github.com/tryAGI/AutoSDK/issues/307) | `traceable`, OpenAI wrappers, RunTree propagation, queued batch ingestion, multipart/compressed ingest fallback, flush helpers, and env-backed tracing config. |
| `Langfuse` | [Python SDK](https://github.com/langfuse/langfuse-python), [JS/TS SDK](https://github.com/langfuse/langfuse-js) | [#305](https://github.com/tryAGI/AutoSDK/issues/305), [#307](https://github.com/tryAGI/AutoSDK/issues/307) | OpenTelemetry span processor, trace/span/generation helpers, score and media upload queues, sampling, flush/shutdown lifecycle, prompt cache, datasets, and batched evaluations. |
| `Braintrust` | [JS SDK](https://github.com/braintrustdata/braintrust-sdk), [Python SDK](https://github.com/braintrustdata/braintrust-sdk-python) | [#305](https://github.com/tryAGI/AutoSDK/issues/305), [#306](https://github.com/tryAGI/AutoSDK/issues/306), [#307](https://github.com/tryAGI/AutoSDK/issues/307) | Logger/span lifecycle APIs, decorators and auto-instrumentation, background logging, OpenTelemetry flush hooks, queue/drop controls, attachments, prompt/span caches, and eval helpers. |
| `Helicone` | [OSS repo and SDK helpers](https://github.com/Helicone/helicone) | [#305](https://github.com/tryAGI/AutoSDK/issues/305), [#306](https://github.com/tryAGI/AutoSDK/issues/306), [#307](https://github.com/tryAGI/AutoSDK/issues/307) | AI gateway base URL flow, async/manual loggers, stream capture, time-to-first-token tracking, provider-specific log routing, direct log submission, and prompt manager helpers. |
| `Opik` | [Python/TypeScript/Ruby SDKs](https://github.com/comet-ml/opik) | [#305](https://github.com/tryAGI/AutoSDK/issues/305), [#306](https://github.com/tryAGI/AutoSDK/issues/306), [#307](https://github.com/tryAGI/AutoSDK/issues/307), [#308](https://github.com/tryAGI/AutoSDK/issues/308) | OpenTelemetry and direct tracing integrations, decorators, background ingestion queues, attachment extraction/upload processing, `flush_tracker`/client flush lifecycle, prompt helpers, and `evaluate`/`evaluate_prompt`/thread evaluation workflows. |
| `Phoenix` | [Phoenix repo and Python/JS packages](https://github.com/Arize-ai/phoenix) | [#305](https://github.com/tryAGI/AutoSDK/issues/305), [#307](https://github.com/tryAGI/AutoSDK/issues/307), [#308](https://github.com/tryAGI/AutoSDK/issues/308) | Phoenix-aware OpenTelemetry registration, batch span processing, env-backed collector/project/auth configuration, prompt management, datasets, experiments, and eval packages. |
| `Weave` | [Python observability SDK](https://github.com/wandb/weave) | [#305](https://github.com/tryAGI/AutoSDK/issues/305), [#307](https://github.com/tryAGI/AutoSDK/issues/307), [#308](https://github.com/tryAGI/AutoSDK/issues/308) | `weave.init` and `@weave.op` tracing, batched call/feedback processors, queue and disk-fallback durability, WAL flush/close lifecycle, prompt formatting, evaluations, and scorer framework. |

## Status Legend

| Status | Meaning |
|--------|---------|
| `.NET` | First-party or provider-endorsed C#/.NET SDK exists. Highest-priority comparison target. |
| `Archived .NET` | Official .NET SDK exists but is archived or discontinued. Useful as historical API-shape evidence only. |
| `SDK` | Official non-.NET SDK exists. Use it for language-neutral generator quality gaps. |
| `Community` | Provider lists or tolerates the client, but it is not clearly first-party. |
| `Docs` | No official SDK found in this pass; compare against API docs, OpenAPI, or examples. |

## High-Priority .NET Targets

| tryAGI SDK | Official SDK | Gap issues | Notes |
|------------|--------------|------------|-------|
| `Algolia` | [algolia/algoliasearch-client-csharp](https://github.com/algolia/algoliasearch-client-csharp) | - | Official generated C# client with batching, retries, and typed request helpers. |
| `Anthropic` | [anthropics/anthropic-sdk-csharp](https://github.com/anthropics/anthropic-sdk-csharp) | [#298](https://github.com/tryAGI/AutoSDK/issues/298), [#299](https://github.com/tryAGI/AutoSDK/issues/299), [#300](https://github.com/tryAGI/AutoSDK/issues/300) | Official C# SDK is beta, but it is now the best direct Claude comparison. |
| `AssemblyAI` | [AssemblyAI/assemblyai-csharp-sdk](https://github.com/AssemblyAI/assemblyai-csharp-sdk) | - | Archived/discontinued in 2025; keep as historical comparison only. |
| `AwsBedrock` | [AWS SDK for .NET](https://github.com/aws/aws-sdk-net) | [#298](https://github.com/tryAGI/AutoSDK/issues/298), [#301](https://github.com/tryAGI/AutoSDK/issues/301) | Compare service-client conventions, auth, request marshalling, and streaming. |
| `Deepgram` | [deepgram/deepgram-dotnet-sdk](https://github.com/deepgram/deepgram-dotnet-sdk) | - | Strong target for REST plus realtime audio ergonomics. |
| `DeepL` | [DeepLcom/deepl-dotnet](https://github.com/DeepLcom/deepl-dotnet) | - | Strong target for auth, document upload/download, and glossary flows. |
| `MicrosoftFoundry` | [Azure AI Inference for .NET](https://learn.microsoft.com/en-us/dotnet/api/overview/azure/ai.inference-readme) | [#298](https://github.com/tryAGI/AutoSDK/issues/298) | Compare Azure SDK conventions and client factory patterns. |
| `Novu` | [Novu SDK docs](https://docs.novu.co/platform/sdks/overview) | - | Provider documents an official .NET server-side SDK. |
| `OpenAI` | [openai/openai-dotnet](https://github.com/openai/openai-dotnet) | [#299](https://github.com/tryAGI/AutoSDK/issues/299), [#300](https://github.com/tryAGI/AutoSDK/issues/300) | Best overall generator-quality benchmark for generated C# from OpenAPI. |
| `Pinecone` | [Pinecone .NET SDK](https://docs.pinecone.io/reference/dotnet-sdk) | - | Compare API-versioned generated SDK structure and data-plane ergonomics. |
| `Qdrant` | [qdrant/qdrant-dotnet](https://github.com/qdrant/qdrant-dotnet) | - | Compare REST/gRPC split, filters, and vector payload modeling. |
| `Recombee` | [Recombee SDK docs](https://docs.recombee.com/api_clients) | - | Provider lists .NET among official server-side SDKs. |
| `Resend` | [resend/resend-dotnet](https://github.com/resend/resend-dotnet) | - | Good small-surface target for request helpers and response errors. |
| `TencentTokenHub` | [Tencent Cloud .NET SDK](https://github.com/TencentCloud/tencentcloud-sdk-dotnet) | [#298](https://github.com/tryAGI/AutoSDK/issues/298) | Compare Tencent Cloud auth/signing conventions where applicable. |
| `Vapi` | [Vapi server SDK docs](https://docs.vapi.ai/server-sdks) | - | Provider documents a C# server SDK alongside TypeScript, Python, Java, Ruby, and Go. |
| `Weaviate` | [weaviate/csharp-client](https://github.com/weaviate/csharp-client) | - | Official C# client; compare schema, query, and gRPC ergonomics. |

## Full Inventory

| tryAGI SDK | Status | Gap issues | Official SDK or compare target | Notes |
|------------|--------|------------|--------------------------------|-------|
| `ACRCloud` | Docs | - | API docs/OpenAPI | No first-party .NET SDK found in this pass. |
| `AI21` | SDK | - | [AI21 Python SDK](https://github.com/AI21Labs/ai21-python) | No official .NET SDK found. |
| `APITemplate` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Algolia` | .NET | - | [C# client](https://github.com/algolia/algoliasearch-client-csharp) | High-priority .NET comparison target. |
| `Anam` | SDK | - | [JavaScript SDK](https://github.com/anam-org/javascript-sdk), [Python SDK](https://anam.ai/docs/sdk-reference/python-sdk) | Good realtime avatar/WebRTC comparison target. |
| `Anthropic` | .NET | [#298](https://github.com/tryAGI/AutoSDK/issues/298), [#299](https://github.com/tryAGI/AutoSDK/issues/299), [#300](https://github.com/tryAGI/AutoSDK/issues/300) | [C# SDK](https://github.com/anthropics/anthropic-sdk-csharp), [client SDK docs](https://platform.claude.com/docs/en/api/client-sdks) | High-priority .NET comparison target. |
| `Apify` | SDK | [#304](https://github.com/tryAGI/AutoSDK/issues/304) | [JavaScript client](https://github.com/apify/apify-client-js), [Python client](https://github.com/apify/apify-client-python) | No official .NET SDK found. |
| `Arcee` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `AssemblyAI` | Archived .NET | - | [Archived C# SDK](https://github.com/AssemblyAI/assemblyai-csharp-sdk), [Python SDK](https://github.com/AssemblyAI/assemblyai-python-sdk) | C# SDK was discontinued; Python remains useful for current API shape. |
| `AsyncAI` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `AudD` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `AvatarTalk` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `AwsBedrock` | .NET | [#298](https://github.com/tryAGI/AutoSDK/issues/298), [#301](https://github.com/tryAGI/AutoSDK/issues/301) | [AWS SDK for .NET](https://github.com/aws/aws-sdk-net) | Compare Bedrock Runtime client conventions. |
| `Baseten` | SDK | - | [Baseten performance client](https://docs.baseten.co/development/model/performance/performance-client) | Python/Node/Rust performance client; no official .NET SDK found. |
| `Beatoven` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `BlackForestLabs` | SDK | - | [FLUX inference repo](https://github.com/black-forest-labs/flux) | Official model/inference reference, not a REST client SDK. |
| `BlandAI` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `BlockadeLabs` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Botpress` | SDK | - | [Botpress repository](https://github.com/botpress/botpress) | Platform repo and JS ecosystem are useful; no .NET SDK found. |
| `Braintrust` | SDK | [#305](https://github.com/tryAGI/AutoSDK/issues/305), [#306](https://github.com/tryAGI/AutoSDK/issues/306), [#307](https://github.com/tryAGI/AutoSDK/issues/307) | [Braintrust SDKs](https://github.com/braintrustdata/braintrust-sdk) | Compare tracing/evals ergonomics and examples. |
| `BraveSearch` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Browserbase` | SDK | - | [Stagehand](https://github.com/browserbase/stagehand) | Older JS/Python SDK repos are deprecated; use current Browserbase docs before filing issues. |
| `BytePlusModelArk` | Docs | - | API docs/OpenAPI | No first-party .NET SDK found in this pass. |
| `CVAT` | SDK | - | [CVAT SDK docs](https://docs.cvat.ai/docs/api_sdk/sdk/) | Official Python SDK is the useful comparison target. |
| `Cartesia` | SDK | - | [Python SDK](https://github.com/cartesia-ai/cartesia-python), [JavaScript SDK](https://github.com/cartesia-ai/cartesia-js) | Stainless-hosted spec source. |
| `Chroma` | SDK | - | [Chroma first-party clients](https://docs.trychroma.com/reference/chroma-reference) | First-party clients are Python, TypeScript, and Rust. |
| `Cohere` | SDK | [#301](https://github.com/tryAGI/AutoSDK/issues/301), [#302](https://github.com/tryAGI/AutoSDK/issues/302) | [Cohere SDK docs](https://docs.cohere.com/v2/reference/about) | Official Python, TypeScript, Java, and Go SDKs. |
| `Composio` | SDK | - | [Composio SDK docs](https://docs.composio.dev/) | Official Python and TypeScript SDKs. |
| `Coze` | SDK | - | [JavaScript](https://github.com/coze-dev/coze-js), [Python](https://github.com/coze-dev/coze-py), [Java](https://github.com/coze-dev/coze-java), [Go](https://github.com/coze-dev/coze-go) | Multi-language official SDK set. |
| `Creatomate` | Docs | - | API docs/OpenAPI | No first-party .NET SDK found in this pass. |
| `CsmAi` | SDK | - | [CSM Python SDK](https://github.com/CommonSenseMachines/csm-ai) | Official Python comparison target. |
| `CursorAgents` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `DId` | SDK | - | [D-ID Agents SDK](https://github.com/de-id/agents-sdk) | TypeScript SDK covers agents/realtime surfaces. |
| `DashScope` | SDK | - | [DashScope SDK docs](https://help.aliyun.com/zh/model-studio/developer-reference/install-and-configure-the-sdk) | Official Alibaba Cloud SDK path; no .NET-specific client found. |
| `Dataloop` | SDK | - | [Dataloop Python SDK](https://github.com/dataloop-ai/dtlpy) | Official Python SDK and CLI. |
| `DeepInfra` | Docs | - | API docs/OpenAI-compatible examples | No first-party SDK found in this pass. |
| `DeepL` | .NET | - | [DeepL .NET](https://github.com/DeepLcom/deepl-dotnet) | High-priority .NET comparison target. |
| `Deepgram` | .NET | - | [Deepgram .NET](https://github.com/deepgram/deepgram-dotnet-sdk) | High-priority .NET comparison target. |
| `Descript` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `DoclingServe` | Docs | - | Docling Serve API/docs | Self-hosted service; no dedicated first-party client found. |
| `DoubaoSeed3D` | Docs | - | API docs/OpenAPI | No first-party .NET SDK found in this pass. |
| `Dust` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `E2B` | SDK | - | [E2B repository](https://github.com/e2b-dev/E2B) | Official SDKs live in the platform repo. |
| `EachLabs` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `EdenAI` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `EigenAI` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `ElevenLabs` | SDK | [#302](https://github.com/tryAGI/AutoSDK/issues/302), [#303](https://github.com/tryAGI/AutoSDK/issues/303) | [Python SDK](https://github.com/elevenlabs/elevenlabs-python), [JavaScript SDK](https://github.com/elevenlabs/elevenlabs-js), [SDK docs](https://elevenlabs.io/docs/eleven-api/resources/libraries/) | ElevenLabs lists .NET as third-party, not official. |
| `Exa` | SDK | - | [Python SDK](https://github.com/exa-labs/exa-py), [JavaScript SDK](https://github.com/exa-labs/exa-js) | Official SDKs. |
| `Fal` | SDK | - | [JavaScript SDK](https://github.com/fal-ai/fal-js) | Fal docs also include Python client examples. |
| `Firecrawl` | SDK | - | [Firecrawl SDK docs](https://docs.firecrawl.dev/sdks/overview) | Official Python, Node, Java, and CLI SDKs. |
| `Fireworks` | Docs | - | API docs/OpenAI-compatible examples | No first-party SDK found in this pass. |
| `FishAudio` | SDK | - | [Fish Audio Python SDK](https://github.com/fishaudio/fish-audio-python) | Official Python comparison target. |
| `Flowise` | Docs | - | API docs/OpenAPI | Flowise is OSS, but no separate first-party API SDK found. |
| `Forem` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Gamma` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Gladia` | SDK | - | [Gladia SDK docs](https://docs.gladia.io/chapters/integrations/sdk) | Official Python and JavaScript SDKs. |
| `Gonka` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Google.Gemini` | SDK | - | [Google GenAI SDK docs](https://ai.google.dev/gemini-api/docs/libraries) | Official Python, JavaScript/TypeScript, Go, and Java SDKs; no Gemini .NET SDK listed there. |
| `Gradium` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Greptile` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Gretel` | SDK | - | [Gretel Python client](https://github.com/gretelai/gretel-python-client) | GitHub repo is archived; recheck current docs before filing issues. |
| `Groq` | SDK | [#302](https://github.com/tryAGI/AutoSDK/issues/302) | [Python SDK](https://github.com/groq/groq-python), [TypeScript SDK](https://github.com/groq/groq-typescript) | Official Python and JS/TS only per current docs. |
| `GroundX` | SDK | - | [GroundX SDKs](https://github.com/groundxai/groundx-sdks) | Official SDK/spec repo. |
| `Guardrails` | SDK | - | [Guardrails API client/spec repo](https://github.com/guardrails-ai/guardrails-api-client) | Compare generated SDK strategy and spec layout. |
| `Haiper` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `HammingAI` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Hedra` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Helicone` | SDK | [#305](https://github.com/tryAGI/AutoSDK/issues/305), [#306](https://github.com/tryAGI/AutoSDK/issues/306), [#307](https://github.com/tryAGI/AutoSDK/issues/307) | [Helicone OSS repo and SDK helpers](https://github.com/Helicone/helicone) | No first-party .NET SDK found; compare gateway, async logging, manual logger, and prompt helper ergonomics. |
| `HeyGen` | Docs | - | [HeyGen developer docs](https://docs.heygen.com/docs/quick-start) | Current docs emphasize API/CLI; no official full REST SDK found in this pass. |
| `Hitem3D` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `HuggingFace` | SDK | - | [huggingface_hub](https://github.com/huggingface/huggingface_hub), [huggingface.js](https://github.com/huggingface/huggingface.js) | Official Python and JS ecosystems. |
| `Humanloop` | SDK | - | [Humanloop Node SDK](https://github.com/humanloop/humanloop-node) | Fern-generated TypeScript SDK reference used by local spec notes. |
| `HumeAI` | SDK | - | [Python SDK](https://github.com/HumeAI/hume-python-sdk), [TypeScript SDK](https://github.com/HumeAI/hume-typescript-sdk) | Official SDKs. |
| `Hyper3D` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Ideogram` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `ImagineArt` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Instill` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Inworld` | SDK | - | [Node.js Runtime SDK](https://docs.inworld.ai/docs/node/runtime-reference/overview), [Unity Runtime SDK](https://docs.inworld.ai/docs/Unity/runtime/runtime-reference/overview) | Official runtime SDKs exist; no REST .NET comparison target found in this pass. |
| `JasperAI` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Jina` | Docs | - | API docs/OpenAPI | Jina OSS libraries exist, but no first-party REST API SDK found in this pass. |
| `Julep` | SDK | - | [Julep repository](https://github.com/julep-ai/julep) | Official SDK/client code is in the platform repo. |
| `KlingAI` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Krea` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `LMNT` | SDK | - | [LMNT SDK docs](https://docs.lmnt.com/sdk/introduction) | Official Python, Node, and Unity SDKs. |
| `LTX` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `LabelStudio` | SDK | - | [Label Studio SDK](https://github.com/HumanSignal/label-studio-sdk) | Official Python SDK. |
| `Lakera` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `LalalAI` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `LangSmith` | SDK | [#305](https://github.com/tryAGI/AutoSDK/issues/305), [#306](https://github.com/tryAGI/AutoSDK/issues/306), [#307](https://github.com/tryAGI/AutoSDK/issues/307) | [LangSmith SDK](https://github.com/langchain-ai/langsmith-sdk) | Official SDK implementations. |
| `Langfuse` | SDK | [#305](https://github.com/tryAGI/AutoSDK/issues/305), [#307](https://github.com/tryAGI/AutoSDK/issues/307) | [JS/TS SDK](https://github.com/langfuse/langfuse-js), [Python SDK](https://github.com/langfuse/langfuse-python) | Compare tracing/observability ergonomics. |
| `Leonardo` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Letta` | SDK | - | [Letta SDK docs](https://docs.letta.com/api-overview/client-sdks) | Official Python and TypeScript SDKs. |
| `LlamaParse` | SDK | - | [LlamaParse API docs](https://developers.api.llamaindex.ai/cloud/llamaparse) | Compare LlamaCloud Python/TypeScript examples; no .NET SDK found. |
| `Loudly` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Luma` | SDK | - | [Luma Python SDK docs](https://docs.lumalabs.ai/docs/python) | Official Python SDK; Node package should be rechecked before filing JS-specific issues. |
| `MagicHour` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Martian` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Mem0` | SDK | - | [Mem0 SDK changelog](https://docs.mem0.ai/changelog/sdk) | Official Python and TypeScript SDK paths. |
| `Meshcapade` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Meshy` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `MicrosoftFoundry` | .NET | [#298](https://github.com/tryAGI/AutoSDK/issues/298) | [Azure AI Inference for .NET](https://learn.microsoft.com/en-us/dotnet/api/overview/azure/ai.inference-readme) | High-priority Azure SDK comparison target. |
| `Milvus` | SDK | - | [Milvus clients](https://milvus.io/docs/install-pymilvus.md) | Official Python, Node.js, Go, and Java clients; no official .NET SDK found. |
| `MiniMax` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Mistral` | SDK | [#302](https://github.com/tryAGI/AutoSDK/issues/302) | [Mistral SDK clients](https://docs.mistral.ai/getting-started/clients/) | Official Python and TypeScript SDKs. |
| `Mixedbread` | SDK | - | [Mixedbread Python SDK](https://github.com/mixedbread-ai/mixedbread-python) | Stainless-hosted spec source. |
| `ModerationAPI` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `ModernMT` | Docs | - | API docs/OpenAPI | No first-party .NET SDK found in this pass. |
| `Moonshot` | Docs | - | API docs/OpenAI-compatible examples | Use OpenAI-compatible behavior as the primary comparison. |
| `Mubert` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Mureka` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Murf` | SDK | - | [Murf Python SDK](https://github.com/murf-ai/murf-python-sdk) | Official Python comparison target. |
| `Nanonets` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Neon` | Docs | - | API docs/OpenAPI | Neon has database clients, but no first-party management API SDK found in this pass. |
| `Neuphonic` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Neural4D` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `NightfallAI` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Nixtla` | SDK | - | [Nixtla Python SDK](https://github.com/Nixtla/nixtla) | Official TimeGPT Python SDK. |
| `Nomic` | SDK | - | [Nomic Python client](https://github.com/nomic-ai/nomic) | Official Nomic Python client. |
| `Novu` | .NET | - | [Novu SDK docs](https://docs.novu.co/platform/sdks/overview) | Provider lists official server-side SDKs including .NET. |
| `Ollama` | SDK | - | [Ollama Python](https://github.com/ollama/ollama-python), [Ollama JavaScript](https://github.com/ollama/ollama-js) | Official Python and JS libraries. |
| `OpenAI` | .NET | [#299](https://github.com/tryAGI/AutoSDK/issues/299), [#300](https://github.com/tryAGI/AutoSDK/issues/300) | [OpenAI .NET](https://github.com/openai/openai-dotnet) | Highest-priority generator-quality benchmark. |
| `OpenRouter` | Docs | - | API docs/OpenAI-compatible examples | No first-party SDK found in this pass. |
| `Opik` | SDK | [#305](https://github.com/tryAGI/AutoSDK/issues/305), [#306](https://github.com/tryAGI/AutoSDK/issues/306), [#307](https://github.com/tryAGI/AutoSDK/issues/307), [#308](https://github.com/tryAGI/AutoSDK/issues/308) | [Opik repository](https://github.com/comet-ml/opik) | Official Python, TypeScript, and Ruby SDKs expose tracing lifecycle, attachment, prompt, and eval workflow helpers. |
| `Oura` | Docs | - | [Oura API docs](https://support.ouraring.com/hc/en-us/articles/4415266939155-The-Oura-API) | No first-party SDK found in this pass. |
| `PDF4Dev` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Phoenix` | SDK | [#305](https://github.com/tryAGI/AutoSDK/issues/305), [#307](https://github.com/tryAGI/AutoSDK/issues/307), [#308](https://github.com/tryAGI/AutoSDK/issues/308) | [Arize Phoenix](https://github.com/Arize-ai/phoenix) | Official Python and JavaScript packages cover OpenTelemetry tracing, prompt management, datasets, experiments, and evals. |
| `Photoroom` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Picsart` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Pika` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Pinecone` | .NET | - | [Pinecone .NET SDK docs](https://docs.pinecone.io/reference/dotnet-sdk), [GitHub](https://github.com/pinecone-io/pinecone-dotnet-client) | High-priority .NET comparison target. |
| `PixVerse` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `PlayHT` | SDK | - | [PlayHT Python SDK](https://github.com/playht/pyht) | Official Python comparison target. |
| `Polar` | SDK | - | [Polar SDK docs](https://docs.polar.sh/documentation/tools/polar-init), [polar-js](https://github.com/polarsource/polar-js) | Official JS, Python, Go, and PHP SDKs. |
| `Portkey` | SDK | - | [Portkey Python SDK](https://github.com/Portkey-AI/portkey-python-sdk) | Official gateway SDK target. |
| `Predibase` | SDK | - | [Predibase Python SDK docs](https://docs.predibase.com/user-guide/inference/overview) | Python SDK is the recommended provider path. |
| `PredictionGuard` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Presenton` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `PromptLayer` | SDK | - | [PromptLayer Python SDK docs](https://docs.promptlayer.com/sdks/python), [REST API reference](https://docs.promptlayer.com/reference/rest-api-reference) | Official Python and JavaScript SDK paths. |
| `Pruna` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Qdrant` | .NET | - | [Qdrant .NET SDK](https://github.com/qdrant/qdrant-dotnet) | High-priority .NET comparison target. |
| `Recombee` | .NET | - | [Recombee API clients](https://docs.recombee.com/api_clients) | Provider lists .NET among official server-side SDKs. |
| `Recraft` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Reducto` | SDK | - | [Reducto Python SDK](https://github.com/reductoai/reducto-python-sdk) | Stainless-generated official Python SDK. |
| `Reka` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Replicate` | SDK | [#302](https://github.com/tryAGI/AutoSDK/issues/302), [#303](https://github.com/tryAGI/AutoSDK/issues/303), [#304](https://github.com/tryAGI/AutoSDK/issues/304) | [Python client](https://github.com/replicate/replicate-python), [JavaScript client](https://github.com/replicate/replicate-javascript) | Official SDKs. |
| `ResembleAI` | SDK | - | [Resemble client libraries](https://docs.resemble.ai/libraries) | Official Python and Node.js SDKs. |
| `Resend` | .NET | - | [Resend .NET SDK](https://github.com/resend/resend-dotnet) | High-priority .NET comparison target. |
| `RetellAI` | SDK | - | [Python SDK](https://github.com/RetellAI/retell-python-sdk), [TypeScript SDK](https://github.com/RetellAI/retell-typescript-sdk) | Stainless-hosted spec source. |
| `RevAI` | Docs | - | API docs/OpenAPI | No first-party .NET SDK found in this pass. |
| `Reve` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Reverie` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Revocalize` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Rime` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Roboflow` | SDK | - | [Roboflow Python package](https://github.com/roboflow/roboflow-python) | Official Python package. |
| `Runware` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Runway` | SDK | - | [Runway SDK docs](https://docs.dev.runwayml.com/api-details/sdks/) | Official Node.js and Python SDKs. |
| `SarvamAI` | SDK | - | [Sarvam SDK docs](https://docs.sarvam.ai/api-reference-docs/getting-started/sd-ks-libraries) | Official Python and JavaScript libraries. |
| `ScaleAI` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `ScrapeGraphAI` | SDK | - | [ScrapeGraph Python SDK](https://github.com/ScrapeGraphAI/scrapegraph-py) | Official Python SDK. |
| `Serper` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Shotstack` | SDK | - | [Shotstack SDK docs](https://shotstack.io/docs/guide/sdks/) | Official PHP, Node, Python, and Ruby SDKs. |
| `Sightengine` | Docs | - | API docs/OpenAPI | No first-party .NET SDK found in this pass. |
| `SiliconFlow` | Docs | - | API docs/OpenAI-compatible examples | No first-party SDK found in this pass. |
| `Simli` | SDK | - | [Simli docs](https://docs.simli.com/) | Provider documents SDK-based realtime integration paths. |
| `Sloyd` | Docs | - | API docs/OpenAPI | API is marked deprecated in local notes; no first-party SDK found. |
| `SmallestAI` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Sonauto` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Soniox` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Speechify` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Speechmatics` | SDK | - | [Python SDK](https://github.com/speechmatics/speechmatics-python-sdk), [JS SDK](https://github.com/speechmatics/speechmatics-js-sdk) | Official SDKs. |
| `StabilityAI` | Docs | - | [Stability API docs](https://platform.stability.ai/docs/api-reference) | Recheck current SDK story; no maintained first-party .NET SDK found. |
| `StepFun` | Docs | - | API docs/OpenAI-compatible examples | No first-party SDK found in this pass. |
| `Strava` | Docs | - | [Strava API docs](https://strava.github.io/api/) | Strava lists language libraries separately; no first-party SDK found in this pass. |
| `Supabase` | Community | - | [Supabase C# community client](https://github.com/supabase-community/supabase-csharp) | Community-maintained C# client, useful for conventions but not first-party. |
| `Synthesia` | Docs | - | [Synthesia API docs](https://docs.synthesia.io/) | No first-party SDK found in this pass. |
| `Tavily` | SDK | - | [Python SDK](https://github.com/tavily-ai/tavily-python), [JavaScript SDK](https://github.com/tavily-ai/tavily-js) | Official SDKs. |
| `Tavus` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `TencentTokenHub` | .NET | [#298](https://github.com/tryAGI/AutoSDK/issues/298) | [Tencent Cloud .NET SDK](https://github.com/TencentCloud/tencentcloud-sdk-dotnet) | Use where TokenHub behavior maps to Tencent Cloud SDK conventions. |
| `Terra` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `ThreeDAIStudio` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Together` | SDK | - | [Python SDK](https://github.com/togethercomputer/together-python), [TypeScript SDK](https://github.com/togethercomputer/together-typescript) | Official SDKs. |
| `Topaz` | Docs | - | [Topaz API docs](https://developer.topazlabs.com/api-reference) | No first-party SDK found in this pass. |
| `Tripo` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Triverse` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Turbopuffer` | SDK | - | [Python SDK](https://github.com/turbopuffer/turbopuffer-python), [TypeScript SDK](https://github.com/turbopuffer/turbopuffer-typescript) | Official SDKs. |
| `TwelveLabs` | SDK | - | [TwelveLabs SDK docs](https://beta.docs.twelvelabs.io/docs/resources/twelve-labs-sd-ks) | Official Python and Node.js SDKs. |
| `Ultravox` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Upstage` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `V0` | SDK | - | [Vercel AI SDK](https://github.com/vercel/ai) | Compare only where V0 API behavior maps to Vercel AI SDK patterns. |
| `Vapi` | .NET | - | [Vapi server SDK docs](https://docs.vapi.ai/server-sdks) | Official C# server SDK documented alongside other languages. |
| `Vectara` | SDK | - | [Vectara Python SDK docs](https://docs.vectara.com/docs/sdk/vectara-python-sdk) | Python SDK is the official comparison target. |
| `Vellum` | SDK | - | [Vellum SDK repos](https://github.com/vellum-ai) | Official Python, Node, Go, and Ruby SDKs. |
| `Vercel` | SDK | - | [Vercel SDK](https://github.com/vercel/sdk) | Official TypeScript SDK. |
| `Vidu` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `VoiceAI` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Voicebox` | Docs | - | Upstream FastAPI app/API | No separate first-party SDK found. |
| `VoyageAI` | SDK | - | [Python SDK](https://github.com/voyage-ai/voyageai-python), [TypeScript SDK](https://github.com/voyage-ai/typescript-sdk) | Official Python and TypeScript SDKs. |
| `WaveSpeedAI` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Weave` | SDK | [#305](https://github.com/tryAGI/AutoSDK/issues/305), [#307](https://github.com/tryAGI/AutoSDK/issues/307), [#308](https://github.com/tryAGI/AutoSDK/issues/308) | [W&B Weave](https://github.com/wandb/weave) | Official Python observability SDK with batching/durable queues, prompt helpers, evaluations, and scorers. |
| `Weaviate` | .NET | - | [Weaviate C# client](https://github.com/weaviate/csharp-client) | High-priority .NET comparison target. |
| `Whoop` | Docs | - | [WHOOP API docs](https://developer.whoop.com/api/) | No first-party SDK found in this pass. |
| `Withings` | SDK | - | [Withings Mobile SDK](https://developer.withings.com/sdk/) | Mobile device setup SDK, not a .NET Data API client. |
| `WorldLabs` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Writer` | SDK | - | [Writer Python SDK](https://github.com/writer/writer-python) | Stainless-generated official Python SDK. |
| `Writesonic` | Docs | - | API docs/OpenAPI | No first-party SDK found in this pass. |
| `Xai` | Docs | - | API docs/OpenAI-compatible examples | No first-party SDK found in this pass. |
| `ZAI` | Docs | - | API docs/OpenAI-compatible examples | No first-party SDK found in this pass. |
| `Zep` | SDK | - | [Zep SDK docs](https://help.getzep.com/v2/quickstart) | Official Python, TypeScript, and Go SDKs. |
| `Zoo` | SDK | - | [Zoo/KittyCAD Python](https://github.com/KittyCAD/kittycad.py), [TypeScript](https://github.com/KittyCAD/kittycad.ts), [Rust](https://github.com/KittyCAD/kittycad.rs) | Official generated clients for the Zoo design API. |
