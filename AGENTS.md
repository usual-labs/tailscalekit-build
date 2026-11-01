# usual-labs/tailscalekit-build

Builds and publishes TailscaleKit.xcframework (iPhone and iOS Simulator) from a
tailscale/libtailscale commit; see README.md. Usual Bot's `Packages/Tailnet/Package.swift` points at
one release by URL and checksum. Nothing updates it automatically.

## Releasing a new TailscaleKit

1. Pick a libtailscale commit; check its `swift/` changes for API breaks against
   `usual-bot/Packages/Tailnet/Sources/Tailnet/Tailnet.swift`.
2. Run the Build workflow with Publish off first. Download the artifact and build Usual Bot for
   iPhone and the Simulator against the zip (`.binaryTarget(path:)` accepts the zip) before
   publishing.
3. Run it again with Publish on. Copy the `binaryTarget` from the release notes into usual-bot and
   build the app on a device.

## Gotchas

- TailscaleKit's Xcode project sets iOS 18.1; the workflow overrides it with
  `XCODE_XCCONFIG_FILE` so the framework matches the app's minimum (Usual Bot: 18.0).
- Zip with `ditto --norsrc --noextattr --noqtn --noacl`, or macOS adds `._` metadata files.
- libtailscale's go.mod may need a newer Go than the runner has; `GOTOOLCHAIN` (default `auto`)
  downloads it.
- The actions are pinned to full commit SHAs, the same pins as usual-bot; keep them in step.
