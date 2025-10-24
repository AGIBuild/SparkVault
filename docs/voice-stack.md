# Voice Stack Overview

## Goals
- Sub-800ms first partial transcript.
- Reliable command vs free-form intent separation.
- Local privacy mode fallback.
- Measurable iteration improvement (>25% faster prompt loop).

## Architecture (Phase 1)
Client (Cursor extension / overlay) -> WebSocket Gateway -> ASR Engine -> Intent Parsing -> Agent Prompt Builder -> Response + (optional TTS)

```
[Mic Capture] --(PCM chunks 100-200ms)--> [WS Gateway]
   |                                     |
   |-- partial transcript <-- ASR stream |
   |-- final transcript ---------------->|
```

## Components
1. Capture Layer
   - getUserMedia or desktop audio API
   - Buffer size: 1600 samples @16kHz per 100ms
2. Transport
   - WebSocket JSON framing:
     - audio_chunk: {seq, base64_pcm, ts}
     - control: start/stop
     - partial: {seq, text}
     - final: {text, confidence}
     - error: {code, message}
3. ASR
   - Default: Cloud streaming (OpenAI / etc.)
   - Fallback: Local Whisper (small) via server process
4. Intent Parsing
   - Heuristics + LLM classification categories:
     - refactor, explain, test, navigate, other
   - Confirmation needed for refactor/apply operations.
5. Agent Integration
   - Compose structured prompt with context (file path, selection snippet).
6. TTS (Phase 2+ optional)
   - Local Piper or Edge TTS

## Data Flow (Simplified)
User speech -> PCM frames -> WS -> ASR stream -> partial transcripts displayed -> final transcript -> intent classification -> prompt -> agent response -> optional voice output.

## Metrics
- t_first_partial = first partial timestamp - capture_start
- t_final = final transcript timestamp - capture_start
- avg_partial_interval (smoothness)
- WER (sampled, manual references)
- Confirmation error rate (mis-applied operations prevented)

## Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| High latency | Smaller chunk size, streaming decode, GPU for Whisper |
| Mis-recognition causing code change | Mandatory diff preview + voice/text confirm |
| Privacy concerns | Local ASR mode + indicator light |
| Noise environment | Energy threshold, optional push-to-talk only |
| Over-triggering commands | Intent confidence threshold, fallback to plain prompt |

## Next Steps
1. Implement WS protocol skeleton.
2. Integrate cloud streaming ASR.
3. Log latency & transcripts to local debug file.
4. Add basic intent classifier (prompt few-shot).
5. Confirm diff application UX pattern.
