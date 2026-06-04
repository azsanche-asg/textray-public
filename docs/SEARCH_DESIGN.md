# Search Design

TextRay search is local, deterministic, and non-semantic.

The goal is to help writers find exact text, mechanical variants, and small typos without guessing meaning or sending queries away from the Mac.

## Match Qualities

### Exact Search

Exact search finds literal text with predictable case-insensitive matching. A query like `project alpha` matches text containing that phrase.

### Punctuation-Normalized Search

Punctuation-normalized search treats mechanical separators consistently. This helps when a writer remembers the words but not the punctuation.

Examples:

- `project alpha` can match `project-alpha`.
- `project-alpha` can match `project alpha`.
- `project_alpha`, `project.alpha`, and `project/alpha` can be compared as the same mechanical phrase.

### Typo-Tolerant Search

Typo-tolerant search catches small mechanical mistakes while staying conservative.

Example:

- `funtion` can match `function`.

Short, noisy, or semantically different queries are rejected rather than guessed.

## No Semantic Search

TextRay does not infer meaning:

- `car` does not mean `automobile`.
- `doctor` does not mean `physician`.
- `function` does not mean `method`.

That constraint is intentional. TextRay is a deterministic text workspace, not an AI notes app.

## Ranking

Ranking is fixed and explainable. Results are ordered by match quality and where the match appears, with stable tie-breakers.

The search pipeline favors:

- Exact matches before normalized matches.
- Normalized matches before typo-tolerant matches.
- Title matches before filename matches.
- Filename matches before first-line matches.
- First-line matches before body-content matches.

## Privacy

Search runs locally over local notes and drafts. TextRay does not upload queries, build remote indexes, or call AI services.
