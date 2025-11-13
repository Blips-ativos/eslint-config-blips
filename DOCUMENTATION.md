# Documentação - @blips/eslint-config

## 📋 Sumário

- [Visão Geral](#visão-geral)
- [Por Que Este Pacote Existe](#por-que-este-pacote-existe)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Arquitetura e Estrutura](#arquitetura-e-estrutura)
- [Regras e Justificativas](#regras-e-justificativas)
- [Instalação e Uso](#instalação-e-uso)
- [Migração de Projetos Legados](#migração-de-projetos-legados)
- [Manutenção e Evolução](#manutenção-e-evolução)

---

## Visão Geral

O `@blips/eslint-config` é um pacote público npm que centraliza e padroniza as configurações de linting e formatação de código para todos os projetos frontend da Blips. Ele fornece três presets configuráveis para diferentes contextos:

- **Base**: Para projetos TypeScript/JavaScript puros
- **React**: Para aplicações React
- **Next.js**: Para aplicações Next.js

### Objetivos Principais

1. **Consistência**: Garantir que todo código frontend siga os mesmos padrões
2. **Qualidade**: Detectar erros e más práticas automaticamente
3. **Produtividade**: Formatação automática e ordenação de imports
4. **Manutenibilidade**: Centralizar configurações em um único pacote versionado

---

## Por Que Este Pacote Existe

### Problemas Resolvidos

**Antes da Centralização:**
- Cada projeto tinha sua própria configuração de ESLint
- Inconsistências entre projetos dificultavam a mobilidade de desenvolvedores
- Atualização de regras requeria mudanças em múltiplos repositórios
- Novos projetos começavam com configurações desatualizadas ou incompletas

**Depois da Centralização:**
- Uma única fonte de verdade para regras de linting
- Atualização centralizada: basta atualizar a versão do pacote
- Onboarding simplificado para novos desenvolvedores
- Garantia de que todos os projetos seguem as mesmas convenções

### Decisão de Migração para ESLint v9+

Em 2024, o ESLint lançou a versão 9 com o novo formato **Flat Config** (`.eslintrc.json` → `eslint.config.js`), trazendo:

- **Simplicidade**: Configuração em JavaScript puro, sem JSON complexo
- **Composição**: Configs são arrays que podem ser facilmente combinados
- **Tipagem**: Melhor suporte para TypeScript e autocomplete
- **Futuro**: Formato recomendado pelo ESLint (formato antigo será descontinuado)

**Decisão da Blips**: Adotar o Flat Config desde o início, evitando migração futura e alinhando com as melhores práticas mais recentes.

---

## Tecnologias Utilizadas

### Core

| Tecnologia | Versão | Propósito |
|------------|--------|-----------|
| **ESLint** | ^9.38.0 | Motor principal de linting |
| **TypeScript ESLint** | ^8.14.0 | Suporte para TypeScript |
| **Prettier** | ^3.2.5 | Formatação de código |

### Plugins React

| Plugin | Propósito |
|--------|-----------|
| **eslint-plugin-react** | Regras específicas para React (JSX, hooks) |
| **eslint-plugin-react-hooks** | Validação das Rules of Hooks |
| **@next/eslint-plugin-next** | Otimizações e melhores práticas Next.js |

### Plugins Utilitários

| Plugin | Propósito |
|--------|-----------|
| **eslint-plugin-simple-import-sort** | Ordenação automática de imports |
| **eslint-config-prettier** | Desabilita regras conflitantes com Prettier |
| **eslint-plugin-prettier** | Integra Prettier como regra do ESLint |

### Por Que Estas Tecnologias?

**TypeScript ESLint**: Análise estática avançada, detecta erros de tipo em tempo de desenvolvimento.

**Prettier**: Elimina debates sobre formatação (tabs vs spaces, vírgulas, etc). O código é automaticamente formatado no save.

**Simple Import Sort**: Mantém imports organizados de forma consistente:
```typescript
// Ordem automática:
// 1. Imports externos (react, next, etc)
// 2. Imports internos absolutos (@/components)
// 3. Imports relativos (./Button, ../utils)
```

**React Hooks Plugin**: Previne bugs comuns como dependências faltando em `useEffect`, arrays de dependências incorretos, etc.

---

## Arquitetura e Estrutura

### Padrão de Composição em Camadas

```
┌─────────────────────────────────────────┐
│           next.js (Next.js)             │
│  • Todas as regras do base.js           │
│  • React + React Hooks                  │
│  • Next.js específico                   │
│  • Core Web Vitals                      │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│          react.js (React)               │
│  • Todas as regras do base.js           │
│  • React + React Hooks                  │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│         base.js (Base)                  │
│  • ESLint recomendado                   │
│  • TypeScript recomendado               │
│  • Prettier                             │
│  • Import sort                          │
└─────────────────────────────────────────┘
```

### Estrutura de Arquivos

```
@blips/eslint-config/
├── package.json          # Metadados, deps, exports
├── base.js              # Config base (TypeScript + Prettier)
├── react.js             # Config React (estende base)
├── next.js              # Config Next.js (estende base)
├── README.md            # Documentação de uso
├── PUBLISHING.md        # Guia de publicação
└── CLAUDE.md           # Guia para IA/desenvolvimento
```

### Exports do Package

```json
{
  "exports": {
    "./base": "./base.js",
    "./react": "./react.js",
    "./next": "./next.js"
  }
}
```

Isso permite importações específicas:
```javascript
import { config } from "@blips/eslint-config/next"
```

---

## Regras e Justificativas

### Regras Base (Todos os Projetos)

#### 1. ESLint Recommended (`js.configs.recommended`)

**O que faz**: Conjunto básico de regras para prevenir erros comuns em JavaScript.

**Exemplos de regras**:
- `no-unused-vars`: Detecta variáveis declaradas mas não usadas
- `no-undef`: Detecta uso de variáveis não declaradas
- `no-constant-condition`: Previne condições sempre verdadeiras/falsas

**Por quê**: Base sólida que previne bugs óbvios sem ser opinativa demais.

#### 2. TypeScript ESLint Recommended (`tseslint.configs.recommended`)

**O que faz**: Regras específicas para TypeScript.

**Exemplos de regras**:
- `@typescript-eslint/no-unused-vars`: Versão TypeScript-aware da regra
- `@typescript-eslint/no-inferrable-types`: Remove anotações de tipo redundantes
- `@typescript-eslint/ban-ts-comment`: Alerta sobre `@ts-ignore` sem justificativa

**Por quê**: TypeScript é usado em todos os projetos Blips. Estas regras garantem uso correto da linguagem.

**Exceção no Next.js**:
```javascript
"@typescript-eslint/no-explicit-any": "off"
```
Desabilitado no Next.js pois APIs do framework frequentemente usam `any` (como `getServerSideProps`).

#### 3. Simple Import Sort

**O que faz**: Ordena imports automaticamente.

**Formato aplicado**:
```typescript
// ✅ Correto (ordenado automaticamente)
import { useEffect, useState } from 'react'
import { NextPage } from 'next'

import { Button } from '@/components/Button'
import { api } from '@/services/api'

import { formatDate } from './utils'
import styles from './styles.module.css'

// ❌ Errado (desordenado)
import styles from './styles.module.css'
import { Button } from '@/components/Button'
import { useEffect } from 'react'
```

**Por quê**:
- Elimina debates sobre ordem de imports
- Facilita code review (mudanças de imports geram diffs limpos)
- Melhora legibilidade

#### 4. Prettier Integration

**O que faz**: Formata código automaticamente.

**Aspectos formatados**:
- Indentação (2 espaços)
- Aspas simples vs duplas
- Ponto e vírgula
- Largura máxima de linha
- Quebras de linha em objetos/arrays

**Por quê**:
- Zero configuração manual de formatação
- Código sempre consistente
- Economiza tempo em code review (não discute-se formatação)

### Regras React

#### 1. React Recommended (`pluginReact.configs.flat.recommended`)

**Exemplos de regras**:
- `react/jsx-uses-react`: Previne false positives de "React não usado"
- `react/jsx-key`: Força `key` em listas
- `react/no-danger`: Alerta sobre uso de `dangerouslySetInnerHTML`

**Por quê**: Previne bugs comuns em React.

#### 2. Desabilitação de `react/react-in-jsx-scope`

```javascript
"react/react-in-jsx-scope": "off"
```

**Por quê**: React 17+ introduziu o novo JSX Transform. Não é mais necessário importar React em todo arquivo:

```typescript
// ❌ React <17 (obrigatório)
import React from 'react'
export const Button = () => <button>Click</button>

// ✅ React 17+ (opcional)
export const Button = () => <button>Click</button>
```

#### 3. Desabilitação de `react/prop-types`

```javascript
"react/prop-types": "off"
```

**Por quê**: PropTypes é redundante em projetos TypeScript. A validação de tipos é feita pelo TypeScript:

```typescript
// TypeScript já valida os tipos
interface ButtonProps {
  label: string
  onClick: () => void
}

export const Button = ({ label, onClick }: ButtonProps) => {
  return <button onClick={onClick}>{label}</button>
}
```

#### 4. React Hooks Rules (`pluginReactHooks.configs.recommended`)

**Regras críticas**:
- `rules-of-hooks`: Hooks só podem ser chamados no top-level
- `exhaustive-deps`: Valida arrays de dependências

**Exemplo de erro detectado**:
```typescript
// ❌ ESLint vai alertar: missing dependency 'count'
useEffect(() => {
  console.log(count)
}, [])

// ✅ Correto
useEffect(() => {
  console.log(count)
}, [count])
```

**Por quê**: Hooks são fundamentais no React moderno. Violações destas regras causam bugs difíceis de debugar (stale closures, re-renders infinitos).

### Regras Next.js

#### 1. Next.js Recommended + Core Web Vitals

**O que faz**: Regras específicas do Next.js focadas em performance e SEO.

**Exemplos de regras**:
- `@next/next/no-img-element`: Força uso de `<Image>` ao invés de `<img>`
- `@next/next/no-html-link-for-pages`: Força uso de `<Link>` para navegação
- `@next/next/google-font-display`: Otimiza carregamento de Google Fonts

**Por quê**: Next.js tem otimizações específicas (Image optimization, prefetching, etc). Estas regras garantem uso correto.

**Exemplo prático**:
```typescript
// ❌ ESLint alerta: use next/image
<img src="/logo.png" alt="Logo" />

// ✅ Correto (otimização automática)
import Image from 'next/image'
<Image src="/logo.png" alt="Logo" width={200} height={50} />
```

**Benefícios do Image component**:
- Lazy loading automático
- Redimensionamento responsivo
- Conversão para WebP/AVIF
- Previne Cumulative Layout Shift (CLS)

#### 2. Prettier como Error (não warning)

```javascript
"prettier/prettier": "error"
```

**Por quê**: No Next.js, código mal formatado bloqueia o build. Isso força formatação correta antes do commit.

---

## Instalação e Uso

### Instalação em Novo Projeto

#### Next.js
```bash
npm i -D eslint@^9.0.0 typescript @blips/eslint-config
```

**eslint.config.js**:
```javascript
import { config as nextConfig } from "@blips/eslint-config/next";

export default nextConfig;
```

#### React (sem Next.js)
```bash
npm i -D eslint@^9.0.0 typescript @blips/eslint-config
```

**eslint.config.js**:
```javascript
import { config as reactConfig } from "@blips/eslint-config/react";

export default reactConfig;
```

#### Base (TypeScript puro)
```bash
npm i -D eslint@^9.0.0 typescript @blips/eslint-config
```

**eslint.config.js**:
```javascript
import { config as baseConfig } from "@blips/eslint-config/base";

export default baseConfig;
```

### Scripts Recomendados

**package.json**:
```json
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint . --fix"
  }
}
```

### Customização (quando necessário)

```javascript
import { config as nextConfig } from "@blips/eslint-config/next";

export default [
  ...nextConfig,
  {
    rules: {
      // Override apenas para casos específicos do projeto
      "no-console": "warn",
    },
  },
];
```

**⚠️ Importante**: Evite customizações. Se uma regra precisa ser mudada em múltiplos projetos, ela deve ser alterada no pacote central.

---

## Migração de Projetos Legados

### Desafio

Projetos antigos podem ter centenas de erros de ESLint. Corrigir tudo de uma vez é inviável.

### Solução: eslint-plugin-only-warn

**Instalação**:
```bash
npm i -D eslint-plugin-only-warn
```

**Configuração**:
```javascript
import { config as nextConfig } from "@blips/eslint-config/next";
import onlyWarn from "eslint-plugin-only-warn";

export default [
  ...nextConfig,
  {
    plugins: {
      onlyWarn,
    },
  },
];
```

**O que faz**: Converte todos os erros em warnings. O build não quebra, mas os problemas ficam visíveis.

**Processo de migração recomendado**:

1. **Dia 1**: Instalar o pacote com `only-warn`
   - Build continua funcionando
   - Equipe vê todos os warnings

2. **Semanas 2-4**: Corrigir warnings gradualmente
   - Priorizar arquivos mais editados
   - Corrigir em PRs normais (não dedicar sprint inteira)

3. **Após correções**: Remover `only-warn`
   - Agora erros bloqueiam o build
   - Código novo já nasce correto

### Tipos Comuns de Erros em Projetos Legados

| Erro | Frequência | Correção |
|------|------------|----------|
| `react-hooks/exhaustive-deps` | ⭐⭐⭐⭐⭐ | Adicionar deps ou usar `useCallback` |
| `@typescript-eslint/no-unused-vars` | ⭐⭐⭐⭐ | Remover variáveis não usadas |
| `simple-import-sort/imports` | ⭐⭐⭐⭐⭐ | Usar `eslint --fix` (auto-corrige) |
| `@next/next/no-img-element` | ⭐⭐⭐ | Substituir por `next/image` |

---

## Manutenção e Evolução

### Quando Atualizar o Pacote

**Cenários que exigem nova versão**:

1. **Nova regra aplicável a todos os projetos**
   - Exemplo: Detectar uso de APIs deprecated do React 19

2. **Atualização de dependências**
   - Exemplo: ESLint 9.38 → 9.40 com bugfixes

3. **Mudança em regras existentes**
   - Exemplo: Tornar `no-console` um error ao invés de warning

4. **Suporte a novo framework**
   - Exemplo: Adicionar preset para Remix ou Astro

### Versionamento Semântico

```bash
# Bugfixes (1.0.0 → 1.0.1)
npm version patch

# Nova funcionalidade (1.0.0 → 1.1.0)
# Exemplo: Adicionar novo preset
npm version minor

# Breaking change (1.0.0 → 2.0.0)
# Exemplo: Tornar regra warning em error
npm version major
```

### Processo de Publicação

```bash
# 1. Atualizar versão
npm version minor

# 2. Publicar
npm publish

# 3. Push com tags
git push && git push --tags
```

### Comunicação de Mudanças

**Mudanças minor**: Comunicar em canal de frontend no Slack.

**Mudanças major**:
1. Abrir issue no GitHub explicando breaking change
2. Comunicar com antecedência (1-2 sprints)
3. Fornecer guia de migração
4. Oferecer suporte durante adoção

### Responsabilidades

**Mantenedores do pacote**:
- Avaliar propostas de novas regras
- Testar mudanças em projeto real antes de publicar
- Manter documentação atualizada
- Responder issues/dúvidas

**Times de desenvolvimento**:
- Manter versão atualizada (pelo menos a cada 2-3 meses)
- Reportar regras problemáticas ou conflitos
- Sugerir melhorias baseadas em experiência real

---

## FAQ

### Por que não usar ESLint v8 com .eslintrc.json?

ESLint v8 e o formato antigo estão sendo descontinuados. Flat Config é o futuro e já é estável na v9.

### Posso desabilitar uma regra localmente?

Sim, para casos pontuais:
```typescript
// eslint-disable-next-line @typescript-eslint/no-explicit-any
const data: any = await fetchUnknownData()
```

Mas adicione um comentário justificando.

### E se meu editor (VS Code) não formatar automaticamente?

Instale a extensão ESLint e adicione ao `settings.json`:
```json
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```

### Como testar mudanças no pacote antes de publicar?

```bash
# No repo do eslint-config
npm link

# No projeto que vai testar
npm link @blips/eslint-config
```

### Posso usar em projetos pessoais?

Sim! O pacote é público e open source (MIT license).

---

## Conclusão

O `@blips/eslint-config` é mais do que um conjunto de regras - é um contrato entre todos os desenvolvedores frontend da Blips sobre como escrevemos código. Ele garante:

- ✅ Código consistente entre projetos
- ✅ Detecção precoce de bugs
- ✅ Onboarding rápido de novos devs
- ✅ Code reviews focados em lógica, não em formatação
- ✅ Atualização centralizada de melhores práticas

Ao adotar e manter este pacote atualizado, investimos na qualidade e manutenibilidade de todo o ecossistema frontend da Blips.
