# ISpeechToTextClient Feature Matrix

The `ISpeechToTextClient` interface provides a unified API for speech-to-text transcription across 6 providers.

## Feature comparison

| Feature | Reka | ElevenLabs | AssemblyAI | Deepgram | Gladia | Cartesia |
|---------|:-:|:-:|:-:|:-:|:-:|:-:|
| File transcription | Y | Y | Y | -[^2] | Y | Y |
| URL transcription | Y | - | Y | Y | - | - |
| Streaming | -[^1] | Y | - | Y | - | - |
| Translation | Y | - | - | - | - | - |
| Timestamps | Y | Y | Y | Y | Y | Y |
| Languages | 20+ | 29 | 100+ | 30+ | 100+ | 115+ |

[^1]: Reka delegates to non-streaming due to API limitations.
[^2]: Deepgram `GetTextAsync` requires a URL via `RawRepresentationFactory`; `GetStreamingTextAsync` accepts audio streams via WebSocket.

## Universal code example

```csharp
using Microsoft.Extensions.AI;

ISpeechToTextClient client = /* any provider */;

// Transcribe an audio file
await using var stream = File.OpenRead("audio.mp3");
var result = await client.GetTextAsync(stream);
Console.WriteLine(result.Text);
```

## Provider-specific initialization

=== "ElevenLabs"

    ```csharp
    ISpeechToTextClient client = new ElevenLabsClient(apiKey)
        .AsSpeechToTextClient();
    ```

=== "AssemblyAI"

    ```csharp
    ISpeechToTextClient client = new AssemblyAiClient(apiKey)
        .AsSpeechToTextClient();
    ```

=== "Reka"

    ```csharp
    ISpeechToTextClient client = new RekaClient(apiKey)
        .AsSpeechToTextClient();
    ```

=== "Deepgram"

    ```csharp
    // Direct cast — DeepgramClient implements ISpeechToTextClient
    // GetTextAsync requires audio URL via RawRepresentationFactory
    // GetStreamingTextAsync accepts audio streams via WebSocket
    ISpeechToTextClient client = new DeepgramClient(apiKey);
    ```

=== "Gladia"

    ```csharp
    // Direct cast — GladiaClient implements ISpeechToTextClient
    ISpeechToTextClient client = new GladiaClient(apiKey);
    ```

=== "Cartesia"

    ```csharp
    // Direct cast — CartesiaClient implements ISpeechToTextClient
    ISpeechToTextClient client = new CartesiaClient(apiKey);
    ```

## Per-SDK documentation

| SDK | Documentation |
|-----|--------------|
| Reka | [tryagi.github.io/Reka/guides/meai/](https://tryagi.github.io/Reka/guides/meai/) |
| ElevenLabs | [tryagi.github.io/ElevenLabs/guides/meai/](https://tryagi.github.io/ElevenLabs/guides/meai/) |
| AssemblyAI | [tryagi.github.io/AssemblyAI/guides/meai/](https://tryagi.github.io/AssemblyAI/guides/meai/) |
| Deepgram | [tryagi.github.io/Deepgram/guides/meai/](https://tryagi.github.io/Deepgram/guides/meai/) |
| Gladia | [tryagi.github.io/Gladia/guides/meai/](https://tryagi.github.io/Gladia/guides/meai/) |
| Cartesia | [tryagi.github.io/Cartesia/guides/meai/](https://tryagi.github.io/Cartesia/guides/meai/) |
