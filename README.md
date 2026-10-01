# Loquor

Turn academic readings into clear listening text, optional exam revision, and MP3s from one Windows desktop screen.

## Run on Windows

Download **LoquorSetup-0.2.0.exe** from [public releases](https://github.com/lukasslunecko-bit/Loquor-Releases/releases/latest) and install it. Python and libraries are included. Alternatively extract the entire Windows ZIP and open `Loquor.exe`; keep its `_internal` folder beside it. Windows 10/11, 64-bit x86. The installer does not require administrator rights. It is currently unsigned.

1. Add PDF, DOCX, TXT or Markdown files. PDFs need readable text or an existing OCR layer.
2. Set cleanup options, output folder, speech provider, voice and speed on the main screen. Preview the selected voice with your own sample.
3. With a signed-in Codex CLI available, **Use Codex automatically** is selected by default. This improves the complete reading after local extraction. It uses your ChatGPT/Codex allowance and does not require an API key. Codex itself is not bundled.
4. Choose **Prepare reading** to review the text, or **Prepare + MP3** to continue into narration.
5. Without Codex, use **Copy prompt + reading**, or the saved `*_chatbot_request.txt`, in your preferred chatbot. Import its complete response and convert that text to MP3. Opening a chatbot never submits text automatically.

Local cleanup runs without a generative model or network calls. It removes selected headers, page numbers, footnotes, tables, captions, references and links, joins wrapped text, and conservatively preserves substantive content. Review the result and removal report: unusual layouts, poor OCR, complex phonetics and formulas can still need correction. Image-only PDFs need OCR beforehand. Embedded document instructions are treated as source data.

## Speech and voices

**Installed Windows voices** keeps narration text local. Compatible SAPI and Windows speech voices are listed; Narrator-only natural voices may not be available. **Microsoft online** uses edge-tts and sends narration text to Microsoft's service. Sonia is the default British female online voice; Susan/Hazel are preferred locally when installed. The unofficial online service may change or be unavailable; local mode never silently falls back to online.

**Install EN voices** installs all standard English TTS language capabilities available on the current Windows installation, with their basic-language dependencies. It requires internet, Windows administrator approval, and sometimes a restart. It does not install Narrator natural voices or change the display language. Cancelled or failed voice installation should be handled through Windows Settings. Preview is available for both online and installed voices.

## Saved files and revision

Each document has its own numbered output folder, normally in Documents/Loquor. The original document is preserved. Local listening text, a single prompt-plus-reading TXT, optional revision request and a detailed cleanup report are saved. Imported or Codex-improved text is saved separately. Repeated preparation and audio conversion use numbered filenames.

Optional exam revision produces a summary and a complete quiz: question, thinking pause, exemplar answer, repeated question. `[[PAUSE:15]]` on its own line becomes 15 seconds of actual silence. These markers are specific to Loquor. Review generated material; practice questions do not predict the real exam.

## Updates and privacy

Loquor checks the public release repository at startup unless disabled. This check sends no documents. It notifies you when a newer stable version is available. **Download and install** is user initiated, verifies GitHub's SHA-256 digest and starts the installer. Offline checks can be retried manually. Settings persist in LocalAppData/Loquor; documents and audio remain in your output folder during upgrades/uninstall.

Codex cleanup/revision sends source text to OpenAI only when enabled/requested. Online narration sends text to Microsoft. Local extraction and local speech stay on your computer. No sign-in credentials, personal readings or generated audio are distributed with this application.

## Source and builds

Source snapshots are provided alongside each public binary release even though the development Git repository is private. Loquor is licensed under GNU AGPL version 3 or later; see LICENSE and third-party notices. Classmates can use the installer without using the source.

For development, install Python 3.14 with tkinter, create a virtual environment, and run `python -m pip install -r requirements-build.txt`, then `python Loquor.pyw`. To build, use `Build_Release.ps1 -Compiler C:\path\to\ISCC.exe` with Inno Setup 7.1.0. `Publish_Release.ps1` publishes prepared artifacts using your existing GitHub CLI login. No secrets belong in this repository. Source packages and upstream build links are described in THIRD_PARTY_NOTICES.md and DEPENDENCIES.json.

Release tests cover all three original academic references locally (excluded from the repository), text handoff/import, one-screen controls, local English voice synthesis, online Sonia synthesis, cancellation, real silent quiz pauses, and a bundled-runtime smoke test. Full-length AI rewrites still deserve editorial review. A clean Windows virtual machine has not been tested.
