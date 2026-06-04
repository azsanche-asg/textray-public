# Privacy And Local-First Model

TextRay is designed as a local-first writing workspace. It does not require cloud storage, telemetry, AI indexing, or a remote account to function.

## Files As Source Of Truth

User notes and drafts are stored locally as text files. Metadata is secondary: it helps restore tabs, recents, preferences, Views, search usage signals, and onboarding state, but it does not replace the user's files.

If metadata becomes stale, the storage model is designed to preserve user files and rebuild or ignore invalid metadata rather than deleting notes or drafts.

## Local Metadata

TextRay stores local JSON metadata for:

- Workspace tabs.
- Recent documents.
- Search preferences.
- Views.
- Suggested Views preferences.
- Local search usage signals.
- Dismissed suggestions.
- Onboarding completion.

Metadata stays on the Mac and is not included in this public mirror or packaging artifacts.

## No Telemetry

TextRay does not include telemetry in the current design. It does not send usage events, document names, note content, search queries, or local metadata to a server.

## No Cloud Sync

TextRay does not provide built-in cloud sync in the current design. The user controls where local files live and can inspect the TextRay storage location directly.

## No AI Or Semantic Indexing

TextRay does not use AI search, semantic embeddings, remote indexing, or synonym matching. Search behavior is deterministic and explains match quality through exact, punctuation-normalized, or typo-tolerant matching.

## Local Search Usage Signals

Suggested Views can use local-only search usage signals to identify repeated searches. These signals are kept in local metadata and do not leave the machine.

## Privacy/Data Controls

The app includes Privacy/Data surfaces that explain what is stored locally and provide controls for local-first data management. Storage views also make notes, drafts, metadata, and local trash locations visible.

## Public Mirror Boundary

This public mirror excludes source code, app binaries, DMG/ZIP artifacts, user notes, drafts, `.textray` metadata, local trash, credentials, certificates, signing profiles, and private paths.
