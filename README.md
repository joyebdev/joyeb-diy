# joyebdiy

Open-source AI coding workspace for building, running, and deploying full-stack apps from your browser or desktop.

![joyebdiy social preview](./public/social_preview_index.jpg)

joyebdiy is the community-driven open-source version inspired by Joyebdiy. It combines chat-driven coding, live WebContainer execution, multi-provider LLM support, git workflows, and one-click deployment integrations.

## What This Project Does

- Generates and edits full-stack Node.js applications with AI assistance.
- Streams model responses and applies code changes directly in a project workbench.
- Runs code in-browser via WebContainer with terminal and live preview.
- Supports git import/push workflows (GitHub and GitLab routes included).
- Supports deployment integrations for Vercel and Netlify from inside the app.
- Ships as both a web app and an Electron desktop app.

## Core Features

- 19+ LLM providers (cloud + local), including OpenAI, Anthropic, Gemini, Ollama, OpenRouter, LM Studio, Mistral, Groq, DeepSeek, Cohere, Together, xAI, Moonshot, Fireworks, Cerebras, Perplexity, GitHub Models, AWS Bedrock, and OpenAI-compatible endpoints.
- Multi-chat workflow with project snapshots and persistence.
- Integrated code editor (CodeMirror), file tree, diff view, and file-locking controls.
- Integrated terminal/preview panel powered by WebContainer.
- MCP (Model Context Protocol) support.
- Supabase integration routes for project/query workflows.
- Desktop packaging and updates through Electron.

## Tech Stack

- Framework: Remix + React 18
- Build: Vite 5
- Runtime target: Cloudflare Pages / Workers compatibility
- Styling: UnoCSS + SCSS
- State: Nanostores + Zustand
- AI SDK: Vercel AI SDK and provider adapters
- Desktop: Electron + electron-builder
- Testing: Vitest
- Linting/formatting: ESLint + Prettier

## Repository Structure

```text
app/
  components/      UI by feature area (chat, editor, deploy, git, settings)
  lib/             Core modules (LLM manager, services, persistence, stores)
  routes/          Remix routes + API endpoints
  styles/          SCSS and UI styles
  types/           App-level TypeScript types

electron/
  main/            Electron main process build config and entry
  preload/         Secure bridge scripts

functions/
  [[path]].ts      Cloudflare Pages function catch-all

scripts/           Dev/build utility scripts
docs/              MkDocs-based documentation site
```

## Prerequisites

- Node.js 18.18.0+
- pnpm 9.14.4+
- Git

## Quick Start

```bash
pnpm install
cp .env.example .env.local
pnpm dev
```

Open: `http://localhost:5173`

## Environment Configuration

Copy `.env.example` to `.env.local` and set only the keys you need.

Common groups:

- AI provider keys: `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, `GOOGLE_GENERATIVE_AI_API_KEY`, `GROQ_API_KEY`, etc.
- Local model endpoints: `OLLAMA_API_BASE_URL`, `LMSTUDIO_API_BASE_URL`, `OPENAI_LIKE_API_BASE_URL`, `OPENAI_LIKE_API_KEY`
- Git integrations: `VITE_GITHUB_ACCESS_TOKEN`, `VITE_GITLAB_ACCESS_TOKEN`
- Deploy integrations: `VITE_VERCEL_ACCESS_TOKEN`, `VITE_NETLIFY_ACCESS_TOKEN`
- Supabase: `VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`, `VITE_SUPABASE_ACCESS_TOKEN`
- Runtime controls: `PORT`, `VITE_LOG_LEVEL`, `DEFAULT_NUM_CTX`

Notes:

- For Ollama and LM Studio, prefer `127.0.0.1` over `localhost`.
- Restart the dev server after changing env values.

## Development Commands

### Local Dev

```bash
pnpm dev
pnpm preview
pnpm typecheck
pnpm lint
pnpm lint:fix
pnpm test
pnpm test:watch
pnpm clean
```

### Build and Deploy

```bash
pnpm build
pnpm deploy
```

### Docker

```bash
pnpm dockerbuild
pnpm dockerbuild:prod
pnpm dockerrun
```

### Electron

```bash
pnpm electron:dev
pnpm electron:dev:inspect

pnpm electron:build:win
pnpm electron:build:mac
pnpm electron:build:linux
pnpm electron:build:dist
```

## API Surface (High-Level)

The app exposes many Remix API routes under `app/routes`.

Major groups:

- Chat and model routes: `api.chat.ts`, `api.llmcall.ts`, `api.models.ts`, `api.models.$provider.ts`
- Provider/config routes: `api.configured-providers.ts`, `api.check-env-key.ts`, `api.export-api-keys.ts`
- Git/GitHub/GitLab routes: `api.git-proxy.$.ts`, `api.github-*.ts`, `api.gitlab-*.ts`, `api.git-info.ts`
- Deployment routes: `api.vercel-deploy.ts`, `api.netlify-deploy.ts`
- Supabase routes: `api.supabase.ts`, `api.supabase.query.ts`, `api.supabase.variables.ts`
- System routes: `api.health.ts`, `api.system.diagnostics.ts`, `api.system.disk-info.ts`, `api.system.git-info.ts`
- MCP routes: `api.mcp-check.ts`, `api.mcp-update-config.ts`

## Deployment Options

- Cloudflare Pages (primary web target)
- Electron desktop builds (Windows/macOS/Linux)
- In-app deployment integrations for Vercel and Netlify
- Git-based workflows for GitHub/GitLab repositories

## Troubleshooting

- If chat requests fail, inspect terminal logs and browser DevTools console.
- If a local model does not connect, verify endpoint URL and that the model server is running.
- If preview is blank, inspect app runtime errors in browser console and terminal output.
- If Wrangler fails on Windows, ensure Visual C++ build/runtime prerequisites are installed.

See also:

- `FAQ.md`
- `CONTRIBUTING.md`
- `PROJECT.md`
- `docs/README.md`

## Contributing

1. Fork and create a feature branch.
2. Make focused changes.
3. Run `pnpm lint`, `pnpm typecheck`, and `pnpm test`.
4. Open a PR with a clear summary.

## License

MIT (see `LICENSE`).
