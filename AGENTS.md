# Chrome Extension Boilerplate — AGENTS.md

Contexto global para desenvolvimento de extensões Chrome com este boilerplate.

## Stack

- Vite (build tool)
- React 19 (popup/options UI)
- TypeScript
- Tailwind CSS
- Manifest V3

## Arquitetura

### Single Project (não é monorepo)

Tudo em `src/`:

```
src/
  background/     → service worker (MV3)
  content/        → content script (roda nas páginas web)
  popup/          → popup HTML + React
  options/        → options page HTML + React
  changelog/      → página de changelog/versões (opcional)
  core/           → utilitários compartilhados
    config.ts     → nome, versão, debug flag
    storage.ts    → wrapper chrome.storage.sync/local
    messaging.ts  → sendMessage/onMessage tipado
    logger.ts     → log com prefixo e níveis
    feature-registry.ts → sistema de features
  features/       → cada funcionalidade é um módulo isolado
  shared/         → hooks, UI components, utils
```

### Sistema de Features

Toda funcionalidade da extensão é uma **feature** registrada:

```ts
import { registerFeature } from '@core/feature-registry'

registerFeature({
  id: 'auto-skip',
  name: 'Auto Skip',
  description: '...',
  defaultEnabled: false,
  run: () => { ... },
  cleanup: () => { ... },
})
```

- Features aparecem automaticamente no popup com toggle on/off
- Estado persistido em `chrome.storage.sync`
- Background executa `runFeatures()` no startup
- Content scripts verificam `isFeatureEnabled(id)` antes de rodar

### Aliases

- `@core/*` → `src/core/*`
- `@shared/*` → `src/shared/*`

### Build

- `npm run dev` → desenvolvimento (Vite watch)
- `npm run build` → build de produção
- `npm run zip` → gera zip para Chrome Web Store

### Changelog

A página de changelog (`changelog.html`) é opcional. Quando habilitada:
- É acessível via link no popup
- Mostra histórico de versões com badges (Feature, Fix, Chore, Refactor)
- Usa as mesmas chaves i18n

O build usa múltiplos configs:
- `vite.config.ts` → popup + options (HTML pages)
- `vite.background.config.ts` → background (ES module, inline imports)
- `vite.content.config.ts` → content (IIFE, inline imports)

## Criar Nova Extensão

Use o CLI:

```bash
npm run create-extension -- nome-da-extensao --description "..." --feature minha-feature --changelog
```

Flags úteis:
- `--no-popup` — remove popup
- `--options` — adiciona options page
- `--no-content` — remove content script
- `--no-background` — remove background
- `--no-changelog` — remove página de changelog

Ou interativo:

```bash
npm run create-extension
```

O CLI gera uma cópia do boilerplate com placeholders substituídos.

## Adicionar Nova Feature

1. Criar pasta `src/features/nome-feature/`
2. Criar `index.ts` com `registerFeature({...})`
3. (Opcional) Criar `content.ts` para DOM manipulation
4. Importar em `src/features/index.ts`
5. Se tiver content script, importar e inicializar em `src/content/index.ts`

## Convenções

- Nomes: `kebab-case` para IDs, `PascalCase` para componentes
- Storage keys: `feature:${id}` para estado de features
- i18n: `_locales/en/messages.json` e `_locales/pt/messages.json`
- Logger: usa `logger.log/info/warn/error` (respeita `config.debug`)

## Permissões Comuns

- `storage` → já incluso por padrão
- `activeTab` + `scripting` → injetar scripts dinamicamente
- `tabs` → ler URLs das abas
- `host_permissions` → sites específicos (ex: `*://*.youtube.com/*`)

## Regras para OpenCode

- Sempre use as aliases `@core/*` e `@shared/*` em vez de paths relativos
- Sempre registre features via `registerFeature` — nunca crie código solto em background/content
- Sempre use `logger` em vez de `console.log` diretamente
- Sempre use `storage` wrapper em vez de `chrome.storage` diretamente
- Sempre use `t()` para strings visíveis ao usuário (i18n)
- Prefira criar features modulares em vez de acumular lógica em `background/` ou `content/`
- Quando criar uma nova extensão via CLI, sempre teste `npm run build` antes de dizer que está pronto
