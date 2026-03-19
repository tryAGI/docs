# ISpeechToTextClient Feature Matrix

The `ISpeechToTextClient` interface provides a unified API for speech-to-text transcription.

## Feature comparison

| Feature | Reka | ElevenLabs | AssemblyAI |
|---------|:-:|:-:|:-:|
| File transcription | Y | Y | Y |
| URL transcription | Y | - | Y |
| Streaming | -[^1] | Y | - |
| Translation | Y | - | - |
| Timestamps | Y | Y | Y |

[^1]: Reka delegates to non-streaming due to API limitations.

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

## Per-SDK documentation

| SDK | Documentation |
|-----|--------------|
| Reka | [tryagi.github.io/Reka/guides/meai/](https://tryagi.github.io/Reka/guides/meai/) |
| ElevenLabs | [tryagi.github.io/ElevenLabs/guides/meai/](https://tryagi.github.io/ElevenLabs/guides/meai/) |
| AssemblyAI | [tryagi.github.io/AssemblyAI/guides/meai/](https://tryagi.github.io/AssemblyAI/guides/meai/) |
