# Release 0.6.0 validation

On Windows 11 x64, Python 3.14.7:

- 59 source tests pass, including native-text preservation without OCR, rotated/faint/tilted scans, blank pages, raw-text/searchable-PDF outputs, cancellation/resumption of completed pages, Edge-to-Kokoro batch fallback, incomplete Edge audio recovery and old-default migration with custom voices preserved.
- A supplied one-page PDF contained five selectable words and one image. Local OCR and positional word spacing recovered 321 listening words, including the names, quantities and grammatical alternatives; the source hash stayed unchanged. No AI provider was called for this recovery.
- Synthetic tilted/low-contrast scans retained the 2019 date, two-group qualifier and causation limitation. A sideways scan was corrected by 270 degrees clockwise. Blank pages and readable native pages retained their place in the PDF.
- Source selection uses provisional counts for pending OCR rather than claiming that an image-only document is unreadable. Page/operation status is shown during recognition. Initial OCR timing is a rough planning estimate, not a guarantee.
- The Windows build and publication workflow fetches checksum-pinned OCR data before source tests and requires the actual packaged worker to recover a sideways scan. Earlier offline voice/MP3/PDF/UI checks remain part of that gate.
- The local standalone executable passed its bundled OCR-worker, language-data, offline audio, workflow and UI smoke checks. A live Sonia test produced a valid 4.06-second recording from a short neutral sample. The main screen and PDF OCR settings were inspected using captures of Loquor's own window.

Limits: OCR can misread plausible text, names and numbers. Every multilingual/column/table/handwriting/perspective scenario has not been tested. Severe blur and page curvature still need manual correction. Advisory plausibility scores are not calibrated character accuracy. Optional online AI uses the existing source-only prompts and cannot reliably reconstruct missing image details.

# Earlier release 0.5.0 validation

On Windows 11 x64, Python 3.14.7:

- 48 source tests pass, including independent summary/quiz failure recovery, skipping unreadable inputs, immutable narration text, stage reuse after study-setting changes, monotonic fallback progress, completed-audio integrity, structured-question validation, manual JSON handoff/resume, quality-review approval, encrypted separate API keys, subscription billing isolation, privacy-preserving diagnostics and audio-only export. A removed narration input reports an error without leaving controls disabled.
- A real signed-in Codex preparation and offline Kokoro run produced the complete reading, 100-word summary and two-question quiz as three text files and three MP3s. Two runs including changed thinking time completed in 162 seconds. The second run used zero new AI calls and reused every raw speech segment.
- Main and settings layouts were rendered in an isolated profile at Windows display scaling, including a 1500×900 desktop window and an 850×650 narrow window. The flow graphic wraps, panels stack and Start/Cancel stay fixed. Quiz variables are shared with the main controls and budget remains separate.
- OpenAI, Claude and Gemini text payloads have mocked transport tests; OpenAI paid-call guards are checked without credentials or charges. Claude Code's native sign-in/command adapter follows current official documentation but has not been validated with a signed-in Claude account. OpenAI speech awaits a live audition.
- Public publication is gated by the Windows build workflow and its bundled offline PDF/Kokoro/MP3/UI smoke test.
- The local standalone executable passed its actual bundled-runtime smoke test: PDF preparation, encoder discovery, Kokoro WAV/MP3, complete local workflow, GUI/drop hook, five installed English Windows voices, preview synthesis and MP3 decoding.

## Earlier release 0.4.0 validation

On Windows 11 x64, Python 3.14.7:

- 25 source tests pass, including one-job reading/summary/quiz outputs, saved-stage resumption, quota fallback across the batch, resumption after quota fallback, Windows cancellation and encrypted credential handling.
- Explicit daily-quota HTTP failures are tested to stop after one attempt. Quota, copyright/policy responses and fallbacks use synthetic/previously recorded response shapes; these checks do not consume live Google quota.
- The Tkinter main screen was visually inspected. Default outputs/speeds, male/female voice filters, source scanning, a real WM_DROPFILES message with Unicode/spaces and deduplication, stage updates, and actual one-click Kokoro WAV production pass in an isolated profile.
- A real complete production job with signed-in Codex and offline Kokoro finished in 283 seconds on a short synthetic curriculum passage, saving the adapted reading, summary and two-question quiz as three texts and three MP3s.
- The source-size check on the three original PDFs estimates about 78, 82 and 116 Gemini speech requests with the default revision settings. All three trigger the conservative free-tier planning warning. These estimates include source clutter and can change after adaptation.
- Packaged-runtime validation includes PDF cleanup, encoder discovery, Kokoro synthesis and MP3 decoding, a local production job, and the new workflow UI/drop hook. The same validation gates public release publication.
- ETA and quota figures are estimates. The app cannot query the project's true remaining free-tier quota. Quiz thinking pauses are excluded from speech request counts and retain their duration during speed changes.

Earlier reference-material validation:

On Windows 11 x64 with Python 3.14.7 for building:

- All three academic reference PDFs prepared successfully: 14,549, 6,730 and 5,938 output words, respectively. No undecoded replacement/control characters remained. Legacy font repairs and complex phonetic notation are reported for review.
- Integrated Tkinter configuration, full-reading export, clipboard handoff/import, preservation of original extracted text, saved project reopening, and preview cancellation passed.
- Actual preview synthesis passed for all five compatible installed English voices on the development machine and online en-GB-SoniaNeural.
- A real Codex complete-reading request preserved the important date, group qualifier and causation limitation in a short synthetic passage.
- Core tests passed for complete-text prompt output, preserved meaningful parentheses/dates, reference removal, required quiz thinking pauses, version checks, verified downloads, and rejection of a mismatched installer checksum.
- PowerShell voice installation was tested with mocked Windows capabilities: dependency order, skipping installed/non-English voices, failure continuation and restart reporting. The test did not install Windows features.
- The frozen executable passed PDF preparation, prompt generation, bundled encoder discovery, Windows voice listing, preview synthesis, local MP3 creation and full MP3 decoding. This test used normal Windows permissions; the tool sandbox cannot access installed voice data correctly.
- Earlier audio integration checks passed for batch cancellation, both speech engines, readable encodings, numbered output files and measured silent quiz pauses.

Limits: no clean Windows VM test or code-signing certificate; full-length AI rewrites still require review. The source PDFs and generated study materials are excluded from shared application files.
