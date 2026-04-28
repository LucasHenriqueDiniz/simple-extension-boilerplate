# Skill: add-feature

## Descrição

Adiciona uma nova feature a uma extensão existente.

## Estrutura de uma Feature

```
src/features/nome-da-feature/
├── index.ts      → Registra a feature no registry
└── content.ts    → (Opcional) Código que roda na página
```

## Passo a passo

### 1. Criar pasta e arquivo de registro

`src/features/nome-da-feature/index.ts`:

```ts
import { registerFeature } from '@core/feature-registry'
import { logger } from '@core/logger'

registerFeature({
  id: 'nome-da-feature',
  name: 'Nome Legível',
  description: 'O que esta feature faz',
  defaultEnabled: false,
  run: () => {
    logger.log('Feature está rodando')
    // Lógica que roda no background
  },
  cleanup: () => {
    logger.log('Feature está sendo desligada')
    // Limpeza (remove listeners, etc.)
  },
})
```

### 2. (Opcional) Criar content script

Se a feature precisa manipular o DOM:

`src/features/nome-da-feature/content.ts`:

```ts
import { logger } from '@core/logger'

export function initNomeDaFeature() {
  logger.log('Content script inicializado')
  // Seu código de DOM aqui
}
```

E em `src/content/index.ts`:

```ts
import { initNomeDaFeature } from '../features/nome-da-feature/content'
import { isFeatureEnabled } from '@core/feature-registry'

const run = async () => {
  const enabled = await isFeatureEnabled('nome-da-feature')
  if (enabled) {
    initNomeDaFeature()
  }
}

run()
```

### 3. Registrar no índice global

Em `src/features/index.ts`, adicionar:

```ts
import './nome-da-feature'
```

### 4. Testar

```bash
npm run build
```

A feature aparecerá automaticamente no popup com um toggle.

## Convenções

- `id`: `kebab-case`, único
- `name`: `Pascal Case` ou título legível
- `defaultEnabled`: `false` a menos que seja feature core
- Content scripts só rodam se `content/` importar e `isFeatureEnabled` for true
