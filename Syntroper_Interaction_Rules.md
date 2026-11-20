# Syntroper diagrams · interaction rules

These rules are the same in every diagram: Galaxy, context maps (Levels 1–3), flowchart, sequence diagram and the context board.

| State | Look | When |
|---|---|---|
| Rest | Solid borders and lines in the base colours | Nothing is hovered or selected |
| Hover | Dashed outline in `--sel-hov`. Nothing else changes | Pointer over one element |
| Selected | Solid `--sel`, thicker line or 1px ring | One element clicked. Always a single element, never a group |
| Related | `--rel` | Elements directly connected to the selection (same step, same link) |
| Everything else | Reduced opacity | While something is selected |

Dashes at rest only mean "suggested" or "unresolved". Hover never adds a second colour or a glow on top of the dashed outline.

## Flowchart shapes

| Shape | Colour |
|---|---|
| Start and end (pill) | Green border |
| Step (rectangle) | Base border |
| Decision (diamond) | Yellow border |
| Other path | Solid border with a left edge in its kind: red for errors, yellow for validation, grey for cancel |

## Sequence diagram

The system level shows two lifelines only: the persona and the named system. The APIs behind a step show in the side card for the selected arrow, not as lifelines.

The bounded context and code levels add lifelines and break each step into more arrows.

Decisions sit on the system lifeline as a diamond, with the current value next to it. Picking another value from its dropdown redraws the steps below it.

## Impact on the context board

The Galaxy in the middle shows what a move affects:

| What | How it looks |
|---|---|
| Use cases and APIs that move | Purple, from their old context to the new one |
| Events their code fires | Red |
| Use cases and contexts that depend on the move | Red bars, joined by red dotted lines |
| Integration points that move with them | Grey dotted |

The right panel has two tabs: Summary, which has the short summary, the decisions and the refactoring plan, and Connected, which lists every affected node by layer.
