# ISpeechToTextClient Coverage

There are currently **10** direct `ISpeechToTextClient` implementations in the tryAGI SDKs.

## Capability Matrix

| SDK | File transcription | URL transcription | `GetStreamingTextAsync()` | Translation | Timestamps | Notes |
|-----|:---:|:---:|:---:|:---:|:---:|-------|
| Reka | Y | Y | ~ | Y | Y | Stream or URL input; translation supported |
| ElevenLabs | Y | - | ~ | - | Y | Realtime WebSocket exists outside the current MEAI adapter |
| AssemblyAI | Y | Y* | ~ | - | Y | Upload + poll flow |
| Deepgram | - | Y | Y | - | Y | URL-based batch transcription plus true realtime WebSocket streaming |
| Gladia | Y | Y* | ~ | Y | Y | URL and translation via `RawRepresentationFactory` |
| Cartesia | Y | - | ~ | - | Y | Synchronous STT with word timestamps |
| FishAudio | Y | - | ~ | - | Y | Timestamped ASR plus speech-related tools |
| RevAI | Y | Y | ~ | - | Y | Upload or URL submission, then poll for completion |
| SarvamAI | Y | - | ~ | - | Y | 22+ Indian languages with provider-specific metadata |
| Speechmatics | Y | - | ~ | - | Y | Batch transcription with polling |

`~` means the MEAI streaming method exists but returns the final transcript after processing completes, not true incremental recognition updates.

`Y*` means the URL path is exposed through `RawRepresentationFactory`, not a dedicated MEAI option.

## Universal Usage

```csharp
using Microsoft.Extensions.AI;

ISpeechToTextClient client = /* any provider */;

await using var audioStream = File.OpenRead("audio.mp3");
var response = await client.GetTextAsync(audioStream);

Console.WriteLine(response.Text);
```

## Initialization Patterns

### Standard direct SDK

```csharp
using AssemblyAI;
using Microsoft.Extensions.AI;

ISpeechToTextClient client = new AssemblyAIClient(apiKey);
```

### Deepgram realtime streaming

```csharp
using Deepgram;
using Microsoft.Extensions.AI;

ISpeechToTextClient client = new DeepgramClient(apiKey);

await using var audioStream = File.OpenRead("audio.wav");
await foreach (var update in client.GetStreamingTextAsync(audioStream))
{
    Console.Write(update.Text);
}
```

### URL-based batch transcription

```csharp
using Microsoft.Extensions.AI;
using RevAI;

ISpeechToTextClient client = new RevAIClient(apiKey);

var response = await client.GetTextAsync(
    Stream.Null,
    new SpeechToTextOptions
    {
        RawRepresentationFactory = _ => new SubmitTranscriptionJobRequest
        {
            MediaUrl = "https://example.com/meeting.mp3",
        },
    });
```

## Streaming Guidance

- `Deepgram` is the only current adapter in this group with truly incremental MEAI streaming.
- `ElevenLabs`, `Reka`, `RevAI`, `SarvamAI`, `Speechmatics`, `FishAudio`, `AssemblyAI`, `Cartesia`, and `Gladia` all expose `GetStreamingTextAsync()`, but the current adapters yield the final transcript after the provider finishes processing.
- If you need provider-native realtime features such as interim hypotheses, diarization events, or richer WebSocket controls, use the provider SDK directly in addition to or instead of the MEAI abstraction.

## SDK Guides

- [Reka](https://tryagi.github.io/Reka/guides/meai/)
- [ElevenLabs](https://tryagi.github.io/ElevenLabs/guides/meai/)
- [AssemblyAI](https://tryagi.github.io/AssemblyAI/guides/meai/)
- [Deepgram](https://tryagi.github.io/Deepgram/guides/meai/)
- [Gladia](https://tryagi.github.io/Gladia/guides/meai/)
- [Cartesia](https://tryagi.github.io/Cartesia/guides/meai/)
- [FishAudio](https://tryagi.github.io/FishAudio/guides/meai/)
- [RevAI](https://tryagi.github.io/RevAI/guides/meai/)
- [SarvamAI](https://tryagi.github.io/SarvamAI/guides/meai/)
- [Speechmatics](https://tryagi.github.io/Speechmatics/guides/meai/)
