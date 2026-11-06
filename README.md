# AmooBuddy

Release APK for `AmooBuddy` phone automation, built with the defensive packaging chain.

```
stepx-amoo-bridge-release.apk   82,347,971 bytes   SHA-256 64e082fe6eab2cffa165d3563706f856540bd3ceedfca9026e4e44a53b52e55a
```

Signer SHA-256: `ab544b52a994651c6acc81c8e920d91824d959a1478d2b7bfa3fe50dc1855b54`

## Verifying the APK

```bash
apksigner verify --print-certs stepx-amoo-bridge-release.apk
```

The signer SHA-256 above must match what `apksigner` reports. Every other check in the
`phone_agent_bridge` README ("发布构建与防重打包自检") runs at runtime on the phone and
cannot be validated from this download page.

## Defensive chain (what this build does)

`TamperGuard` is release-only: every process starts it once and compares the installed
package signature against the build-time pin. When the running package is not the one built
here, the process reports `proven` - the `signature_mismatch`, `debuggable_release`, or
`tracer_attached` signals - and destroys:

+ the HTTP service token (private `files/bridge-token.txt`)
+ the wake credential (private files)
+ the shared mailbox artifacts, when the signing is a proven repack

The guard is inert for debug builds and for unsigned builds: a local adb install loop stays
safe. It does not delete user data, change a system setting, restart, or uninstall itself.
Confirmed signals on the phone can be recovered by the owner in Settings → 打包完整性.

## Installing

```bash
adb install stepx-amoo-bridge-release.apk
```

`adb install -r` replaces an existing debug or older release build. Install needs the
same signature as the one published here: `ab544b...` (full hash above).
