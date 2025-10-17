Problem
Developers lose time switching between typing prompts and mentally iterating on code changes. Hands-free or rapid verbal clarification can accelerate refactors, explanations, and test generation. Accessibility and multitasking (pairing, hardware debugging) contexts amplify this friction.

Insight
A low-latency streaming voice layer can compress prompt cycles. Spoken language captures intent ("extract just the sorting part") faster than composing multi-sentence instructions, enabling incremental refinement and immediate follow-up.

Concept
Push-to-talk overlay in Cursor → streaming ASR → transcript → lightweight intent parsing (commands vs free-form prompt) → agent response (text + optional TTS). Keeps short-lived conversational context scoped to current file/buffer. Confirmation required for write operations (apply diff). Privacy mode for local ASR/TTS fallback.

Potential Impact
- Productivity: >25% faster iteration for exploratory refactor + explanation tasks (target metric: average time from idea to agent response).
- Accessibility: Broadens usage for voice-dependent developers.
- Differentiation: Multimodal agent experience strengthens adoption.
- Learning: Optional logging (opt-in) of spoken clarifications improves future suggestion accuracy.

Feasibility Notes
Latency target: <800ms partial caption appearance. Local Whisper (medium or small) may meet acceptable accuracy with GPU; cloud realtime endpoints give lower ops overhead. Intent parsing via prompt-engineered LLM or small classifier. Risk of mis-recognition mitigated by diff confirmation. Integration: microphone capture → WebSocket → partial transcript display.

Related
- VSCode voice command extensions
- Whisper / OpenAI Realtime / Vosk / Coqui STT
- Accessibility guidelines (WCAG voice alternatives)
- Prior research: multimodal dev productivity

Evolution Ideas
Phase 1: Passive transcript + manual “Send to agent”
Phase 2: Streaming intent classification, automatic agent reply
Phase 3: Inline diff preview + spoken “apply” confirmation
Phase 4: File summarization via voice (“summarize this file”)
Phase 5: Multi-agent comparison (“compare two implementations”)

Risk Flags
Accuracy drift, privacy (audio data), latency, noisy environments, inadvertent triggering.

Impact Hypothesis
If hands-free conversational prompting works reliably, mean time to first actionable agent suggestion in exploratory tasks decreases by >25%.

Next Step
Decide ASR/TTS stack; prototype push-to-talk capture + transcript panel.

Scoring (initial placeholder)
Impact: 4–5 (needs validation)
Feasibility: 3 (stack clear; integration non-trivial)
Novelty: 4 (existing voice control; integrated dev-agent loop less common)
Urgency: 3 (beneficial but not time-sensitive)
Alignment: 5 (tool augmentation + accessibility)

Checklist
[ ] Create idea file (done, link: ideas/2025-10-17-cursor-voice-assistant.md)
[ ] Select ASR engine & measure latency baseline
[ ] Draft minimal UI mock (overlay + transcript)
[ ] Define confirmation pattern for write actions
[ ] Establish evaluation metric: time from push-to-talk to agent response
