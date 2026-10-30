# Distribution and compatibility

TextRay is distributed directly through [textray.burritoslabs.com](https://textray.burritoslabs.com/). The website is the canonical source for downloads, tutorials and purchases. This repository does not distribute app binaries or act as an update feed.

## Release path

- A Developer ID signed, hardened-runtime application and guided installer.
- Apple notarization and stapling, with Gatekeeper verification.
- A DMG whose installer lets you choose a destination without moving or resetting your library.
- Sparkle updates with signed feeds and signed archives, checked before extraction.
- Explicit 30-day trial start and signed, device-bound licenses that work offline after activation.

The public release is **1.0.0 (28)**, signed, notarized and stapled with purchases enabled. Its preceding private 1.0.0 (27) candidate passed actual installation from the mounted image and an actual signed update/relaunch. See [qualification](QUALIFICATION.md) for the exact scope and caveats.

## Compatibility

The release supports **Apple silicon, macOS Tahoe 26.6.2 or later in the Tahoe 26 release line**. Runtime qualification was performed on 26.6.2. The binary includes an Intel slice and an older macOS deployment target, but compilation alone does not establish supported runtime behavior. The download page and update feed enforce the advertised compatibility requirements.

## Offer and ownership

The price is **€39.99 including applicable taxes, once for TextRay 1.x on two personal Macs**. The full trial lasts **30 days**, with no card or account required to start. Released 1.x updates are included; future major upgrades are optional. iCloud sync and Views do not carry a separate TextRay charge. Apple’s iCloud account and storage requirements still apply.

Expiry of the trial keeps retained work available for reading, copying, saving, export and recovery. It does not delete drafts or interrupt an already accepted write.

Activation, recovery and device transfer use a product-specific service. The app verifies signed receipts locally; trial timing and device proof live in Keychain rather than in the synced text library. Normal reinstallation does not restart a trial.

The signed trial and purchase checkout are public. Production checks verified the live account, inclusive EUR39.99 price, Managed Payments checkout, cancellation route, scheduled event reconciliation and delivery from the production email sender.
