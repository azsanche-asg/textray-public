# Engineering evidence and its limits

Updated 30 October 2026. These are observed results from private qualification, not guarantees for every Mac or workload. The public repository shares the method and outcome; raw developer logs, private paths and test credentials are not published.

## Qualification baseline: private 1.0.0 (27)

Qualification ran on Apple silicon with macOS 26.6.2.

| Area | What was checked | Result / boundary |
| --- | --- | --- |
| Application regression suite | Editing, recovery, organization, search, Views, layouts, sync model, trial and installation cases | 909 tests passed, zero failures |
| Commercial service | SQLite, cryptography and local worker runtime with provider fixtures | 31 tests passed |
| Actual payment provider | Test-mode checkout, signed forwarded events, duplicates, altered payload rejection, two-device limit, transfer, recovery and refunds | Passed. No live charge; license emails captured locally |
| Missed webhook recovery | Separate empty ledger, actual Stripe event history, repeated reconciliation | Purchase and refund recovered without webhook delivery to that ledger |
| App distribution | Developer ID, notarization, stapling and Gatekeeper; installer launched from the mounted DMG | Passed on the qualified Mac |
| Actual updater | Signed build 26 to 27 replacement and relaunch | Two scratch tabs, Python mode, caret 7:9 and trial retained |
| Updater failures | Tampered feed, modified archive and interrupted download | Rejected before replacement |
| Production CloudKit probe | Two isolated stores on one Mac, bidirectional records, offline conflicts, history and duplicate delivery | Passed through Apple’s production service; not a fresh two-physical-Mac test |

The actual updater succeeded when the test app was launched through Finder. Earlier command-line launch attempts encountered macOS access problems and failed safely. Finder also opened the DMG successfully where the command-line mount attempt had been denied. Those failed attempts are not counted as successful installs.

## Public release: 1.0.0 (28)

The public build enables purchase routing and updates release/policy wording. The app, installer and disk image passed notarization and stapling; feed/archive signatures passed verification. Thirteen focused commerce/installation tests and 31 backend tests passed. Downloaded public installer and update files matched the qualified SHA-256 hashes. Native browser playback and seeking passed after adding bounded streaming byte-range responses for videos.

Production checkout and email delivery are still being qualified during the initial rollout; the purchase page remains closed. No live purchase has been made or claimed as part of these checks.

## Memory and larger libraries

The following earlier measurements exercise the retained-work architecture. They are labeled with their tested build; they are not rebranded as fresh 1.0 benchmarks.

| Workload | Build and measurement | Interpretation |
| --- | --- | --- |
| 500 distinct 256 KiB documents | 0.2 (25), standalone native registry/pane probe: metadata-only RSS about 35.2 MiB versus 33.2 MiB for one document; about 107.1 MiB after 500 visits, with five buffers retained | Inactive documents do not require all their text buffers to remain loaded. This excludes the full app and WebKit. |
| Repeated 500-document workload | 0.2 (12), 20 cycles and 10,000 native editor visits over about 865 seconds; post-purge RSS about 166 MiB | The bounded workload passed its steady-state growth gate. It was not a weeks-long soak. |
| Search at 10,000 files / about 100 MiB | Earlier search qualification, 12 warm samples: first result p95 13.7 ms; completion p95 669 ms; first scan 1.53 seconds | Engine measurements exclude typing debounce and UI painting. Load and warm-cache state materially affect timing. |

The search run also recorded a faster earlier repeat; the slower final measurement is shown here to avoid choosing only the best result. A universal sub-500 ms completion claim was not established. TextRay has not published a controlled head-to-head memory or speed comparison with TextMate or Zed.

## Failure recovery

Private qualification includes process termination around transaction boundaries, failed commits, permission failures, read-only external files, backup restoration into a populated destination and retention with pinned history. A 500-document / 121-checkpoint backup round trip preserved text and organization while retaining existing destination work.

This does not mean data loss is impossible. Independent backups, visible storage errors and explicit conflict handling remain part of the design. Saving locally and converging on another Mac are separate observations.

## Still outside these claims

- Intel and other macOS versions are not runtime-qualified by an Apple-silicon test, even though a universal binary and an older deployment target compile.
- The original two-Mac sync acceptance is separate from the current one-Mac/two-store probe. No new multi-week or two-Mac result is implied here.
- Production checkout and delivered recovery email remain outside the completed qualification until the rollout checks are recorded.

[Architecture](ARCHITECTURE_OVERVIEW.md) · [Distribution](PACKAGING_AND_DISTRIBUTION.md)
