# Publishing a release

The development repository stays private. Public releases include an optional Loquor source ZIP, installer, portable Windows ZIP and SHA-256 checksums.

1. Update `app_updates.VERSION` in the private source project and prepare `Loquor-source-VERSION.zip` with the application files, licences and build scripts. Exclude personal documents, generated audio, credentials, build output and Git internals.
2. Create a **draft** release tagged `vVERSION` in this repository and upload the source ZIP. Use the private project's `Publish_Release.ps1`, or GitHub's release editor.
3. In this repository's Actions page, run **Build Windows release** with that version. It downloads the source from the draft, installs dependencies on a GitHub Windows runner, runs tests, builds and checks the bundled app, compiles the installer, uploads binaries/checksums, and publishes only after success.

The workflow uses GitHub's short-lived repository token. No personal access token or access to the private source repository is required. Failed builds leave the release as a draft for repair. The public latest-release API drives Loquor's update notices.
