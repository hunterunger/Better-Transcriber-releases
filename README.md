# Better Transcriber — Releases

This public repository hosts the **Sparkle update feed** for
[Better Transcriber](https://github.com/hunterunger/Better-Transcriber) (private).

- **`appcast.xml`** — the Sparkle feed the app polls for updates. The app's
  `SUFeedURL` points at:
  `https://raw.githubusercontent.com/hunterunger/Better-Transcriber-releases/main/appcast.xml`
- **Release binaries** (`.zip` of the `.app`) are attached to this repo's
  [GitHub Releases](../../releases). The `appcast.xml` enclosure URLs point at
  those release assets.

## How updates are signed

Updates are signed with an **EdDSA** key. The private key lives in the
developer's macOS login keychain (created by Sparkle's `generate_keys`); the
public key is embedded in the app's Info.plist as `SUPublicEDKey`:

```
lwkq2mRa6dgkEwoMqCvI+nWh5EGwBKeCxT7OUohKeg0=
```

Sparkle verifies every downloaded update against this key, so only builds signed
with the matching private key will install.

## Cutting a release

From the **code** repo, run `scripts/release.sh <version>` (see that script for
details). It archives, signs, regenerates `appcast.xml`, creates a GitHub
Release here, uploads the `.zip`, and pushes the updated `appcast.xml`.

> Note: for users on other Macs, the build must be signed with a **Developer ID**
> certificate and **notarized**, or Gatekeeper will block it. Sparkle's EdDSA
> signature is separate from (and in addition to) Apple notarization.
