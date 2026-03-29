# SDK Catalog

**120+ SDKs** for AI/ML services, all auto-generated from OpenAPI specs via [AutoSDK](https://github.com/HavenDV/AutoSDK). Each SDK targets `net10.0`, supports AOT/trimming, and is published to NuGet.

## LLM / Text Generation

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Anthropic | Chat completions, streaming, tool calling, vision, thinking | [tryAGI.Anthropic](https://www.nuget.org/packages/tryAGI.Anthropic) | [GitHub](https://github.com/tryAGI/Anthropic) | [Docs](https://tryagi.github.io/Anthropic/) | `IChatClient` |
| OpenAI | Chat, embeddings, images, audio, custom providers | [tryAGI.OpenAI](https://www.nuget.org/packages/tryAGI.OpenAI) | [GitHub](https://github.com/tryAGI/OpenAI) | [Docs](https://tryagi.github.io/OpenAI/) | `IChatClient` `IEmbeddingGenerator` |
| Ollama | Local LLM inference, chat, embeddings | [tryAGI.Ollama](https://www.nuget.org/packages/tryAGI.Ollama) | [GitHub](https://github.com/tryAGI/Ollama) | [Docs](https://tryagi.github.io/Ollama/) | `IChatClient` `IEmbeddingGenerator` |
| Google.Gemini | Generative AI, chat, embeddings, thinking | [tryAGI.Google.Gemini](https://www.nuget.org/packages/tryAGI.Google.Gemini) | [GitHub](https://github.com/tryAGI/Google_Generative_AI) | [Docs](https://tryagi.github.io/Google_Generative_AI/) | `IChatClient` `IEmbeddingGenerator` |
| Mistral | Chat completions, streaming, tool calling, vision | [tryAGI.Mistral](https://www.nuget.org/packages/tryAGI.Mistral) | [GitHub](https://github.com/tryAGI/Mistral) | [Docs](https://tryagi.github.io/Mistral/) | `IChatClient` |
| Cohere | Chat, embeddings, reranking, RAG | [tryAGI.Cohere](https://www.nuget.org/packages/tryAGI.Cohere) | [GitHub](https://github.com/tryAGI/Cohere) | [Docs](https://tryagi.github.io/Cohere/) | `IChatClient` `IEmbeddingGenerator` |
| Together | Cloud inference, chat, embeddings, reasoning | [tryAGI.Together](https://www.nuget.org/packages/tryAGI.Together) | [GitHub](https://github.com/tryAGI/Together) | [Docs](https://tryagi.github.io/Together/) | `IChatClient` `IEmbeddingGenerator` |
| AI21 | Chat completions, streaming, tool calling, reasoning | [tryAGI.AI21](https://www.nuget.org/packages/tryAGI.AI21) | [GitHub](https://github.com/tryAGI/AI21) | [Docs](https://tryagi.github.io/AI21/) | `IChatClient` |
| Reka | Chat, vision, audio/video/PDF, speech-to-text | [tryAGI.Reka](https://www.nuget.org/packages/tryAGI.Reka) | [GitHub](https://github.com/tryAGI/Reka) | [Docs](https://tryagi.github.io/Reka/) | `IChatClient` `ISpeechToTextClient` |
| HuggingFace | Serverless inference, chat, embeddings | [tryAGI.HuggingFace](https://www.nuget.org/packages/tryAGI.HuggingFace) | [GitHub](https://github.com/tryAGI/HuggingFace) | [Docs](https://tryagi.github.io/HuggingFace/) | `IChatClient` `IEmbeddingGenerator` |
| Writer | Enterprise AI: chat, knowledge graphs, vision, translation | [tryAGI.Writer](https://www.nuget.org/packages/tryAGI.Writer) | [GitHub](https://github.com/tryAGI/Writer) | [Docs](https://tryagi.github.io/Writer/) | `IChatClient` |
| Upstage | Solar LLM, embeddings, Document AI, translation | [tryAGI.Upstage](https://www.nuget.org/packages/tryAGI.Upstage) | [GitHub](https://github.com/tryAGI/Upstage) | [Docs](https://tryagi.github.io/Upstage/) | `IChatClient` `IEmbeddingGenerator` `AIFunction` tools |
| SarvamAI | Indian language AI: chat, STT, TTS, translation | [tryAGI.SarvamAI](https://www.nuget.org/packages/tryAGI.SarvamAI) | [GitHub](https://github.com/tryAGI/SarvamAI) | [Docs](https://tryagi.github.io/SarvamAI/) | `IChatClient` `ISpeechToTextClient` `AIFunction` tools |
| PredictionGuard | LLMs with safety guardrails, factuality, PII detection | [tryAGI.PredictionGuard](https://www.nuget.org/packages/tryAGI.PredictionGuard) | [GitHub](https://github.com/tryAGI/PredictionGuard) | [Docs](https://tryagi.github.io/PredictionGuard/) | `AIFunction` tools |
| Writesonic | AI content generation, ChatSonic, image generation | [tryAGI.Writesonic](https://www.nuget.org/packages/tryAGI.Writesonic) | [GitHub](https://github.com/tryAGI/Writesonic) | [Docs](https://tryagi.github.io/Writesonic/) | `AIFunction` tools |
| JasperAI | AI marketing content, brand voices, knowledge | [tryAGI.JasperAI](https://www.nuget.org/packages/tryAGI.JasperAI) | [GitHub](https://github.com/tryAGI/JasperAI) | [Docs](https://tryagi.github.io/JasperAI/) | `AIFunction` tools |
| Xai | Grok models: images, video, realtime voice | [tryAGI.Xai](https://www.nuget.org/packages/tryAGI.Xai) | [GitHub](https://github.com/tryAGI/Xai) | [Docs](https://tryagi.github.io/Xai/) | via CustomProviders |
| Groq | Fast LPU inference for open-source models | [tryAGI.Groq](https://www.nuget.org/packages/tryAGI.Groq) | [GitHub](https://github.com/tryAGI/Groq) | [Docs](https://tryagi.github.io/Groq/) | via CustomProviders |
| DeepInfra | Serverless AI inference, detection, classification | [tryAGI.DeepInfra](https://www.nuget.org/packages/tryAGI.DeepInfra) | [GitHub](https://github.com/tryAGI/DeepInfra) | [Docs](https://tryagi.github.io/DeepInfra/) | via CustomProviders |
| SiliconFlow | Unified AI cloud: text, image, audio, video models | [tryAGI.SiliconFlow](https://www.nuget.org/packages/tryAGI.SiliconFlow) | [GitHub](https://github.com/tryAGI/SiliconFlow) | [Docs](https://tryagi.github.io/SiliconFlow/) | `AIFunction` tools |

## Image Generation

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Ideogram | AI image generation from text prompts | [tryAGI.Ideogram](https://www.nuget.org/packages/tryAGI.Ideogram) | [GitHub](https://github.com/tryAGI/Ideogram) | [Docs](https://tryagi.github.io/Ideogram/) | - |
| Leonardo | AI image generation and editing | [tryAGI.Leonardo](https://www.nuget.org/packages/tryAGI.Leonardo) | [GitHub](https://github.com/tryAGI/Leonardo) | [Docs](https://tryagi.github.io/Leonardo/) | - |
| Recraft | AI image generation and style transfer | [tryAGI.Recraft](https://www.nuget.org/packages/tryAGI.Recraft) | [GitHub](https://github.com/tryAGI/Recraft) | [Docs](https://tryagi.github.io/Recraft/) | - |
| Replicate | AI model hosting and inference platform | [tryAGI.Replicate](https://www.nuget.org/packages/tryAGI.Replicate) | [GitHub](https://github.com/tryAGI/Replicate) | [Docs](https://tryagi.github.io/Replicate/) | - |
| StabilityAI | Text-to-image, image-to-image, upscaling | [tryAGI.StabilityAI](https://www.nuget.org/packages/tryAGI.StabilityAI) | [GitHub](https://github.com/tryAGI/StabilityAI) | [Docs](https://tryagi.github.io/StabilityAI/) | - |
| BlackForestLabs | FLUX image models: Pro, Dev, Ultra, Kontext | [BlackForestLabs](https://www.nuget.org/packages/BlackForestLabs) | [GitHub](https://github.com/tryAGI/BlackForestLabs) | [Docs](https://tryagi.github.io/BlackForestLabs/) | - |
| Photoroom | Background removal, AI backgrounds, relighting | [tryAGI.Photoroom](https://www.nuget.org/packages/tryAGI.Photoroom) | [GitHub](https://github.com/tryAGI/Photoroom) | [Docs](https://tryagi.github.io/Photoroom/) | `AIFunction` tools |
| Picsart | AI image/video editing, background removal, GenAI | [tryAGI.Picsart](https://www.nuget.org/packages/tryAGI.Picsart) | [GitHub](https://github.com/tryAGI/Picsart) | [Docs](https://tryagi.github.io/Picsart/) | `AIFunction` tools |

## Video Generation

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| HeyGen | AI avatar video generation | [tryAGI.HeyGen](https://www.nuget.org/packages/tryAGI.HeyGen) | [GitHub](https://github.com/tryAGI/HeyGen) | [Docs](https://tryagi.github.io/HeyGen/) | - |
| Hedra | AI character video generation | [tryAGI.Hedra](https://www.nuget.org/packages/tryAGI.Hedra) | [GitHub](https://github.com/tryAGI/Hedra) | [Docs](https://tryagi.github.io/Hedra/) | - |
| Luma | Dream Machine video and image generation | [tryAGI.Luma](https://www.nuget.org/packages/tryAGI.Luma) | [GitHub](https://github.com/tryAGI/Luma) | [Docs](https://tryagi.github.io/Luma/) | - |
| Runway | Image/text-to-video, TTS, sound effects, dubbing | [tryAGI.Runway](https://www.nuget.org/packages/tryAGI.Runway) | [GitHub](https://github.com/tryAGI/Runway) | [Docs](https://tryagi.github.io/Runway/) | - |
| KlingAI | Text/image-to-video, lip sync, effects, avatars | [tryAGI.KlingAI](https://www.nuget.org/packages/tryAGI.KlingAI) | [GitHub](https://github.com/tryAGI/KlingAI) | [Docs](https://tryagi.github.io/KlingAI/) | `AIFunction` tools |
| DId | Talking avatar videos, AI agents, streaming | [tryAGI.DId](https://www.nuget.org/packages/tryAGI.DId) | [GitHub](https://github.com/tryAGI/DId) | [Docs](https://tryagi.github.io/DId/) | `AIFunction` tools |
| Synthesia | Enterprise AI video with speaking avatars | [tryAGI.Synthesia](https://www.nuget.org/packages/tryAGI.Synthesia) | [GitHub](https://github.com/tryAGI/Synthesia) | [Docs](https://tryagi.github.io/Synthesia/) | `AIFunction` tools |
| Tavus | Conversational video AI with replicas and personas | [tryAGI.Tavus](https://www.nuget.org/packages/tryAGI.Tavus) | [GitHub](https://github.com/tryAGI/Tavus) | [Docs](https://tryagi.github.io/Tavus/) | `AIFunction` tools |
| Shotstack | Programmatic video, image, and audio editing | [tryAGI.Shotstack](https://www.nuget.org/packages/tryAGI.Shotstack) | [GitHub](https://github.com/tryAGI/Shotstack) | [Docs](https://tryagi.github.io/Shotstack/) | `AIFunction` tools |
| Descript | AI video/audio editing, import, export | [tryAGI.Descript](https://www.nuget.org/packages/tryAGI.Descript) | [GitHub](https://github.com/tryAGI/Descript) | [Docs](https://tryagi.github.io/Descript/) | - |
| Creatomate | Programmatic video/image rendering with templates | [tryAGI.Creatomate](https://www.nuget.org/packages/tryAGI.Creatomate) | [GitHub](https://github.com/tryAGI/Creatomate) | [Docs](https://tryagi.github.io/Creatomate/) | `AIFunction` tools |
| MagicHour | AI video: face swap, lip sync, text/image-to-video | [tryAGI.MagicHour](https://www.nuget.org/packages/tryAGI.MagicHour) | [GitHub](https://github.com/tryAGI/MagicHour) | [Docs](https://tryagi.github.io/MagicHour/) | `AIFunction` tools |

## 3D Generation

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Tripo | AI 3D model generation from text and images | [tryAGI.Tripo](https://www.nuget.org/packages/tryAGI.Tripo) | [GitHub](https://github.com/tryAGI/Tripo) | [Docs](https://tryagi.github.io/Tripo/) | - |
| Meshy | Text/image-to-3D, rigging, animation, retexture | [Meshy](https://www.nuget.org/packages/Meshy) | [GitHub](https://github.com/tryAGI/Meshy) | [Docs](https://tryagi.github.io/Meshy/) | - |
| Meshcapade | 3D avatar creation, motion capture, scenes | [Meshcapade](https://www.nuget.org/packages/Meshcapade) | [GitHub](https://github.com/tryAGI/Meshcapade) | [Docs](https://tryagi.github.io/Meshcapade/) | - |

## Generative Media Inference

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Fal | Platform API for generative media models | [tryAGI.Fal](https://www.nuget.org/packages/tryAGI.Fal) | [GitHub](https://github.com/tryAGI/Fal) | [Docs](https://tryagi.github.io/Fal/) | - |
| WaveSpeedAI | 700+ AI models for image, video, and audio | [tryAGI.WaveSpeedAI](https://www.nuget.org/packages/tryAGI.WaveSpeedAI) | [GitHub](https://github.com/tryAGI/WaveSpeedAI) | [Docs](https://tryagi.github.io/WaveSpeedAI/) | `AIFunction` tools |

## Audio / Speech

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| ElevenLabs | Text-to-speech, speech-to-text, voice cloning | [tryAGI.ElevenLabs](https://www.nuget.org/packages/tryAGI.ElevenLabs) | [GitHub](https://github.com/tryAGI/ElevenLabs) | [Docs](https://tryagi.github.io/ElevenLabs/) | `ISpeechToTextClient` |
| AssemblyAI | Speech-to-text, audio intelligence, real-time | [tryAGI.AssemblyAI](https://www.nuget.org/packages/tryAGI.AssemblyAI) | [GitHub](https://github.com/tryAGI/AssemblyAI) | [Docs](https://tryagi.github.io/AssemblyAI/) | `ISpeechToTextClient` |
| Deepgram | Speech-to-text, text-to-speech, voice agents | [tryAGI.Deepgram](https://www.nuget.org/packages/tryAGI.Deepgram) | [GitHub](https://github.com/tryAGI/Deepgram) | [Docs](https://tryagi.github.io/Deepgram/) | `ISpeechToTextClient` |
| Gladia | Transcription for 100+ languages, live and batch | [Gladia](https://www.nuget.org/packages/Gladia) | [GitHub](https://github.com/tryAGI/Gladia) | [Docs](https://tryagi.github.io/Gladia/) | `ISpeechToTextClient` |
| Cartesia | Low-latency TTS, STT, voice cloning, AI agents | [Cartesia](https://www.nuget.org/packages/Cartesia) | [GitHub](https://github.com/tryAGI/Cartesia) | [Docs](https://tryagi.github.io/Cartesia/) | `ISpeechToTextClient` |
| FishAudio | TTS, speech recognition, voice cloning, 50+ languages | [tryAGI.FishAudio](https://www.nuget.org/packages/tryAGI.FishAudio) | [GitHub](https://github.com/tryAGI/FishAudio) | [Docs](https://tryagi.github.io/FishAudio/) | `ISpeechToTextClient` `AIFunction` tools |
| Murf | Enterprise TTS, 150+ voices, 35 languages | [tryAGI.Murf](https://www.nuget.org/packages/tryAGI.Murf) | [GitHub](https://github.com/tryAGI/Murf) | [Docs](https://tryagi.github.io/Murf/) | `AIFunction` tools |
| RevAI | Speech-to-text, sentiment analysis, topic extraction | [tryAGI.RevAI](https://www.nuget.org/packages/tryAGI.RevAI) | [GitHub](https://github.com/tryAGI/RevAI) | [Docs](https://tryagi.github.io/RevAI/) | `ISpeechToTextClient` `AIFunction` tools |
| Speechmatics | Batch STT, 55+ languages, diarization, translation | [tryAGI.Speechmatics](https://www.nuget.org/packages/tryAGI.Speechmatics) | [GitHub](https://github.com/tryAGI/Speechmatics) | [Docs](https://tryagi.github.io/Speechmatics/) | `ISpeechToTextClient` `AIFunction` tools |
| Ultravox | Voice AI conversation platform | [Ultravox](https://www.nuget.org/packages/Ultravox) | [GitHub](https://github.com/tryAGI/Ultravox) | [Docs](https://tryagi.github.io/Ultravox/) | - |
| LalalAI | Audio stem separation, voice cleaning, noise removal | [tryAGI.LalalAI](https://www.nuget.org/packages/tryAGI.LalalAI) | [GitHub](https://github.com/tryAGI/LalalAI) | [Docs](https://tryagi.github.io/LalalAI/) | `AIFunction` tools |
| Loudly | AI music generation, royalty-free tracks | [tryAGI.Loudly](https://www.nuget.org/packages/tryAGI.Loudly) | [GitHub](https://github.com/tryAGI/Loudly) | [Docs](https://tryagi.github.io/Loudly/) | `AIFunction` tools |

## Voice AI

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| RetellAI | Voice AI agents for phone calls, analytics | [tryAGI.RetellAI](https://www.nuget.org/packages/tryAGI.RetellAI) | [GitHub](https://github.com/tryAGI/RetellAI) | [Docs](https://tryagi.github.io/RetellAI/) | `AIFunction` tools |
| Vapi | Voice AI assistants for phone and web calls | [tryAGI.Vapi](https://www.nuget.org/packages/tryAGI.Vapi) | [GitHub](https://github.com/tryAGI/Vapi) | [Docs](https://tryagi.github.io/Vapi/) | `AIFunction` tools |
| BlandAI | AI-powered phone calls, campaigns, pathways | [tryAGI.BlandAI](https://www.nuget.org/packages/tryAGI.BlandAI) | [GitHub](https://github.com/tryAGI/BlandAI) | [Docs](https://tryagi.github.io/BlandAI/) | - |
| HammingAI | Voice agent testing, evaluation, monitoring | [tryAGI.HammingAI](https://www.nuget.org/packages/tryAGI.HammingAI) | [GitHub](https://github.com/tryAGI/HammingAI) | [Docs](https://tryagi.github.io/HammingAI/) | `AIFunction` tools |

## Translation / NLP

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| DeepL | Translation, rephrasing, document translation, glossaries | [DeepL](https://www.nuget.org/packages/DeepL) | [GitHub](https://github.com/tryAGI/DeepL) | [Docs](https://tryagi.github.io/DeepL/) | `AIFunction` tools |
| ModernMT | Adaptive machine translation, 200+ languages | [tryAGI.ModernMT](https://www.nuget.org/packages/tryAGI.ModernMT) | [GitHub](https://github.com/tryAGI/ModernMT) | [Docs](https://tryagi.github.io/ModernMT/) | `AIFunction` tools |

Also see [SarvamAI](#llm--text-generation) (22+ Indian languages: translation, transliteration, STT via `AIFunction` tools).

## Search / RAG / Embeddings

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Exa | AI-powered web search, contents, answers | [Exa](https://www.nuget.org/packages/Exa) | [GitHub](https://github.com/tryAGI/Exa) | [Docs](https://tryagi.github.io/Exa/) | `AIFunction` tools |
| Serper | Google search results: web, news, images, scholar | [Serper](https://www.nuget.org/packages/Serper) | [GitHub](https://github.com/tryAGI/Serper) | [Docs](https://tryagi.github.io/Serper/) | `AIFunction` tools |
| BraveSearch | Privacy-focused web, image, video, news search | [tryAGI.BraveSearch](https://www.nuget.org/packages/tryAGI.BraveSearch) | [GitHub](https://github.com/tryAGI/BraveSearch) | [Docs](https://tryagi.github.io/BraveSearch/) | `AIFunction` tools |
| GroundX | RAG infrastructure: document ingestion and search | [tryAGI.GroundX](https://www.nuget.org/packages/tryAGI.GroundX) | [GitHub](https://github.com/tryAGI/GroundX) | [Docs](https://tryagi.github.io/GroundX/) | `AIFunction` tools |
| Algolia | AI search, recommendations, and analytics | [tryAGI.Algolia](https://www.nuget.org/packages/tryAGI.Algolia) | [GitHub](https://github.com/tryAGI/Algolia) | [Docs](https://tryagi.github.io/Algolia/) | `AIFunction` tools |
| ScrapeGraphAI | AI web scraping with natural language prompts | [tryAGI.ScrapeGraphAI](https://www.nuget.org/packages/tryAGI.ScrapeGraphAI) | [GitHub](https://github.com/tryAGI/ScrapeGraphAI) | [Docs](https://tryagi.github.io/ScrapeGraphAI/) | `AIFunction` tools |
| Greptile | AI codebase intelligence and code search | [tryAGI.Greptile](https://www.nuget.org/packages/tryAGI.Greptile) | [GitHub](https://github.com/tryAGI/Greptile) | [Docs](https://tryagi.github.io/Greptile/) | `AIFunction` tools |
| Jina | Embeddings, reranking, classification, search | [tryAGI.Jina](https://www.nuget.org/packages/tryAGI.Jina) | [GitHub](https://github.com/tryAGI/Jina) | [Docs](https://tryagi.github.io/Jina/) | `IEmbeddingGenerator` |
| VoyageAI | Text embeddings and reranking | [tryAGI.VoyageAI](https://www.nuget.org/packages/tryAGI.VoyageAI) | [GitHub](https://github.com/tryAGI/VoyageAI) | [Docs](https://tryagi.github.io/VoyageAI/) | `IEmbeddingGenerator` |
| Nomic | Text and image embeddings, Atlas visualization | [tryAGI.Nomic](https://www.nuget.org/packages/tryAGI.Nomic) | [GitHub](https://github.com/tryAGI/Nomic) | [Docs](https://tryagi.github.io/Nomic/) | `AIFunction` tools |
| TwelveLabs | Video understanding: search, embed, generate | [TwelveLabs](https://www.nuget.org/packages/TwelveLabs) | [GitHub](https://github.com/tryAGI/TwelveLabs) | [Docs](https://tryagi.github.io/TwelveLabs/) | `IEmbeddingGenerator` |
| Mixedbread | Embeddings, reranking, vector stores, document parsing | [Mixedbread](https://www.nuget.org/packages/Mixedbread) | [GitHub](https://github.com/tryAGI/Mixedbread) | [Docs](https://tryagi.github.io/Mixedbread/) | `IEmbeddingGenerator` |
| Tavily | AI-optimized web search and content extraction | [tryAGI.Tavily](https://www.nuget.org/packages/tryAGI.Tavily) | [GitHub](https://github.com/tryAGI/Tavily) | [Docs](https://tryagi.github.io/Tavily/) | `AIFunction` tools |
| Vectara | RAG-as-a-Service platform | [tryAGI.Vectara](https://www.nuget.org/packages/tryAGI.Vectara) | [GitHub](https://github.com/tryAGI/Vectara) | [Docs](https://tryagi.github.io/Vectara/) | - |

## Vector Databases

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Pinecone | Vector database with similarity search and inference | [tryAGI.Pinecone](https://www.nuget.org/packages/tryAGI.Pinecone) | [GitHub](https://github.com/tryAGI/Pinecone) | [Docs](https://tryagi.github.io/Pinecone/) | `AIFunction` tools |
| Chroma | Open-source AI-native embedding database | [tryAGI.Chroma](https://www.nuget.org/packages/tryAGI.Chroma) | [GitHub](https://github.com/tryAGI/Chroma) | [Docs](https://tryagi.github.io/Chroma/) | - |
| Weaviate | Open-source vector database for AI apps | [tryAGI.Weaviate](https://www.nuget.org/packages/tryAGI.Weaviate) | [GitHub](https://github.com/tryAGI/Weaviate) | [Docs](https://tryagi.github.io/Weaviate/) | - |
| Qdrant | Vector search engine with filtering and clustering | [tryAGI.Qdrant](https://www.nuget.org/packages/tryAGI.Qdrant) | [GitHub](https://github.com/tryAGI/Qdrant) | [Docs](https://tryagi.github.io/Qdrant/) | - |
| Milvus | Open-source vector database for similarity search | [tryAGI.Milvus](https://www.nuget.org/packages/tryAGI.Milvus) | [GitHub](https://github.com/tryAGI/Milvus) | [Docs](https://tryagi.github.io/Milvus/) | `AIFunction` tools |
| Turbopuffer | High-performance serverless vector database | [tryAGI.Turbopuffer](https://www.nuget.org/packages/tryAGI.Turbopuffer) | [GitHub](https://github.com/tryAGI/Turbopuffer) | [Docs](https://tryagi.github.io/Turbopuffer/) | - |

## Document Processing

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| LlamaParse | Document parsing, extraction, pipelines, retrieval | [tryAGI.LlamaParse](https://www.nuget.org/packages/tryAGI.LlamaParse) | [GitHub](https://github.com/tryAGI/LlamaParse) | [Docs](https://tryagi.github.io/LlamaParse/) | `AIFunction` tools |
| Nanonets | Intelligent document processing, OCR, 110+ languages | [tryAGI.Nanonets](https://www.nuget.org/packages/tryAGI.Nanonets) | [GitHub](https://github.com/tryAGI/Nanonets) | [Docs](https://tryagi.github.io/Nanonets/) | `AIFunction` tools |
| Reducto | AI document parsing, extraction, classification | [tryAGI.Reducto](https://www.nuget.org/packages/tryAGI.Reducto) | [GitHub](https://github.com/tryAGI/Reducto) | [Docs](https://tryagi.github.io/Reducto/) | `AIFunction` tools |
| DoclingServe | Self-hosted document conversion and chunking | [tryAGI.DoclingServe](https://www.nuget.org/packages/tryAGI.DoclingServe) | [GitHub](https://github.com/tryAGI/DoclingServe) | [Docs](https://tryagi.github.io/DoclingServe/) | - |

## Observability / Evaluation

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Phoenix | LLM observability: traces, spans, evaluations | [tryAGI.Phoenix](https://www.nuget.org/packages/tryAGI.Phoenix) | [GitHub](https://github.com/tryAGI/Phoenix) | [Docs](https://tryagi.github.io/Phoenix/) | `AIFunction` tools |
| Langfuse | Open-source LLM observability and prompt management | [Langfuse](https://www.nuget.org/packages/Langfuse) | [GitHub](https://github.com/tryAGI/Langfuse) | [Docs](https://tryagi.github.io/Langfuse/) | - |
| Helicone | LLM monitoring: requests, metrics, dashboards | [tryAGI.Helicone](https://www.nuget.org/packages/tryAGI.Helicone) | [GitHub](https://github.com/tryAGI/Helicone) | [Docs](https://tryagi.github.io/Helicone/) | `AIFunction` tools |
| Opik | LLM observability, evaluation, experimentation | [tryAGI.Opik](https://www.nuget.org/packages/tryAGI.Opik) | [GitHub](https://github.com/tryAGI/Opik) | [Docs](https://tryagi.github.io/Opik/) | `AIFunction` tools |
| Weave | W&B LLM observability: tracing, evaluations | [tryAGI.Weave](https://www.nuget.org/packages/tryAGI.Weave) | [GitHub](https://github.com/tryAGI/Weave) | [Docs](https://tryagi.github.io/Weave/) | `AIFunction` tools |
| ScaleAI | Data labeling, RLHF, and AI evaluation | [tryAGI.ScaleAI](https://www.nuget.org/packages/tryAGI.ScaleAI) | [GitHub](https://github.com/tryAGI/ScaleAI) | [Docs](https://tryagi.github.io/ScaleAI/) | `AIFunction` tools |

## AI Gateway / Routing

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| OpenRouter | LLM gateway with 500+ models, routing, credits | [tryAGI.OpenRouter](https://www.nuget.org/packages/tryAGI.OpenRouter) | [GitHub](https://github.com/tryAGI/OpenRouter) | [Docs](https://tryagi.github.io/OpenRouter/) | `AIFunction` tools |
| Portkey | AI gateway: 250+ LLMs, guardrails, caching, routing | [tryAGI.Portkey](https://www.nuget.org/packages/tryAGI.Portkey) | [GitHub](https://github.com/tryAGI/Portkey) | [Docs](https://tryagi.github.io/Portkey/) | - |
| EdenAI | Unified AI gateway: 500+ models, multi-provider | [tryAGI.EdenAI](https://www.nuget.org/packages/tryAGI.EdenAI) | [GitHub](https://github.com/tryAGI/EdenAI) | [Docs](https://tryagi.github.io/EdenAI/) | `AIFunction` tools |
| Martian | Intelligent LLM router, cost/quality optimization | [tryAGI.Martian](https://www.nuget.org/packages/tryAGI.Martian) | [GitHub](https://github.com/tryAGI/Martian) | [Docs](https://tryagi.github.io/Martian/) | `AIFunction` tools |
| Baseten | Model serving and deployment platform | [tryAGI.Baseten](https://www.nuget.org/packages/tryAGI.Baseten) | [GitHub](https://github.com/tryAGI/Baseten) | [Docs](https://tryagi.github.io/Baseten/) | `AIFunction` tools |
| Predibase | LoRA fine-tuning and serverless LLM inference | [tryAGI.Predibase](https://www.nuget.org/packages/tryAGI.Predibase) | [GitHub](https://github.com/tryAGI/Predibase) | [Docs](https://tryagi.github.io/Predibase/) | `AIFunction` tools |

## AI Security / Guardrails

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Guardrails | LLM validation: hallucination, PII, prompt injection | [tryAGI.Guardrails](https://www.nuget.org/packages/tryAGI.Guardrails) | [GitHub](https://github.com/tryAGI/Guardrails) | [Docs](https://tryagi.github.io/Guardrails/) | `AIFunction` tools |
| Lakera | Prompt injection, jailbreak, PII detection | [tryAGI.Lakera](https://www.nuget.org/packages/tryAGI.Lakera) | [GitHub](https://github.com/tryAGI/Lakera) | [Docs](https://tryagi.github.io/Lakera/) | `AIFunction` tools |
| NightfallAI | Data security: PII, PHI, PCI, secrets detection | [tryAGI.NightfallAI](https://www.nuget.org/packages/tryAGI.NightfallAI) | [GitHub](https://github.com/tryAGI/NightfallAI) | [Docs](https://tryagi.github.io/NightfallAI/) | `AIFunction` tools |
| ModerationAPI | Multi-modal content moderation, 200+ languages | [tryAGI.ModerationAPI](https://www.nuget.org/packages/tryAGI.ModerationAPI) | [GitHub](https://github.com/tryAGI/ModerationAPI) | [Docs](https://tryagi.github.io/ModerationAPI/) | `AIFunction` tools |
| Sightengine | Visual content moderation, 120+ detection classes | [tryAGI.Sightengine](https://www.nuget.org/packages/tryAGI.Sightengine) | [GitHub](https://github.com/tryAGI/Sightengine) | [Docs](https://tryagi.github.io/Sightengine/) | `AIFunction` tools |

## AI Agent Infrastructure

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| E2B | Secure cloud sandboxes for AI agents | [E2B](https://www.nuget.org/packages/E2B) | [GitHub](https://github.com/tryAGI/E2B) | [Docs](https://tryagi.github.io/E2B/) | - |
| Mem0 | AI memory layer for personalized agents | [Mem0](https://www.nuget.org/packages/Mem0) | [GitHub](https://github.com/tryAGI/Mem0) | [Docs](https://tryagi.github.io/Mem0/) | - |
| CursorAgents | Autonomous AI coding agents on GitHub repos | [tryAGI.CursorAgents](https://www.nuget.org/packages/tryAGI.CursorAgents) | [GitHub](https://github.com/tryAGI/CursorAgents) | [Docs](https://tryagi.github.io/CursorAgents/) | `AIFunction` tools |
| Letta | Stateful AI agents with persistent memory | [tryAGI.Letta](https://www.nuget.org/packages/tryAGI.Letta) | [GitHub](https://github.com/tryAGI/Letta) | [Docs](https://tryagi.github.io/Letta/) | - |
| Browserbase | Cloud browser infrastructure for AI agents | [tryAGI.Browserbase](https://www.nuget.org/packages/tryAGI.Browserbase) | [GitHub](https://github.com/tryAGI/Browserbase) | [Docs](https://tryagi.github.io/Browserbase/) | `AIFunction` tools |
| Julep | Stateful AI agent workflows with persistent memory | [tryAGI.Julep](https://www.nuget.org/packages/tryAGI.Julep) | [GitHub](https://github.com/tryAGI/Julep) | [Docs](https://tryagi.github.io/Julep/) | `AIFunction` tools |
| Dust | AI agent platform with conversations and knowledge | [tryAGI.Dust](https://www.nuget.org/packages/tryAGI.Dust) | [GitHub](https://github.com/tryAGI/Dust) | [Docs](https://tryagi.github.io/Dust/) | `AIFunction` tools |
| Zep | AI agent memory with temporal knowledge graphs | [tryAGI.Zep](https://www.nuget.org/packages/tryAGI.Zep) | [GitHub](https://github.com/tryAGI/Zep) | [Docs](https://tryagi.github.io/Zep/) | `AIFunction` tools |

## Chatbot Platforms

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Botpress | AI chatbot/agent: admin, chat, files, runtime | [tryAGI.Botpress](https://www.nuget.org/packages/tryAGI.Botpress) | [GitHub](https://github.com/tryAGI/Botpress) | [Docs](https://tryagi.github.io/Botpress/) | `AIFunction` tools |

## Prompt Management

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Humanloop | Prompt management, versioning, evaluations | [tryAGI.Humanloop](https://www.nuget.org/packages/tryAGI.Humanloop) | [GitHub](https://github.com/tryAGI/Humanloop) | [Docs](https://tryagi.github.io/Humanloop/) | `AIFunction` tools |
| PromptLayer | Prompt versioning, A/B testing, request tracking | [tryAGI.PromptLayer](https://www.nuget.org/packages/tryAGI.PromptLayer) | [GitHub](https://github.com/tryAGI/PromptLayer) | [Docs](https://tryagi.github.io/PromptLayer/) | `AIFunction` tools |
| Braintrust | AI evaluation, experiments, datasets, scoring | [tryAGI.Braintrust](https://www.nuget.org/packages/tryAGI.Braintrust) | [GitHub](https://github.com/tryAGI/Braintrust) | [Docs](https://tryagi.github.io/Braintrust/) | `AIFunction` tools |
| Vellum | Prompt engineering, evaluation, deployment | [tryAGI.Vellum](https://www.nuget.org/packages/tryAGI.Vellum) | [GitHub](https://github.com/tryAGI/Vellum) | [Docs](https://tryagi.github.io/Vellum/) | - |

## Data Labeling / Annotation

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| LabelStudio | Open-source data labeling and annotation platform | [tryAGI.LabelStudio](https://www.nuget.org/packages/tryAGI.LabelStudio) | [GitHub](https://github.com/tryAGI/LabelStudio) | [Docs](https://tryagi.github.io/LabelStudio/) | `AIFunction` tools |
| CVAT | Computer vision annotation for images and videos | [tryAGI.CVAT](https://www.nuget.org/packages/tryAGI.CVAT) | [GitHub](https://github.com/tryAGI/CVAT) | [Docs](https://tryagi.github.io/CVAT/) | `AIFunction` tools |
| Dataloop | Enterprise AI data management and ML pipelines | [tryAGI.Dataloop](https://www.nuget.org/packages/tryAGI.Dataloop) | [GitHub](https://github.com/tryAGI/Dataloop) | [Docs](https://tryagi.github.io/Dataloop/) | `AIFunction` tools |

## Emotion AI

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| HumeAI | Emotion recognition, empathic voice, expressive TTS | [tryAGI.HumeAI](https://www.nuget.org/packages/tryAGI.HumeAI) | [GitHub](https://github.com/tryAGI/HumeAI) | [Docs](https://tryagi.github.io/HumeAI/) | `AIFunction` tools |

## Time Series AI

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Nixtla | Time series forecasting, anomaly detection | [tryAGI.Nixtla](https://www.nuget.org/packages/tryAGI.Nixtla) | [GitHub](https://github.com/tryAGI/Nixtla) | [Docs](https://tryagi.github.io/Nixtla/) | `AIFunction` tools |

## Computer Vision

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Roboflow | Object detection, segmentation, classification, OCR | [Roboflow](https://www.nuget.org/packages/Roboflow) | [GitHub](https://github.com/tryAGI/Roboflow) | [Docs](https://tryagi.github.io/Roboflow/) | - |

## Recommendation

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Recombee | AI-powered real-time recommendations | [tryAGI.Recombee](https://www.nuget.org/packages/tryAGI.Recombee) | [GitHub](https://github.com/tryAGI/Recombee) | [Docs](https://tryagi.github.io/Recombee/) | `AIFunction` tools |

## Synthetic Data

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Gretel | Privacy-preserving synthetic data generation | [tryAGI.Gretel](https://www.nuget.org/packages/tryAGI.Gretel) | [GitHub](https://github.com/tryAGI/Gretel) | [Docs](https://tryagi.github.io/Gretel/) | `AIFunction` tools |

## Notification / Communication

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Novu | Notification infrastructure: email, SMS, push, chat | [tryAGI.Novu](https://www.nuget.org/packages/tryAGI.Novu) | [GitHub](https://github.com/tryAGI/Novu) | [Docs](https://tryagi.github.io/Novu/) | `AIFunction` tools |
| Resend | Developer email API: contacts, domains, broadcasts | [tryAGI.Resend](https://www.nuget.org/packages/tryAGI.Resend) | [GitHub](https://github.com/tryAGI/Resend) | [Docs](https://tryagi.github.io/Resend/) | `AIFunction` tools |

## Web Scraping

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Apify | Web scraping/automation, 4000+ pre-built Actors | [tryAGI.Apify](https://www.nuget.org/packages/tryAGI.Apify) | [GitHub](https://github.com/tryAGI/Apify) | [Docs](https://tryagi.github.io/Apify/) | `AIFunction` tools |

## Platforms / Orchestration

| SDK | Description | NuGet | GitHub | Docs | MEAI |
|-----|-------------|-------|--------|------|------|
| Composio | AI agent integrations: 250+ tools (GitHub, Slack...) | [tryAGI.Composio](https://www.nuget.org/packages/tryAGI.Composio) | [GitHub](https://github.com/tryAGI/Composio) | [Docs](https://tryagi.github.io/Composio/) | `AIFunction` tools |
| Coze | ByteDance AI agent/chatbot platform | [tryAGI.Coze](https://www.nuget.org/packages/tryAGI.Coze) | [GitHub](https://github.com/tryAGI/Coze) | [Docs](https://tryagi.github.io/Coze/) | - |
| Firecrawl | Web scraping, crawling, and extraction API | [tryAGI.Firecrawl](https://www.nuget.org/packages/tryAGI.Firecrawl) | [GitHub](https://github.com/tryAGI/Firecrawl) | [Docs](https://tryagi.github.io/Firecrawl/) | - |
| Flowise | Low-code AI workflow builder | [tryAGI.Flowise](https://www.nuget.org/packages/tryAGI.Flowise) | [GitHub](https://github.com/tryAGI/Flowise) | [Docs](https://tryagi.github.io/Flowise/) | - |
| Forem | Community platform API (powers dev.to) | [tryAGI.Forem](https://www.nuget.org/packages/tryAGI.Forem) | [GitHub](https://github.com/tryAGI/Forem) | [Docs](https://tryagi.github.io/Forem/) | - |
| Instill | AI pipeline platform: VDP, Artifact, Model APIs | [tryAGI.Instill](https://www.nuget.org/packages/tryAGI.Instill) | [GitHub](https://github.com/tryAGI/Instill) | [Docs](https://tryagi.github.io/Instill/) | - |
| LangSmith | LLM observability and evaluation by LangChain | [tryAGI.LangSmith](https://www.nuget.org/packages/tryAGI.LangSmith) | [GitHub](https://github.com/tryAGI/LangSmith) | [Docs](https://tryagi.github.io/LangSmith/) | - |

## LangChain Ecosystem

| Project | Description | NuGet | GitHub |
|---------|-------------|-------|--------|
| LangChain | C# LangChain framework: chat, embeddings, RAG, vector DBs | [LangChain.Core](https://www.nuget.org/packages/LangChain.Core) | [GitHub](https://github.com/tryAGI/LangChain) |
| LangChain.Providers | Provider abstractions for AI service integrations | [LangChain.Providers.Abstractions](https://www.nuget.org/packages/LangChain.Providers.Abstractions) | [GitHub](https://github.com/tryAGI/LangChain.Providers) |
| LangChain.Databases | Database/vector storage abstractions | [LangChain.Databases.Abstractions](https://www.nuget.org/packages/LangChain.Databases.Abstractions) | [GitHub](https://github.com/tryAGI/LangChain.Databases) |

## Core Infrastructure

| Project | Description | NuGet | GitHub |
|---------|-------------|-------|--------|
| AutoSDK | Source generator for .NET SDKs from OpenAPI specs | [AutoSDK](https://www.nuget.org/packages/AutoSDK) | [GitHub](https://github.com/HavenDV/AutoSDK) |
| CSharpToJsonSchema | C# to JSON Schema source generator for tool calling | [CSharpToJsonSchema](https://www.nuget.org/packages/CSharpToJsonSchema) | [GitHub](https://github.com/tryAGI/CSharpToJsonSchema) |
| Tiktoken | .NET port of OpenAI's Tiktoken tokenizer | [Tiktoken](https://www.nuget.org/packages/Tiktoken) | [GitHub](https://github.com/tryAGI/Tiktoken) |
