

# Blips ESLint config

## O que inclui?

- Configuração base (standard);
- Plugin React;
- Plugin React Hooks;
- Plugin JSX a11y;
- Integração com Prettier;
- Preset para TypeScript;
- Preset para Node.js/Server quando aplicável.

## Setup

### React (com Next.js)

Instale as dependências:

```bash
npm i -D eslint @blips/eslint-config
```

Dentro do `.eslintrc.json` do projeto:

```json
{
	"extends": [
		"@blips/eslint-config/next",
		"next/core-web-vitals"
	]
}
```

### React (sem Next.js)

Instale as dependências:

```bash
npm i -D eslint @blips/eslint-config
```

Dentro do `.eslintrc.json` do projeto:

```json
{
	"extends": "@blips/eslint-config/react"
}
```

### Node.js

Instale as dependências:

```bash
npm i -D eslint @blips/eslint-config
```

Dentro do `.eslintrc.json` do projeto:

```json
{
	"extends": "@blips/eslint-config/node"
}
```

## Contribuindo

Contribuições são bem-vindas. Abra uma issue antes de grandes mudanças. Faça PRs com descrição das alterações, exemplos e, quando necessário, scripts de teste para validar regras.

## Contato

Para dúvidas, abra uma issue ou contate o time de front-end.
