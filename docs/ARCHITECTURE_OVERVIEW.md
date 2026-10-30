# Architecture

TextRay separates the text you own, the places you view it, and the arrangements that help you return to it. This keeps immediate capture simple while allowing several ways to organize the same work.

## The model

| Concept | What it stores | What it does not imply |
| --- | --- | --- |
| Document | A stable identity, retained text/revisions, language and optional external-file reference | A filename is not required. |
| Window or tab | A view of a document and its local editing/presentation state | Two views of one document are not independent copies. |
| Session | A resumable working context and document/window arrangement; automatic run/day history and named or nested sessions are supported | Closing a session does not discard its text. |
| Workspace | Virtual links to user-chosen windows and individual tabs; membership may overlap | A workspace does not own a folder or force a tiled layout. |
| Project | A registered folder, browsed and searched in place | Registering it does not import every file into a session. |
| View | A saved deterministic query, options and an explicit fixed or following scope | Results are references to matching work, not copied text. |

## From keystroke to retained work

The native editor updates a shared document buffer. A recovery coordinator batches persistence work; the store commits content, revision ancestry, document metadata and its sync outbox together. Saving an ordinary file is a separate, explicit operation with external-change checks. A document can therefore be safely retained in TextRay while its original file still has unsaved changes.

The recovery store uses one serialized SQLite writer, rollback journaling, full synchronization and macOS fullfsync. Immutable, hash-verified 64 KiB chunks use LZFSE compression; unchanged chunks are shared between revisions. Window arrangements, session/workspace membership, View definitions and checkpoint references are metadata in the library.

This is a durability design, not a claim that every keystroke is already on disk. Status distinguishes pending work, stored recovery content and file state. Failed commits stay visible and prevent an unsafe close or eviction.

## Many retained documents, few resident buffers

Restoration loads document identities and presentation metadata first. Text loads when needed, and multiple views of a document share one buffer. A window reuses its native editor when switching tabs.

Visible editors and active operations retain their necessary buffers. A small recent cache allows up to four additional buffers within a 16 MiB estimated budget; memory pressure drops that cache. Eviction must first finish durable storage. Hidden/minimized views detach when no longer needed, and inactive Markdown previews release WebKit resources.

The cache budget is **not** a whole-app RAM ceiling. Visible large files, simultaneous windows, undo and previews still cost memory. Eviction releases the buffer’s in-memory undo state; retained history and named checkpoints provide recovery beyond that lifetime. [Qualification](QUALIFICATION.md) distinguishes component probes from whole-app observations.

## History and restoration

Automatic revisions support recovery and retention; named checkpoints preserve intentional milestones. Restoring earlier text creates a separate document so current work remains available. Backup import adds recovered identities without silently replacing unrelated work.

Closing a window removes that window from the arrangement; Recently Closed can restore it and its membership. Closing a session retains the session’s arrangement for resumption. Retention settings govern how much history remains, so recovery is not a promise of unlimited history. Keep independent backups of important work.

## Sync without sharing a live database

Opt-in CloudKit sync exchanges application records and content through the user’s private iCloud database. The live SQLite file is never treated as a shared cloud file. Revision ancestry, idempotent application, durable outgoing work and explicit conflicts support offline editing and reconnection.

Text and portable organization can travel between Macs. Screen geometry, reading layout and local file access remain device concerns. Syncing a document reference does not give another Mac access to an arbitrary external folder.

## Main boundaries

```text
Native windows and editor
          |
Shared document registry ---- Search and live Views
          |                            |
Recovery coordinator           Disposable candidate index
          |
Transactional local library ---- Backup and history
          |
Durable sync outbox
          |
Optional private CloudKit database

Explicit Save -> chosen external file
Licensing and updates -> separate services, no working text
```

[Technology stack](TECH_STACK.md) · [Search design](SEARCH_DESIGN.md) · [Privacy](PRIVACY_AND_LOCAL_FIRST.md)
