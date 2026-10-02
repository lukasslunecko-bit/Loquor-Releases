# Loquor

Turn academic readings into listening text, optional exam revision, and MP3s from one Windows desktop screen.

## Run on Windows

Download **LoquorSetup-0.3.0.exe** from [public releases](https://github.com/lukasslunecko-bit/Loquor-Releases/releases/latest). Python, libraries, the MP3 encoder and the Kokoro offline model are included. Alternatively extract the entire Windows ZIP and open `Loquor.exe`; keep its `_internal` folder beside it. Windows 10/11, x64. Installation needs no administrator rights. The installer is currently unsigned. The offline model makes this download substantially larger than earlier releases.

1. Add PDF, DOCX, TXT or Markdown files. PDFs need readable text or an existing OCR layer.
2. Choose the output folder, narration engine, voice and speed on the main screen. Preview the voice with an editable sample. Less frequent choices live under **Settings**.
3. **Use Codex automatically** improves the complete reading after local extraction when a signed-in Codex CLI is available. It uses your ChatGPT/Codex allowance, not an API key. Codex itself is not bundled.
4. Choose **Prepare reading** to review the text, or **Prepare + MP3** to continue into narration.
5. Without Codex, use **Copy prompt + reading**, or the saved `*_chatbot_request.txt`, in your preferred chatbot. Import its complete response and convert it to MP3. Opening a chatbot does not submit text automatically.

Local cleanup uses no generative model or network calls. It removes selected headers, page numbers, footnotes, tables, captions, references and links, joins wrapped text, and conservatively preserves substantive content. Review the result and removal report: unusual layouts, poor OCR, complex phonetics and formulas can still need correction. Image-only PDFs need OCR beforehand. Embedded document instructions are treated as source data.

## Narration

**Gemini online** is the preferred engine, with Aoede and instructions for clear British English delivery. Reading speed defaults to **1.15×**, revision to **1.00×**. **Set up Google** opens a guided window with a direct API-key link, masked entry and a connection test. For free-only use, create a Google AI Studio key for a project without paid billing. Google controls eligibility and quotas; Loquor does not enable billing, and a key for a paid project can incur charges. Connection testing sends one short neutral sentence. The current model is `gemini-3.8-flash-tts`.

**Kokoro offline** runs entirely on your CPU without an account or key. Emma and Isabella are included; Emma is the default. Both reading and revision default to **1.00×**. Rendering can take longer than the finished recording on ordinary laptops. Select Kokoro directly to narrate without sending text to a speech service.

**Microsoft Edge online** and **installed Windows voices offline** remain available. Edge uses the unofficial edge-tts service, with Sonia as the British English default. Compatible SAPI/Windows speech voices appear in local mode; Narrator-only natural voices may not be accessible. Under narration Settings, **Windows voice packs** installs standard English speech capabilities and their language dependencies. This optional operation needs internet, Windows administrator approval and sometimes a restart; it does not install Narrator natural voices or change the display language.

Speech speed is adjusted with pitch-preserving audio processing after synthesis. Separate reading/revision presets are stored per engine. Changing the main-screen speed updates the current preset. Automatically queued readings and revision batches use their corresponding presets. For manually added files, choose **Use for** before converting. Quiz markers such as `[[PAUSE:15]]` become fifteen seconds of actual silence, independently of speech speed.

## Google blocks, interruptions and resumable jobs

Loquor distinguishes a response mentioning possible copyright similarity from an unspecified policy block. It displays Google's explanation when available; an ambiguous refusal is not labelled as proven copyright infringement.

The default for a copyright/policy block is to **switch the whole document to Kokoro**, keeping one narrator throughout. Narration Settings also offers **Kokoro only for blocked sections** or **Ask each time**. Section fallback can mix narrators and uses each engine's speed preset. These choices apply to Google's content blocks; quota, access and connection errors preserve progress and pause after bounded retries. You can resume later or choose Kokoro yourself.

Audio is generated in short sections and cached under `.loquor-jobs` inside your MP3 folder. **Convert / Resume** reuses completed sections when the text and settings match. Keep this folder to retain progress; deleting it removes the cache, not your finished MP3s. Changing text or settings starts a separate job. Google-blocked sections are recorded so resuming does not repeatedly submit the same failed passage. A final MP3 is assembled only when all required sections have succeeded and the assembled file decodes. This catches technical failures and obviously truncated audio; it is not a word-by-word transcription check.

**Condense for study** creates a separate, explicitly shortened learner-focused adaptation. Copy a prompt plus the text for any chatbot, or generate it using your signed-in Codex CLI. The original stays intact, and you review the new text before narrating it. Condensation is never an automatic response to a refusal, and Gemini may still decline an adaptation.

## Saved files and revision

Each prepared document has its own numbered output folder, normally in Documents/Loquor. The original is preserved. Listening text, a single prompt-plus-reading TXT, optional revision request and a detailed cleanup report are saved. Imported or Codex-improved text is saved separately. Repeated preparation and finished audio use numbered filenames.

Optional exam revision produces a summary and a complete quiz: question, silent thinking time, exemplar answer, repeated question. Pause markers are specific to Loquor. Review generated material; practice questions do not predict the actual exam.

## Updates and privacy

Loquor checks the public release repository at startup unless disabled. This check sends no documents. A newer stable version is announced in the app. **Download and install** is user initiated, verifies GitHub's SHA-256 digest and starts the installer. Offline checks can be retried manually. Documents and audio stay in your output folder during upgrades/uninstall.

Settings persist in LocalAppData/Loquor. Google keys are protected using Windows per-user DPAPI in a separate file, never in settings JSON, job metadata, prompts or the installer. Removing the key is available in Google setup. Someone running code as the same Windows user can still access that user's protected credentials.

Enabled Codex cleanup/revision/condensation sends source text to OpenAI. Gemini narration sends text to Google; Edge sends it to Microsoft. Local extraction, Kokoro and installed Windows speech stay on your computer. Reading text and generated audio in your job cache are not encrypted. No account credentials, personal readings or generated audio are distributed with the application.

## Source and builds

Optional source snapshots accompany public binary releases; the development Git repository is private. Loquor is GNU AGPL version 3 or later; see LICENSE and third-party notices. Classmates need only the installer.

For development, install Python 3.14 with tkinter, create a virtual environment, run `python -m pip install -r requirements-build.txt`, then `python fetch_kokoro.py` and `python Loquor.pyw`. The build-time model download is pinned to a verified SHA-256 hash; end users receive it already bundled. Run `python -m unittest discover -s tests -v` for the source checks. Build using `Build_Release.ps1 -Compiler C:\path\to\ISCC.exe` with Inno Setup 7.1.0. `python package_release.py --source-only` creates a source snapshot without model binaries, build outputs or secrets.

The public Windows build workflow downloads that snapshot and the pinned model, runs source and voice-installation tests, builds the standalone app, runs a real bundled offline synthesis/MP3 test, then publishes the installer and portable package with checksums. Third-party source/build links are in THIRD_PARTY_NOTICES.md and DEPENDENCIES.json.

Validation includes the three original academic references in earlier extraction tests; Emma/Isabella auditions on the original two speech samples; current fallback, cancellation/resume and pause tests; actual offline MP3 synthesis, voice preview, Windows key protection and UI preference checks. Gemini success and copyright-block response shapes were observed in earlier API trials. A clean Windows virtual machine has not been tested. Full-length AI adaptations still deserve editorial review.
