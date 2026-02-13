# Voice transcription: local-first + provider fallback — candidate

STATUS: candidate

## CLAIM
Use local STT (whisper-cli/whisper.cpp) as primary to keep transcripts reliable and cheap; keep a provider fallback only for resilience.

## HOW_TO_APPLY
- Configure `tools.media.audio.models[0]` as `type:"cli"` and point to `whisper-cli` + a local model.
- Optionally add a second model entry as a provider fallback.

## RISKS/LIMITS
- Local STT needs ffmpeg + model files and correct PATH.
- Docker/Linux builds can break if binaries are platform-mismatched.
