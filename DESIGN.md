# DESIGN.md

> Approved by the owner on 2026-11-26. Brand: new, direction "Calm & spare". Mockups: the prototypes of issues #1 to #4 (branches `prototype/issue-<n>`), binding through each issue's criteria.

## Principles

- Calm: one accent colour (green), used for the one primary action and for the tick. Everything else is ink, muted grey and hairlines.
- A list, not cards: tasks are rows on hairline dividers, 52px tall; no shadows, no boxed cards.
- Said in words: a state is never colour alone ("Overdue, 25 Nov", not only red).
- Nothing moves: no animation or transition; only colours change on hover and focus.
- Every control is visible without hovering and reachable by keyboard.

## Tokens

Every colour and size in the code comes from these, by name. A literal value in a component is a bug.

| Token              | Light   | Dark    | Use                                             |
| ------------------ | ------- | ------- | ----------------------------------------------- |
| `--bg`             | #FAFAF7 | #151614 | Page background                                 |
| `--surface`        | #FFFFFF | #1D1E1C | Text fields                                     |
| `--ink`            | #1C1C1A | #ECEBE5 | Body text, titles                               |
| `--muted`          | #6B6B66 | #A3A29B | Secondary text, icons, done titles, placeholder |
| `--line`           | #E4E3DD | #2E2F2C | Hairlines, field borders                        |
| `--hover`          | #EFEEE9 | #262725 | Hover and pressed backgrounds                   |
| `--accent`         | #2F6F5E | #7DBFA9 | The primary button, the tick, focus ring        |
| `--accent-ink`     | #FFFFFF | #10241D | Text and tick on the accent                     |
| `--danger`         | #B4432E | #F08A70 | Error messages, overdue dates                   |
| `--radius-control` | 8px     |         | Fields and primary buttons                      |
| `--radius-small`   | 6px     |         | Icon buttons, filter buttons                    |
| `--row-height`     | 52px    |         | Minimum height of a task row                    |

Where the tokens live in code: `src/tokens.css` (from `.factory/design/tokens.json`).

## Type

The system sans (`-apple-system, BlinkMacSystemFont, "Segoe UI", system-ui, sans-serif`), no web fonts. Body 15px / 1.45, regular. Page title 28px / 1.2, semibold, letter-spacing -0.01em. Secondary controls and messages 14px. Dates 13px. Numbers (counts, dates) use tabular figures.

## Components

- **Primary button** ("Add", "Save"): accent background, accent-ink text, semibold, radius-control; 48px tall in the add form, 36px in a row. Hover: slightly brighter.
- **Ghost button** ("Cancel"): no background, muted text; hover: hover background, ink text.
- **Text field**: surface background, 1px line border, radius-control, 48px tall (36px in a row), 16px text; focus: accent border.
- **Checkbox**: a 22px circle with a 1.5px muted border; checked: filled accent with an accent-ink tick.
- **Icon button** (pencil, ×): 32px square, muted icon, radius-small; hover: hover background, ink icon. Always has an accessible name.
- **Filter buttons**: text buttons, 32px tall; the one in use has the hover background, ink text and semibold, and `aria-pressed="true"`.
- **Empty state**: one muted sentence in the list's place, saying what to do.
- **Error message**: 14px danger text directly under the field it concerns, `role="alert"`.

## Layout

One left-aligned column, at most 600px wide, centred; padding 56px 24px at the top and sides on desktop, 28px 16px at 520px and below. Breakpoints: 390 and 1440 are the widths every screen is checked at. The header holds the title (left) and the count (right); under it the add form; then the list; then the filter row.

## Motion

None. No animation, transition or scroll effect. Hover and focus change colours only.

## Accessibility

Text contrast at least 4.5:1 in both themes. Visible focus: a 2px accent outline. Icon-only buttons carry accessible names ("Delete <title>", "Edit <title>"). Targets at least 32px. Everything works with the keyboard: Enter submits, Escape cancels an edit.

## Voice

Short, plain, sentence case, no exclamation marks. Errors say what to do: "Type a task first.", "A task needs a title." Empty states invite the next step: "Nothing to do yet. Add your first task above."
