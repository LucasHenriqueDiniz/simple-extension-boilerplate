# Skill: generate-store-assets

## Descrição

Gera todos os assets e textos necessários para publicar uma extensão na Chrome Web Store.

## O que precisa

Antes de publicar, você precisa de:

### 1. Descrição curta (máx 132 caracteres)

```
{{EXTENSION_NAME}} — {{DESC_CURTA}}
```

Exemplo:
> YouTube Ad Skipper — Skip ads automatically and enjoy uninterrupted videos.

### 2. Descrição completa

```
{{EXTENSION_NAME}} é uma extensão Chrome que {{O_QUE_FAZ}}.

✨ Principais recursos:
• {{FEATURE_1}}
• {{FEATURE_2}}
• {{FEATURE_3}}

🔒 Privacidade:
Esta extensão não coleta dados pessoais. Todas as configurações são armazenadas localmente no seu navegador.

📄 Permissões:
{{LISTAR_PERMISSOES_COM_EXPLICACAO}}

💬 Feedback:
Encontrou um bug ou tem uma sugestão? Entre em contato pelo GitHub.
```

### 3. Screenshots (obrigatório: 1-5 imagens)

- Tamanho: 1280x800 ou 640x400 (proporção 16:10)
- Formatos: JPEG ou PNG (sem alpha)
- Mostre o popup, options, ou a feature em ação

### 4. Ícone promocional (opcional)

- Pequeno: 440x280px
- Grande: 920x680px (recomendado)
- Marquee: 1400x560px

### 5. Vídeo promocional (opcional)

- YouTube URL, máx 30 segundos

### 6. Categoria

Escolha a mais adequada:
- Productivity
- Social & Communication
- Entertainment
- Developer Tools
- etc.

## Checklist antes de enviar

- [ ] Ícone 128x128 em `public/icons/icon.png`
- [ ] Screenshots em boa resolução
- [ ] Descrição curta ≤ 132 caracteres
- [ ] Descrição completa em inglês (obrigatório)
- [ ] Traduções de descrição para outros idiomas (opcional)
- [ ] Política de privacidade (URL) se coletar dados
- [ ] Website URL (opcional)
- [ ] Preço: Gratuito ou Pago
- [ ] Conta de desenvolvedor Chrome Web Store ($5)

## Comando para gerar ZIP

```bash
npm run zip
```

O arquivo gerado em `dist-zip/extension-YYYYMMDD.zip` é o que você sobe na loja.
