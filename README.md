# @blips/eslint-config

> Configuração ESLint padrão da Blips para projetos React e Next.js

## � Pacote Público

Este é um pacote público mantido pela **Blips** e disponível para toda a comunidade no NPM.

## O que inclui?

- Configuração base ESLint v9+ (Flat Config);
- Plugin React com suporte a JSX;
- Plugin React Hooks;
- Integração com Prettier;
- Preset para TypeScript (via typescript-eslint);
- Plugin Next.js (quando aplicável);
- Ordenação automática de imports (simple-import-sort).

## 📦 Instalação

Instale o pacote como dependência de desenvolvimento:

```bash
npm install @blips/eslint-config --save-dev
# ou
pnpm add @blips/eslint-config -D
# ou
yarn add @blips/eslint-config -D
```

## Setup

> **⚠️ Importante**: Este pacote usa o formato **Flat Config** do ESLint v9+. Certifique-se de ter ESLint v9 ou superior instalado.

### React (com Next.js)

Instale as dependências:

```bash
npm i -D eslint@^9.0.0 typescript @blips/eslint-config
# ou
pnpm add -D eslint@^9.0.0 typescript @blips/eslint-config
# ou
yarn add -D eslint@^9.0.0 typescript @blips/eslint-config
```

Crie um arquivo `eslint.config.js` na raiz do projeto:

```javascript
import { config as nextConfig } from "@blips/eslint-config/next";

export default nextConfig;
```

### React (sem Next.js)

Instale as dependências:

```bash
npm i -D eslint@^9.0.0 typescript @blips/eslint-config
# ou
pnpm add -D eslint@^9.0.0 typescript @blips/eslint-config
# ou
yarn add -D eslint@^9.0.0 typescript @blips/eslint-config
```

Crie um arquivo `eslint.config.js` na raiz do projeto:

```javascript
import { config as reactConfig } from "@blips/eslint-config/react";

export default reactConfig;
```

### Configuração Base (TypeScript)

Para projetos que não usam React/Next.js:

```bash
npm i -D eslint@^9.0.0 typescript @blips/eslint-config
# ou
pnpm add -D eslint@^9.0.0 typescript @blips/eslint-config
# ou
yarn add -D eslint@^9.0.0 typescript @blips/eslint-config
```

Crie um arquivo `eslint.config.js` na raiz do projeto:

```javascript
import { config as baseConfig } from "@blips/eslint-config/base";

export default baseConfig;
```

## 🔧 Customização

Você pode estender a configuração base adicionando suas próprias regras:

```javascript
import { config as nextConfig } from "@blips/eslint-config/next";

export default [
  ...nextConfig,
  {
    rules: {
      // Suas regras customizadas aqui
      "no-console": "warn",
    },
  },
];
```

## 📝 Scripts Recomendados

Adicione ao seu `package.json`:

```json
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint . --fix"
  }
}
```

## Contribuindo

Contribuições são bem-vindas. Abra uma issue antes de grandes mudanças. Faça PRs com descrição das alterações, exemplos e, quando necessário, scripts de teste para validar regras.

Para instruções sobre como publicar novas versões deste pacote, consulte [PUBLISHING.md](./PUBLISHING.md).

## Contato

Para dúvidas, abra uma issue ou contate o time de front-end.
