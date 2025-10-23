
README do pacote de configuração ESLint do Blips

Descrição
---------

Este repositório contém a configuração compartilhada de ESLint utilizada pelo time de front-end do Blips. O objetivo é padronizar regras, plugins e ambientes de linting para todos os projetos do ecossistema Blips, garantindo qualidade de código consistente, melhores práticas e integração fácil com editores e pipelines de CI.

Principais características
- Fornece presets básicos e específicos (por exemplo: base, react, typescript).
- Integração com Prettier para evitar conflitos entre formatação e regras de lint.
- Conjunto de regras opinativas e regras configuráveis para acomodar diferentes projetos.

Como usar
---------

Instalação (exemplo via npm):

```bash
npm install --save-dev @blips/eslint-config
```

Exemplo mínimo de `.eslintrc.json` em um projeto consumidor:

```json
{
	"extends": ["@blips/eslint-config"]
}
```

Para projetos TypeScript ou React, estenda o preset correspondente:

```json
{
	"extends": ["@blips/eslint-config", "@blips/eslint-config/react", "@blips/eslint-config/typescript"]
}
```

Contribuindo
-----------

Contribuições são bem-vindas. Siga este fluxo ao propor mudanças:

1. Abra uma issue descrevendo a motivação para adicionar/alterar regras.
2. Crie um branch com alterações claras e justifique cada mudança no PR.
3. Adicione exemplos e, quando aplicável, casos de teste para regras customizadas.
4. Rode localmente o ESLint nos exemplos para verificar comportamento e autofix.

Benefícios
---------

- Consistência de estilo entre projetos do Blips.
- Redução de discussões sobre formatação em PRs.
- Detecção precoce de padrões de código problemáticos.

Contato
-------

Para dúvidas ou suporte, abra uma issue ou contate o time de front-end.
