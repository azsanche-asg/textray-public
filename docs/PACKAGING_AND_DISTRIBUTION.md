# Packaging And Distribution

TextRay currently uses a DMG-first direct macOS distribution path for private-alpha preparation. This document describes status honestly for portfolio review.

## Release Build

The private project has Debug and Release build verification through Xcode. The public mirror does not include the Xcode project, source files, tests, built apps, or build products.

## DMG Packaging

The private project includes local packaging scripts that can create private-alpha artifacts under an ignored `dist/` directory. DMG is the preferred direct-distribution artifact. ZIP packaging exists as an internal fallback/check artifact.

The DMG package contains the app bundle and an Applications symlink. Package artifacts do not include user notes, drafts, `.textray` metadata, local trash, credentials, certificates, signing profiles, or local signing environment files.

## Developer ID Signing

The private project includes a Developer ID signing path for a copied app bundle when an appropriate local signing identity is available. It also includes read-only signing status inspection using standard macOS tools.

The mirror does not include signing identities, certificates, private keys, provisioning profiles, app-specific passwords, API keys, or Developer ID identity strings.

## Verification Tools

The private packaging/signing workflow uses standard macOS tooling where appropriate:

- `hdiutil` for DMG creation and mounting.
- `codesign` for app signature verification.
- `spctl` for Gatekeeper assessment.

## Notarization And Stapling Status

Notarization is not complete.

Stapling is not complete.

Gatekeeper warnings or blocks may still occur until notarization and stapling are completed.

## Install Guide Status

The private project includes private-alpha install and first-run guidance. That guidance is cautious: TextRay is not a public release, not a Mac App Store build, not notarized, and not stapled.

## Current Limitations

- Public release is not complete.
- The Mac App Store is not the current target.
- Notarization/stapling are future work.
- This public mirror is not a download channel.
- No app binaries, DMGs, ZIPs, or release artifacts are included here.
