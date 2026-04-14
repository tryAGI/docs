# Realtime Avatar Streaming

tryAGI provides a unified `IRealtimeAvatarClient` abstraction for interactive avatar streaming. Send text or audio, receive lip-synced video and audio from AI-powered avatars in real time.

## Supported Providers

| Provider | SDK | Transport | Input | Output |
|----------|-----|-----------|-------|--------|
| [D-ID](https://www.d-id.com/) | `tryAGI.DId` | WebRTC (SIPSorcery) | Text | Video + Audio |
| [Simli](https://simli.com/) | `tryAGI.Simli` | WebSocket + WebRTC | Audio (PCM16) | Video + Audio |
| [Anam](https://anam.ai/) | `tryAGI.Anam` | REST + WebRTC | Text | Video + Audio |
| [AvatarTalk](https://avatartalk.ai/) | `tryAGI.AvatarTalk` | REST + WebSocket | Text | Video (MP4) |
| [Pika](https://pika.art/) | `tryAGI.Pika` | REST (meeting bot) | Text | Meeting video (30 FPS) |

## Quick Start -- D-ID

D-ID uses WebRTC for bi-directional streaming with AI agents. The SDK handles SDP/ICE negotiation automatically.

### Installation

```bash
dotnet add package tryAGI.DId
```

### Using the Unified Interface

```csharp
using DId;
using tryAGI.RealtimeAvatar;

var client = new DIdClient(apiKey);

// Connect returns IRealtimeAvatarClient
await using IRealtimeAvatarClient avatar = await DIdRealtimeAvatarClient.ConnectAsync(
    client,
    agentId: "your-agent-id");

// Send text — the avatar speaks and lip-syncs
await avatar.SendTextAsync("Hello! How can I help you today?");

// Receive video frames (H.264 or VP8)
await foreach (var frame in avatar.ReceiveVideoFramesAsync())
{
    // frame.Data = encoded video bytes
    // frame.Codec = "H264" or "VP8"
    // frame.Timestamp = RTP timestamp
}
```

### Using the D-ID Session Directly

For more control over WebRTC features:

```csharp
using DId;

var client = new DIdClient(apiKey);

await using var session = await DIdRealtimeSession.ConnectAsync(
    client,
    agentId: "your-agent-id",
    compatibilityMode: CreateStreamRequestCompatibilityMode.On, // VP8
    streamWarmup: true);

// Send a chat message
await session.SendMessageAsync("Tell me about quantum computing");

// Receive video, audio, and data channel messages concurrently
var videoTask = Task.Run(async () =>
{
    await foreach (var frame in session.ReceiveVideoFramesAsync())
    {
        Console.WriteLine($"Video: {frame.Format.FormatName} @ {frame.Timestamp}");
    }
});

var audioTask = Task.Run(async () =>
{
    await foreach (var frame in session.ReceiveAudioFramesAsync())
    {
        Console.WriteLine($"Audio: {frame.Format.FormatName}, {frame.DurationMs}ms");
    }
});

var dataTask = Task.Run(async () =>
{
    await foreach (var msg in session.ReceiveDataMessagesAsync())
    {
        Console.WriteLine($"Data: {msg}");
    }
});
```

## Quick Start -- Simli

Simli uses WebSocket for signaling and audio input, with WebRTC for video/audio output.

### Installation

```bash
dotnet add package tryAGI.Simli
```

### P2P WebSocket Connection

```csharp
using Simli;
using Simli.Realtime;

var client = new SimliClient(apiKey);

// 1. Get a session token
var token = await client.Compose.CreateComposeTokenAsync(new CreateComposeTokenRequest
{
    FaceId = "your-face-id",
});

// 2. Connect via WebSocket
var ws = new SimliPeerToPeerRealtimeClient();
await ws.ConnectAsync(token.SessionToken ?? string.Empty);

// 3. Send PCM16 audio for lip-sync
byte[] pcmAudio = GetAudioBytes(); // 16-bit PCM
await ws.SendAudioAsync(pcmAudio);

// 4. Listen for server events (SDP answer, status signals)
await foreach (var evt in ws.ReceiveEventsAsync())
{
    Console.WriteLine($"{evt.Type}: {evt.RawPayload}");
}
```

## Quick Start -- Pika

Pika uses a meeting-bot approach: an AI avatar joins a video call (Google Meet, Zoom, etc.) and participates in real time.

### Installation

```bash
dotnet add package tryAGI.Pika
```

### Join a Meeting with an AI Avatar

```csharp
using Pika;

var client = new PikaClient(devKey);

// Check balance
var balance = await client.Developer.GetBalanceAsync();

// Join a Google Meet with an AI avatar
var session = await client.Sessions.CreateMeetingSessionAsync(
    meetUrl: "https://meet.google.com/abc-defg-hij",
    botName: "AI Assistant",
    platform: CreateMeetingSessionRequestPlatform.GoogleMeet,
    // image and voiceId parameters
);

// Poll until ready
var status = await client.Sessions.GetSessionStatusAsync(session.SessionId);
```

## The `IRealtimeAvatarClient` Interface

All adapters implement a common interface for provider-agnostic code:

```csharp
namespace tryAGI.RealtimeAvatar;

public interface IRealtimeAvatarClient : IAsyncDisposable
{
    bool IsConnected { get; }
    Task SendTextAsync(string text, CancellationToken cancellationToken = default);
    Task SendAudioAsync(ReadOnlyMemory<byte> pcm16Audio, CancellationToken cancellationToken = default);
    IAsyncEnumerable<AvatarVideoFrame> ReceiveVideoFramesAsync(CancellationToken cancellationToken = default);
    IAsyncEnumerable<AvatarAudioFrame> ReceiveAudioFramesAsync(CancellationToken cancellationToken = default);
}
```

### Frame Records

```csharp
public sealed record AvatarVideoFrame(byte[] Data, string Codec, uint Timestamp);
public sealed record AvatarAudioFrame(byte[] Data, string Codec, uint DurationMs);
```

### Provider Capabilities

Not all providers support both text and audio input:

| Provider | `SendTextAsync` | `SendAudioAsync` | `ReceiveVideoFramesAsync` | `ReceiveAudioFramesAsync` |
|----------|-----------------|-------------------|---------------------------|---------------------------|
| D-ID | Yes | No (text only) | Yes (WebRTC) | Yes (WebRTC) |
| Simli | No (audio only) | Yes | Via WebRTC* | Via WebRTC* |
| Pika | Yes | No (text only) | Meeting video | Meeting audio |

*Simli delivers video/audio over WebRTC tracks. The WebSocket client handles signaling and audio input; a WebRTC peer connection is needed to receive the output streams.

## Architecture

```
+---------------------+
|  Your Application   |
|                     |
| IRealtimeAvatarClient
+----------+----------+
           |
    +------+------+
    |             |            |
+---v---+   +---v---+   +---v---+
| D-ID  |   | Simli |   | Pika  |  ... more providers
|Adapter|   |Adapter|   |Adapter|
+---+---+   +---+---+   +---+---+
    |           |            |
+---v---+   +--v----+   +--v----+
|WebRTC |   |  WS + |   | REST  |
|SIPSor.|   | WebRTC|   |(mtg.) |
+-------+   +-------+   +-------+
```

## WebRTC in .NET

The D-ID adapter uses [SIPSorcery](https://github.com/sipsorcery/sipsorcery) -- a pure C# WebRTC library:

- **Cross-platform**: Windows, macOS, Linux
- **Audio codecs**: OPUS, G.711, G.722
- **Video codecs**: H.264, VP8 (via FFmpeg)
- **Handles**: RTCPeerConnection, ICE negotiation, SDP exchange, data channels

Video frames arrive as encoded H.264 or VP8 data. Decoding requires FFmpeg or platform-specific decoders.

## Related SDKs

| SDK | Install | Description |
|-----|---------|-------------|
| [D-ID](https://github.com/tryAGI/DId) | `dotnet add package tryAGI.DId` | Talking avatars, AI agents, WebRTC streaming |
| [Simli](https://github.com/tryAGI/Simli) | `dotnet add package tryAGI.Simli` | Real-time avatar with WebRTC + WebSocket |
| [Anam](https://github.com/tryAGI/Anam) | `dotnet add package tryAGI.Anam` | Ultra-low-latency avatars (180ms) |
| [AvatarTalk](https://github.com/tryAGI/AvatarTalk) | `dotnet add package tryAGI.AvatarTalk` | 13 avatars, 16 languages, WebSocket streaming |
| [Pika](https://github.com/tryAGI/Pika) | `dotnet add package tryAGI.Pika` | Real-time AI avatars for video meetings, voice cloning |
