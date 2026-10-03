# Loquor roadmap

## First implementation: 0.5.0

Connections and separate defaults; visible quiz choices/separate Gemini planning; independent output recovery; resumable adaptation sections; independent AI/raw-speech/assembly caching; structured questions and deterministic pauses; coverage warnings and optional review; immutable running inputs; effective narrator; monotonic progress; recent projects/results/retry/export; manual chatbot handoff; per-job presets; pronunciation/source audition; one settings window; fixed production controls and responsive graphic; text-free diagnostics.

The signed-in Codex and offline Kokoro route has an actual end-to-end check. Optional text API and OpenAI speech adapters have mocked transport checks, not live account validation. Claude Code should remain experimental until it is tested with a user's own subscribed account. APIs and subscriptions are separate; no paid automatic fallback is planned.

## Local PDF recognition: 0.6.0

Automatic/forced local OCR, contrast/rotation/deskew, bundled language data, raw-text/searchable-PDF intermediates, per-page resumption and advisory quality warnings. Edge Sonia becomes the default with whole-recording offline Kokoro fallback. Severe blur, curved pages, handwriting and sophisticated table/column validation still need broader testing or additional tools.

## Following implementation and validation

- Audition OpenAI Marin/Cedar with explicit API-billing opt-in; compare pronunciation, consistency and joins using the same reference passages.
- Benchmark Chatterbox Nano/Turbo and Qwen3-TTS on ordinary Windows CPU/GPU hardware before bundling or ranking their quality. Keep heavier runtimes optional and separate from the small default application dependency set.
- Add optional chapter-sized tracks alongside complete recordings and richer track metadata, with boundaries that respect sections/questions.
- Offer a smaller installer with verified voice acquisition during setup, alongside the complete offline installer. Offline fallback must be ready before production.
- Add deeper continuity/terminology checks and hierarchical coverage notes for exceptionally large revision inputs; retain clear limitations of automated semantic checks.
- Improve ETA with stage-specific timing history and clearer provider waiting/retry telemetry. Current estimates use observed narration rates and an initial preparation estimate.
- Broaden keyboard/screen-reader and large-font testing, clean Windows VM installation tests and a provider/account matrix.
- Validate migration/reuse of more 0.4.0 cache stages. Preserve originals, profiles and completed outputs throughout.

No quality superiority is assumed before auditioning. No ChatGPT/Claude conversational voice UI is treated as a downloadable batch TTS API.
