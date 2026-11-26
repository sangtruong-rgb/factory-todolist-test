# CLAUDE.md

A small todo list web app: one page where a person keeps their tasks in the browser (no server, no sign-in). It is also a test of the Factory pipeline. The product is in `.factory/product.md`, the look in `DESIGN.md` (tokens in `.factory/design/tokens.json`, wired in `src/tokens.css`), decisions in `.factory/decisions.md`, the stack in `docs/adr/0001-stack.md`, and the coding rules in `CODING_STANDARDS.md`. Each issue's prototype is on its branch `prototype/issue-<n>` and is copied to `docs/prototypes/issue-<n>/` by the run that builds it.

## Run

- Install: `pnpm install`
- Run locally: `pnpm dev` (http://localhost:5173), or `pnpm start --port <port>` on a chosen free port. No environment variables (`.env.example` says so).
- Preview: none.

## Checks

Each exits non-zero on failure; CI (`.github/workflows/ci.yml`) runs the same commands.

- Tests: `pnpm test` (Vitest, jsdom, Testing Library); one file: `pnpm exec vitest run <file>`
- Types: `pnpm typecheck`
- Lint: `pnpm lint` (oxlint, warnings fail)
- Format: `pnpm format` (Prettier; `pnpm format:write` fixes)
- Build: `pnpm build`

## Layout

- `src/main.tsx`: entry; imports `tokens.css` and `index.css`.
- `src/App.tsx`: the app shell, the Tasks page.
- `src/tokens.css`: design tokens as CSS variables, light and dark.
- `src/test/setup.ts`: Testing Library matchers for Vitest.
- `docs/adr/`: decisions about the stack. `docs/prototypes/`: approved prototypes, never edited, excluded from lint and format.

## Patterns

- A component: a function component in `src/` with `<Name>.test.tsx` next to it; copy the shape of `src/App.tsx` and `src/App.test.tsx`.
- Styles: plain CSS using the tokens (`var(--accent)`); no CSS-in-JS, no UI library.
- State: React state in the component that owns it; tasks are read from and written to `localStorage` through one small module, so the rest of the code never touches storage directly.
- Tests use `@testing-library/user-event` for clicks and typing, and query by role, label or text.

## Project defaults

Settled for every ticket; a ticket says otherwise only on purpose.

- Lists: no paging; newest first unless a ticket says otherwise; an empty list shows one muted sentence saying what to do.
- Dates and numbers: dates as day and short English month ("28 Nov"), with the year when it is not the current year ("5 Jan 2027"); the device's local time zone; whole numbers as digits.
- Errors: shown inline in the danger colour directly under the field, `role="alert"`, worded as what to do; nothing is logged.
- Forms: validated on submit; an error message goes away when the input becomes valid; a refused field keeps the focus.
- Deletion: hard delete, at once, no confirmation and no undo.
- Names: English, camelCase for code, PascalCase for components; UI text in English, sentence case.
- Access: none; there are no accounts.
