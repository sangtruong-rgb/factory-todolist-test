# ADR 0001: Vite, React and TypeScript, client-only

- Status: accepted (the owner, 2026-11-26)
- Source: `.factory/product.md` confirmed 2026-11-26; issues #1 to #4

## Context

One page, one user per browser, tasks kept in the browser's storage (#1 C6): no server, no sign-in, no database. Maintained by one person. It must start with one command and build to static files.

## Options

### Vite + React + TypeScript

- Pieces: React 19, TypeScript, Vite, Vitest with Testing Library and jsdom, oxlint (the starter's linter), Prettier, pnpm.
- Fits because: the most common setup for a small single-page app; components map onto the screens of the prototypes.
- Costs to run: static files, free on any static host.
- Maintained by: anyone who knows React.
- Main risk: more dependencies than a todo strictly needs.

### Vite + TypeScript, no framework

- Pieces: TypeScript and DOM code, Vitest with jsdom, oxlint, Prettier.
- Fits because: smallest bundle, nothing to learn.
- Costs to run: static files.
- Maintained by: anyone who knows TypeScript.
- Main risk: hand-rolled rendering grows uneven from one change to the next.

### Next.js + TypeScript

- Pieces: App Router with static export.
- Fits because: familiar.
- Costs to run: static files.
- Maintained by: anyone who knows Next.js.
- Main risk: server rendering and localStorage need care for a page that is client-only anyway.

## Decision

Vite + React + TypeScript, chosen by the owner: the best-known setup, with tests in Vitest and the starter's own linter.

## Consequences

Easy: test components with Testing Library, build static files, start with `pnpm dev`. Hard: anything server-side, which would need a new decision. Revisit if tasks must sync between devices.
