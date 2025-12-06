  # Sui Tasks

  End-to-end Web3 task management: Move smart contracts for projects, a TypeScript indexer for fast reads, and a Next.js dapp with Sui wallet support and
  a Kanban board UI.

  ## What’s Inside
  - `sui-tasks-engine`: Move package (`jira_engine`) with `username_registry` and `project` modules for on-chain project creation, membership, tasks,
  subtasks, attachments, and manager-cap authorization. **Deployed package ID:** `0x39d1dfff0845ababac9dd640a0dadf9565b0ee6ef6a7de8a488facfc279032de`
  (UsernameRegistry object: `0xb957b429336915c820567d1ddbec652a3a126946d522ceaf3fa6ac5335b738c6`; Clock: `0x6`).
  - `indexer/sui-task-indexer`: TypeScript/Prisma indexer + REST API that stores every event and maintains current state tables for projects, members,
  tasks, subtasks, and attachments.
  - `dapp`: Next.js 14 + Tailwind UI that connects to Sui Wallet, builds transactions (`lib/sui/transactions.ts`), and reads from the indexer for fast UX.
  - `ts-tests`: Jest integration tests and helpers for exercising the deployed Move package.

  ## Core Features
  - On-chain project lifecycle with member gating, task ownership, subtasks, and attachments; rich events for every change.
  - Username registry for human-readable identities.
  - Off-chain state mirroring for quick queries plus a full event audit trail.
  - Frontend with wallet connect, project creation, member management, and Kanban-style task updates.

  ## Quick Start
  1) **Contracts** (`sui-tasks-engine`): `sui move test`; publish with `sui client publish --gas-budget <budget>` if redeploying. Use the deployed package
  ID above (and UsernameRegistry object) in consumers.
  2) **Indexer** (`indexer/sui-task-indexer`): copy `.env.example` → `.env`, set `DATABASE_URL`, `PACKAGE_ID` (use the deployed ID), `NETWORK`; `npm
  install`; `npm run db:setup:dev`; `npm run indexer` (or `npm run start:all` to run API + indexer).
  3) **Dapp** (`dapp`): copy `.env.example` → `.env.local`, set `NEXT_PUBLIC_PACKAGE_ID` + `NEXT_PUBLIC_USERNAME_REGISTRY_ID` (values above) and
  `NEXT_PUBLIC_INDEXER_API_URL`; `npm install`; `npm run dev` and open `http://localhost:3000`.
  4) **Tests**: `sui move test` for on-chain logic; `cd ts-tests && npm test` for Jest contract interaction tests.

  ## Key Commands
  - Indexer DB studio: `npm run db:studio`
  - Indexer backfill from events: `npm run backfill`
  - Dapp build: `npm run build && npm start`

  ## Notes
  - Indexer REST routes include `/api/projects`, `/api/tasks?assignee=<addr>`, and event history endpoints.
  - Default network is testnet; override RPC via `NEXT_PUBLIC_SUI_RPC_URL` if needed.
