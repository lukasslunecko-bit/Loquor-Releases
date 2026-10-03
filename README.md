# Loquor

Prepare academic readings, revision summaries and spoken quizzes, then turn the selected outputs into MP3s from one Windows screen.

## Windows setup

Download **LoquorSetup-0.6.0.exe** from [public releases](https://github.com/lukasslunecko-bit/Loquor-Releases/releases/latest). Python, dependencies, the MP3 encoder, local OCR language data and Kokoro's offline model are included. Windows 10/11 x64; installation is per user and needs no administrator rights. The installer is currently unsigned. The portable ZIP also works: extract everything and keep `_internal` beside `Loquor.exe`.

1. Add or drag and drop PDF, DOCX, TXT or Markdown files. Scanned PDFs can be recognised locally; automatic OCR is enabled by default.
2. Defaults select a complete reading, summary and quiz, each as text and audio. Their text/audio checkboxes are independent. **Question count, thinking time and summary length are on the main screen.** Optional presets select long reading, exam revision, offline reading or quality-first work.
3. Open **Settings → Connections** once to select separate defaults for study-text preparation and narration. The main screen allows a different route for a particular job. Setup status identifies missing sign-in or API keys.
4. Click **Produce selected outputs**. The workflow graphic, textual Activity status, actual narrator, elapsed time and rough ETA explain progress. Start and Cancel remain visible when scrolling. Ctrl+Enter starts; Escape cancels. Narrow windows stack the panels and wrap the workflow graphic.
5. Open **Results & recent projects** to play/open outputs, reopen saved jobs, retry a selected output with another voice, or export only finished audio for a phone. Completed outputs remain usable when another stage fails.

Original documents remain intact. Local cleanup removes selected headers, page numbers, footnotes, tables, captions, references, links and broken line wrapping. Poor scans, unusual layouts, complex phonetics and formulas can still require correction. Embedded source instructions are treated as academic data.

## Local PDF OCR

**Settings → PDF OCR** controls recognition. Automatic mode keeps usable native text and recognises image-only, sparse scan or visibly damaged text pages. Mixed PDFs are handled page by page. Select **Redo all pages** when an existing OCR layer is incorrect or incomplete; detecting every plausible but wrong text layer automatically is not possible. Off retains extraction-only behaviour.

The packaged MuPDF/Tesseract engine and checksum-pinned language data run locally, with no API, GPU or separate Tesseract installation needed. English is selected by default; Czech, German, French and Spanish are bundled, including mixed-language selections. OCR improves grayscale contrast, checks 0/90/180/270-degree orientation and can straighten tilt up to 8 degrees. Manual clockwise rotation is available. Recognition defaults to 300 DPI with bounded image memory; upscaling cannot restore missing scan detail. [PyMuPDF OCR documentation](https://pymupdf.readthedocs.io/en/latest/recipes-ocr.html), [Tesseract quality guidance](https://tesseract-ocr.github.io/tessdoc/ImproveQuality.html).

Activity shows the page and operation. File selection checks size without starting OCR; word counts and quota estimates remain provisional for unread pages. Initial timing allows roughly 20 seconds per OCR page and varies with quality, orientation and hardware. A cancellable worker retains completed pages in `.loquor-workflow/ocr` for resumption. Changing cleanup preferences does not require recognising cached pages again.

For OCR documents, the document folder contains **raw extracted text**, the cleaned listening text and a page report recording rotation, tilt and review warnings. Optionally save a corrected searchable PDF copy. Caches contain unencrypted document text and images. The original PDF is never overwritten. Word spacing is reconstructed from positions before listening cleanup. Check names, quantities, multi-column order, tables and unusual notation against the source. Plausibility and coverage signals are advisory, not guaranteed accuracy. Blurred print, handwriting, strong perspective and curved book pages can need manual correction.

The existing preparation provider can repair clear OCR errors afterwards, preserving uncertainty instead of inventing facts. Local cleanup with reading-only outputs and Kokoro/Windows speech keeps the whole process offline. Quality-first review also includes OCR warnings.

## Preparation connections

**ChatGPT through Codex** remains the default. Loquor detects the official native CLI, can run its official Windows installer, and launches its own browser sign-in. An eligible ChatGPT/Codex allowance is required; no OpenAI API key is needed for this route. API-billing environment overrides are excluded from subscription subprocesses. [Official Codex CLI setup](https://learn.chatgpt.com/docs/codex/cli).

**Claude through Claude Code** is an additional experimental preparation route. Install the official native client using the setup button/WinGet, sign in with your own Claude subscription, then recheck. Git for Windows may also be required. Loquor invokes the unmodified client with tools and MCP disabled; it never collects subscription session tokens. Provider terms and allowances apply. This adapter has transport/command-level checks but has not been validated with a signed-in Claude account on the development machine. [Official setup](https://code.claude.com/docs/en/setup), [integration conditions](https://code.claude.com/docs/en/legal-and-compliance).

**OpenAI API, Claude API and Gemini API** can prepare study text using a securely saved key and an editable model ID. OpenAI/Claude API calls require the explicit **Allow separately billed API calls** preference, disabled by default. A ChatGPT or Claude subscription does not supply API credits. Gemini eligibility and billing depend on the key's project; Loquor cannot determine whether that project has paid billing enabled. Connection testing sends a short neutral prompt and can consume allowance or API usage. These text API adapters have mocked transport tests; paid endpoints have not been exercised with real credentials.

**Manual chatbot handoff** saves prompt-plus-source requests for missing stages. In Results, copy a request, open your chosen chatbot, import its JSON reply and resume. Long adaptations are split into sections, so manual preparation can require several replies. Opening a chatbot does not submit text automatically. Review also retains the earlier plain-text full-reading handoff/import tools.

**Local cleanup only** needs no AI account. Select reading outputs alone and an offline narrator for a completely local route. Summary and quiz require an AI or a manual chatbot reply.

Settings are organised into Connections, Study material, Document cleanup, PDF OCR, Narration, Output and Updates. Study material accepts additional prompt preferences and optional question repetition. The source-only and faithful-reading instructions remain in the generated prompts. The Gemini speech planning budget is under **Connections**, separate from quiz settings.

## Narration

- **Microsoft Edge online:** the new default is British English `en-GB-SoniaNeural`, reading/revision 1.00×, with whole-recording offline Kokoro fallback enabled. No API key is needed. A cached English voice catalog keeps the dropdown usable before connecting; Refresh fetches the current catalog. Edge uses the unofficial edge-tts service. When it is unavailable, the rest of that batch continues locally. Untouched 0.5.0 factory defaults migrate to Sonia; custom saved narrator choices stay intact.
- **Gemini online:** optional; Aoede is its default voice; reading 1.15×, revision 1.00×. Connect a Google AI Studio key. For free-only use choose a project without paid billing. The speech model is `gemini-3.8-flash-tts`.
- **Kokoro offline:** bundled British Emma, Isabella, George and Lewis; Emma is the default fallback. Reading and revision default to 1.00×. CPU synthesis can take longer than the recording on ordinary laptops.
- **OpenAI speech API:** optional separately billed `gpt-4o-mini-tts`, with Marin and Cedar among the choices. Requires an OpenAI API key and explicit API-billing opt-in. Preview before committing to a long job. This route has not been auditioned live in this release. [Official speech guide](https://developers.openai.com/api/docs/guides/text-to-speech).
- **Installed Windows voices offline** remain available. Standard SAPI/Windows voices depend on the computer. Narrator-only natural voices may not be accessible. Windows voice-pack setup is optional and can require administrator approval, internet and a restart.

These are synthetic voices. Speed changes use pitch-preserving audio processing after synthesis; thinking pauses keep their full duration. **Use source sample** auditions a short cleaned excerpt. Narration settings offer accent/style instructions, optional volume normalization and a pronunciation dictionary in `term = spoken form` format. The dictionary changes only speech input, not the academic text.

## Recovery, quality and quota

Extraction, section adaptation, summary and structured questions have independent caches. Changing summary length does not regenerate the reading or quiz; changing thinking time does not call an AI again. Raw speech is cached independently of speed and silence, so pause/speed changes reuse speech and reassemble the recording. Unrelated engine settings do not invalidate an output. Content digests detect changed completed audio.

Narration consumes immutable saved text snapshots. Editing review text creates input for a later run rather than changing the running job. The original cleaned reading stays available. Reading adaptations are checked for substantial shortening, unreadable characters, missing numbers and heading coverage; these are warnings, not proof of semantic fidelity. Quality-first mode can pause before narration when warnings need review. Review the reading against its source and mark it reviewed in Results, then resume. Practice questions are source-grounded study aids, not predictions of actual exam questions.

A failed summary/quiz no longer blocks other usable outputs. Unreadable inputs are reported while other documents continue. Cancellation saves finished stages. Reopen a recent job or click Produce with the same inputs to resume. The current cache format is new in 0.5.0: older finished text/audio is preserved, but some 0.4.0 generated stages may be prepared again. PDF extraction is renewed for the new OCR settings where needed; plaintext/Word cache identities ignore PDF-only settings. Keep `.loquor-workflow`, `Audio/.loquor-jobs` and `Audio/.loquor-speech` to retain progress. Caches contain unencrypted text/audio.

Before Gemini narration, Loquor estimates speech requests and can recommend Kokoro. The initial **10/day is a planning budget, not a guaranteed Google free-tier quota**. Set it to your project's active limit using the AI Studio link in Connections. Local counts exclude other applications, computers and project users and reset at midnight US Pacific time. Exact remaining project quota cannot be queried by Loquor.

Exhausted Gemini speech quota defaults to whole-recording Kokoro fallback and continues remaining batch outputs with Kokoro. A possible copyright/policy restriction defaults to whole-document fallback; blocked-section fallback and Ask each time remain optional. Ambiguous refusals are not labelled as proven copyright infringement. Activity and Results show the effective engine, voice and speed. Paid services are never selected as automatic fallbacks.

Final audio is assembled only when all its speech sections succeed, then checked for decoding. This catches technical failures and obviously short audio, not every spoken omission or repetition. A cancelled API request may still finish and consume usage at its provider. Condensation remains a separate, explicitly shortened study adaptation that the user reviews.

## Privacy, updates and sharing

Local extraction/OCR, Kokoro and installed Windows speech stay on the computer. Selected online preparation/narration sends source text to that provider. API keys use Windows per-user DPAPI in separate files; they never enter job/settings JSON, prompts or shared packages. The official clients own subscription authentication. Someone running code as the same Windows user can access that user's protected credentials.

Recent-project entries only reference saved job files. Diagnostic exports omit document text, names, paths, prompts, raw errors and credentials. Audio-only export excludes source documents, prompts and caches.

Startup update checks use the public GitHub release repository and send no documents. Download/install is user initiated and verifies GitHub's SHA-256 digest. Let active recordings finish before installing an update. Upgrades preserve saved work and profiles.

## Development

The development repository is private; source snapshots accompany public releases. Loquor is GNU AGPL version 3 or later; see LICENSE and THIRD_PARTY_NOTICES.md. Classmates need only the installer.

Use Python 3.14 with tkinter, install `requirements-build.txt`, run `python fetch_ocr.py` and `python fetch_kokoro.py`, then `python Loquor.pyw`. Run `python -m unittest discover -s tests -v`. Build with `Build_Release.ps1 -Compiler C:\path\to\ISCC.exe` (Inno Setup 7.1.0). `python package_release.py --source-only` excludes models, work/build outputs and local review notes. The pinned OCR language and speech-model downloads are SHA-256 verified; end users receive them bundled.

GitHub builds source snapshots on Windows, runs source/voice tests and a real packaged offline synthesis test, then publishes the installer and portable ZIP only on success. See VALIDATION.md and ROADMAP.md for current evidence and subsequent work. A clean Windows VM and full-length provider matrix have not been tested.
