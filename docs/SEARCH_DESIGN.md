# Deterministic search and live Views

Search should make its answer explainable: which text was searched, why it matched, and whether the result set is complete.

## One matching contract

Literal and Foundation/ICU regular-expression matching use the same rules across document, session, workspace, project and retained-library scopes. Case sensitivity and whole-word matching are explicit. Optional normalization and single-word typo tolerance are labeled; exact retrieval precedes approximate retrieval. There is no model-based semantic ranking.

Live unsaved text overrides its stored version. Project searches also account for locally retained unsaved changes to external originals. A document visible in several windows appears once in the result set. Results carry context and line/column positions, and navigation revalidates the target before selecting it.

## Acceleration must not decide correctness

The disposable SQLite index stores a small trigram Bloom filter per content hash, not another copy of the text. A verified ASCII literal of at least three bytes can reject a candidate when a required trigram is absent. Every remaining candidate still goes through the matcher. Unicode, short queries, regex and missing or suspect index entries take the scan path.

This intentionally permits false positives from the filter and verifies them afterward. The correctness requirement is that the filter must not hide a real match. Tests compare indexed results with an independent exhaustive scan, including corrupt/stale entries and same-size external edits.

The index has bounded entries and an approximately 96 MiB SQLite page ceiling. Evicting it affects speed, not retained documents. The design trades a compact metadata/filter pass for avoiding a second full-text corpus and a large postings index.

## Folder discovery and responsiveness

Bundled ripgrep handles file discovery and ignore rules. TextRay passes arguments directly to the helper; project search does not build a shell command. The shared Foundation matcher performs matching, keeping regex semantics consistent across scopes.

Search runs away from the main thread, debounces ordinary edits, delivers results incrementally and supports cancellation. Result limits and a per-document regex time budget are reported as incomplete work, rather than silently presenting an exhaustive answer. Filesystem events request reconciliation; an event stream alone is not proof that an index is current.

## What makes a View live

A View stores its query, options and scope identity. A fixed scope stays attached to a chosen session, workspace, document or project. A following scope resolves against the current context, which the interface names explicitly.

Visible Views refresh on relevant edits and changes. Hidden or closed Views release search work and snapshots, then refresh when reopened. They are not a permanent background scan of every project. Editing a View makes its unsaved settings visible; Save Copy creates another saved definition, and Revert to Saved View restores the original definition.

Replacement has a preview and revalidates its sources before applying. Changes to retained documents commit together, preserving native undo where an editor is loaded. An external original changes only when explicitly saved through the file-conflict barrier.

[Measured results and limits](QUALIFICATION.md) · [Use a View in a workflow](PRODUCT_WALKTHROUGH.md)
