# Architecture Overview

This document describes TextRay at a high level for portfolio review. It does not include private source code or proprietary implementation details.

## System Shape

```text
macOS SwiftUI app
  |
  +-- Editor and workspace UI
  +-- Palette and search UI
  +-- Settings, storage, privacy, help
  |
  +-- Workspace and tab coordination
  +-- Search and Views services
  +-- Storage and local data safety services
  |
  +-- User-owned text files
  +-- Local JSON metadata
  +-- Local trash, imports, backups
```

## Storage Layer

TextRay treats user files as the durable source of truth. Notes are user-visible text files, drafts are local text files, and metadata exists to restore workspace state, recents, search settings, Views, Suggested Views, onboarding state, and local usage signals.

Storage responsibilities include directory preparation, draft and note persistence, safe note promotion, local trash flows, backup/export, import of existing notes folders, metadata rebuilding, and atomic file writing.

## Workspace And Tabs

The workspace model keeps multiple writing contexts open at once. Tabs can represent blank drafts, autosaved drafts, or saved notes. Workspace metadata stores tab order, active tab identity, and document references so the app can restore open work after relaunch without embedding note content in metadata.

## Editor Coordinator

The editor coordinator keeps document operations tab-aware. Opening a note, selecting a recent item, activating a search result, or promoting a draft to a note preserves existing work and avoids duplicate tabs where possible.

Autosave writes local text files. Save-as-note creates a user-visible note from a draft while avoiding overwrite collisions.

## Palette And Search

The palette is the keyboard-first navigation layer. It surfaces open tabs, recents, notes, actions, create-draft flows, and search results.

Search is local and deterministic. The search service builds a local corpus from supported note and draft files, then ranks matches by explicit quality and field priority rather than semantic inference.

## Views And Suggested Views

Views are saved live searches. They organize documents by query rather than moving files into folders.

Suggested Views are derived from local-only usage signals. They are designed to make repeated searches easier without uploading behavior or building a remote profile.

## Settings And Privacy

Settings expose storage transparency, search behavior, Views and Suggested Views preferences, Privacy/Data controls, and Shortcuts/About information.

The privacy model is intentionally simple: no telemetry, no cloud sync, no AI/semantic indexing, and local files remain the source of truth.

## Performance Instrumentation

The private project includes benchmark coverage for search queries, corpus building, palette responsiveness, workspace restore, large-file behavior, and benchmark dataset generation. These tests keep local-first text workflows measurable as the app grows.

## Packaging And Distribution Tooling

TextRay uses a direct macOS distribution path for private-alpha preparation:

- Release build verification.
- DMG packaging.
- Developer ID signing setup and verification when a local signing identity is available.
- Read-only signing status inspection.
- Install and first-run guidance.

Notarization and stapling are future work and are not claimed as complete by this mirror.
