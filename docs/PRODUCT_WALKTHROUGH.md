# Product Walkthrough

This walkthrough describes the current TextRay private-alpha experience at a product level. It does not include private source code.

## First-Run Onboarding

On first launch, TextRay explains the local-first storage model, the TextRay folder, notes, drafts, metadata, and privacy assumptions. Onboarding is designed to make local storage transparent before the user starts writing.

## Writing A Draft

The app opens into a plain-text editor. When meaningful text is entered, TextRay autosaves it as a local draft. Empty launch state does not create unnecessary files.

## Saving As A Note

A draft can be promoted to a normal note. TextRay derives a practical filename from the title or first meaningful line and avoids overwriting existing notes by creating a unique filename when needed.

## Tabs

Tabs keep multiple contexts open: blank drafts, autosaved drafts, and saved notes. Closing a tab closes the workspace context; it does not delete the underlying local file.

Workspace metadata restores open tabs after relaunch when referenced files still exist.

## Palette

The palette provides keyboard-first navigation. It can show open tabs, recents, notes, actions, create-draft fallback items, and search results.

## Search

Search covers local notes and drafts. Results identify match quality: exact, punctuation-normalized, or typo-tolerant. Search is deterministic and does not infer synonyms or semantic similarity.

## Views

Views are live saved searches. They help organize writing by query while leaving notes as local files rather than moving them into opaque containers.

Suggested Views can surface repeated local search patterns when enabled.

## Settings

Settings include:

- General.
- Storage.
- Search.
- Views and Suggestions.
- Privacy/Data.
- Shortcuts/About.

Search and Suggested Views settings expose persistent controls. Storage and privacy surfaces explain local-first behavior and data boundaries.

## Storage And Privacy

TextRay shows where notes, drafts, metadata, and local trash live. Privacy/Data controls explain that there is no telemetry, no cloud sync, and no AI/semantic indexing.

## Help And Shortcuts

The Shortcuts/About surface documents key commands and product assumptions so users can orient quickly without leaving the app.
