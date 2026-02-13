# Runbook: Local voice transcription (whisper-cli)

Goal: speech→text without paid APIs.

## macOS (Homebrew)
- Install: `brew install whisper-cpp ffmpeg`
- Download model (example): `ggml-base.bin` from whisper.cpp releases.

## OpenClaw config (example)
Add to `tools.media.audio.models` (CLI first, provider fallback optional):

```json5
{
  tools: {
    media: {
      audio: {
        enabled: true,
        models: [
          {
            type: "cli",
            command: "/opt/homebrew/bin/whisper-cli",
            args: ["-m", "~/.openclaw/models/whisper/ggml-base.bin", "-f", "{{MediaPath}}", "-nt"],
            timeoutSeconds: 90
          }
        ]
      }
    }
  }
}
```

## Verification
- Send a short voice note.
- Expect transcript injected into message body / `{{Transcript}}`.
