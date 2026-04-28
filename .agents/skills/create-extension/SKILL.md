# Skill: create-extension

## Descrição

Cria uma nova extensão Chrome a partir deste boilerplate usando o CLI interno.

## Uso

### Modo não-interativo (recomendado)

```bash
npm run create-extension -- <nome> --description "..." --feature <nome-feature>
```

Flags disponíveis:
- `--description "texto"`
- `--version 1.0.0`
- `--feature nome-feature`
- `--no-popup` (remove popup)
- `--options` (adiciona options page)
- `--no-content` (remove content script)
- `--no-background` (remove background)

### Modo interativo

```bash
npm run create-extension
```

Responda as perguntas para configurar a extensão.

## Exemplo Completo

```bash
npm run create-extension -- youtube-ad-skipper \
  --description "Skip YouTube ads automatically" \
  --feature ad-skipper
```

## O que o CLI faz

1. Copia o boilerplate para uma nova pasta (kebab-case do nome)
2. Substitui placeholders:
   - Nome do projeto
   - Nome legível da extensão
   - Versão e descrição
3. Ajusta `manifest.json` conforme surfaces selecionadas
4. Cria a feature inicial em `src/features/` se solicitado

## Pós-criação

Sempre oriente o usuário a:

```bash
cd <nome-da-extensao>
npm install
npm run build
```

E carregar `dist/` em `chrome://extensions/` (Developer mode → Load unpacked).
