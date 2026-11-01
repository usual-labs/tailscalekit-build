# tailscalekit-build

Ready-made builds of [TailscaleKit](https://github.com/tailscale/libtailscale/tree/main/swift),
Tailscale's Swift package for running a Tailscale node inside an app, as a zipped XCFramework that
Swift Package Manager can download. Tailscale publishes TailscaleKit as source only, and building
it needs Go. [Usual Bot](https://github.com/usual-labs/usual-bot) uses these builds on iPhone to
reach a gateway on your tailnet without the Tailscale VPN.

This is an unofficial build, not made by, affiliated with or endorsed by Tailscale Inc.
"Tailscale" is a trademark of Tailscale Inc.

## Using a release

Each [release](https://github.com/usual-labs/tailscalekit-build/releases) is named after the
libtailscale commit it was built from (`libtailscale-<commit>`) and gives the `binaryTarget` to put
in your `Package.swift`, with the zip's URL and checksum. The framework covers iPhone and the iOS
Simulator, not the Mac.

Each zip has a build attestation. To check that this repository's workflow built it:

```sh
gh attestation verify TailscaleKit.xcframework.zip -R usual-labs/tailscalekit-build
```

## Making a release

Run the **Build** workflow from the Actions tab with a full libtailscale commit SHA and the lowest
iOS version to support. Leave **Publish** off for a trial run: the zip and its release notes stay
on the run as an artifact for a week. With **Publish** on, the workflow attests the zip and
publishes the release. A commit can be released once; its tag is taken after that.

## License

The workflow and these docs are under the Apache License 2.0 ([LICENSE](LICENSE)). TailscaleKit is
Copyright (c) Tailscale Inc & AUTHORS, under the BSD 3-Clause license, which each zip includes.
