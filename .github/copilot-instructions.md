## Repo Purpose
- Static playground for the `&lt;slot-it&gt;` custom element that manages a grid of `&lt;slot-cell&gt;` elements wrapping unnamed `&lt;slot&gt;` nodes.
- `project-rules.md` is the authoritative spec; keep this file and the README in sync with implementation.

## Tech & Conventions
- Vanilla JS only; no bundlers or frameworks. Compose DOM with minimal HTML strings and the provided helper.
- Implement and reuse `const createElement = (tag, props = {}) => Object.assign(document.createElement(tag), props);`.
- Default to ASCII in source files; match the repo's terse comment style and only add comments for non-obvious logic.
- Keep `index.html` small and ensure it links back to the Slot-it GitHub repo as required in the spec.

- Define `&lt;slot-it&gt;` as a standalone web component owning its template, styling, and keyboard listeners (arrows + numpad for 8-direction moves).
- Initialize a 3×3 grid of `&lt;slot-cell&gt;` custom elements with ids `cell_-1_-1` through `cell_1_1`, mapping to `[x,y]` coordinates as described in `project-rules.md`.
- Each `&lt;slot-cell&gt;` wraps an unnamed `&lt;slot&gt;` and tracks its position, current edge flags (`edge="N"`, etc.), and whether it hosts the user cursor.
- Movement stops at grid bounds; when the active cell hits an edge, dispatch logic to add the appropriate row/column without letting the user exit.

- On north edge entry, create a new row translated by `[0,-1]` and assign `edge="N"` to the new northern cells, clearing the old north flags.
- On east/south edge entry, append both a column to the east and a row to the south, with `[1,1]` translation.
- Mirror those insertions across the west and diagonal edges using `[-1,0]`, `[0,1]`, `[-1,1]`, `[1,-1]`, and `[-1,-1]` translations as called for by movement direction; shift edge flags to the new perimeter cells.
- Maintain consistent id patterns (`cell_${x}_${y}`) and update coordinates when inserting rows or columns to avoid duplicates.
- After structural updates, broadcast an `"update"` event from `&lt;slot-it&gt;` so every `&lt;slot-cell&gt;` can refresh state (edge flags, focus, local data).

## Events & State Flow
- Use custom `"update"` events exclusively for cross-cell communication; include payloads describing grid mutations and the active `[x,y]`.
- Each `&lt;slot-cell&gt;` listens for `"update"` to adjust its edge attribute, determine if it should render the user marker, and request new neighbors when necessary.
- Keep component state centralized in `&lt;slot-it&gt;` (current position, known bounds) and treat `&lt;slot-cell&gt;` instances as lightweight views.

## Developer Workflow
- Open `index.html` directly in a browser or via a static server; no build step exists.
- Use browser devtools to simulate keyboard events and verify grid expansion in all eight directions.
- Before commits, ensure the HTML output still references the GitHub repo and that newly generated cells respect the edge/coordinate rules.