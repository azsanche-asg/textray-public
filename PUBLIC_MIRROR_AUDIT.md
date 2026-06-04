# Public Mirror Audit

This audit records the intended safety boundary for the TextRay public portfolio mirror.

## Inclusion Summary

- Documentation is included.
- Screenshots are included only when captured from neutral demo content.
- `assets/TextRay-logo.png` is included intentionally as a branding and portfolio display asset.
- The TextRay name, logo, and branding assets are not freely reusable unless later licensed by the owner.

## Exclusion Checklist

- [x] No source code included.
- [x] No Swift files included.
- [x] No Xcode project included.
- [x] No app binaries included.
- [x] No DMG artifacts included.
- [x] No ZIP artifacts included.
- [x] No signing certificates included.
- [x] No signing credentials included.
- [x] No signing profiles included.
- [x] No API keys included.
- [x] No local `.textray` metadata included.
- [x] No user notes or drafts included.
- [x] No local trash included.
- [x] No private local paths or usernames are intentionally included in documentation.
- [x] No Developer ID identity strings included.
- [x] No claim that TextRay source is publicly available.
- [x] No false open-source claim.
- [x] No false notarization claim.
- [x] No false stapling claim.
- [x] No public release claim.
- [x] No Mac App Store readiness claim.

## Distribution Claim Check

This mirror says:

- Direct DMG distribution is the current direction.
- Release builds and DMG packaging are verified in the private project.
- Developer ID signed-app DMG verification exists when an appropriate local signing identity is available.
- Notarization is not complete.
- Stapling is not complete.
- Public release is not complete.
- Mac App Store is not the current target.

## Screenshot Check

The current screenshot set was captured for portfolio display from a clean macOS TextRay session using neutral demo content. The screenshot set includes:

- First-run onboarding.
- Main editor with a neutral draft.
- Palette search for `project alpha`.
- Search settings.
- Privacy/Data settings.
- Storage settings cropped to avoid absolute local path rows.
- Shortcuts/About settings.
- DMG install Finder window.

Screenshots were visually checked during capture. They should still be manually reviewed before publishing. They should show only neutral demo content and must not expose:

- Real notes or drafts.
- Internal development notes.
- `.textray` metadata.
- Local usernames or private paths.
- Credentials or certificate details.
- Misleading release status.

Current screenshot safety confirmations:

- [x] No real user notes or drafts are intentionally shown.
- [x] No internal batch/development notes are intentionally shown.
- [x] No signing identities, certificates, or credentials are intentionally shown.
- [x] No private local paths or usernames are intentionally shown in the final screenshots; the Storage screenshot is cropped before absolute path rows.
- [x] Screenshots are safe to publish after the owner's final manual visual review.

## Final Checklist Before Pushing

- [ ] Run `find . -type f` from inside this public mirror and review the file list.
- [ ] Confirm no `.swift`, `.xcodeproj`, `.app`, `.dmg`, `.zip`, `.p8`, `.p12`, `.cer`, `.mobileprovision`, or `.textray` files are present.
- [ ] Open every screenshot and visually inspect for real data, private paths, local usernames, credentials, or misleading claims.
- [ ] Confirm `README.md` states the source code is private and not included.
- [ ] Confirm no app binary or package artifact was added.
- [ ] Confirm no license file was added unless the owner intentionally chooses one later.
