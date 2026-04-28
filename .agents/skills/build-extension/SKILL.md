# Skill: build-extension

## Descrição

Builda, empacota e prepara a extensão para teste ou publicação.

## Comandos

### Desenvolvimento (com HMR)

```bash
npm run dev
```

Roda o Vite em modo watch. Útil para iterar no popup/options.

**Limitação:** content scripts e background requerem reload manual da extensão em `chrome://extensions/`.

### Build de produção

```bash
npm run build
```

Gera a pasta `dist/` pronta para carregar no Chrome.

### Gerar ZIP (Chrome Web Store)

```bash
npm run zip
```

Gera `dist-zip/extension-YYYYMMDD.zip` — esse é o arquivo que você sobe na Chrome Web Store.

## Estrutura do dist/

```
dist/
  popup.html
  options.html
  popup/popup.js
  popup/popup.css
  options/options.js
  background/background.js
  content/content.js
  manifest.json
  icons/
  _locales/
```

## Carregar no Chrome

1. Abra `chrome://extensions/`
2. Ative **Developer mode** (canto superior direito)
3. Clique **Load unpacked**
4. Selecione a pasta `dist/`
5. A extensão aparece na barra de ferramentas

## Reload após mudanças

- **Popup/Options:** feche e reabra
- **Content script:** recarregue a página (F5)
- **Background:** clique no ícone de refresh em `chrome://extensions/`

## Publicação

1. Crie uma conta em [Chrome Web Store Developer Dashboard](https://chrome.google.com/webstore/devconsole/)
2. Pague a taxa de registro ($5 uma vez)
3. Clique **New Item**
4. Faça upload do `.zip` gerado por `npm run zip`
5. Preencha descrição, screenshots, ícone
6. Envie para revisão
