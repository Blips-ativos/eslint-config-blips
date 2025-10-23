# 📦 Guia de Publicação - @blips/eslint-config

## Pré-requisitos

### 1. Criar uma Conta no NPM

Se você ainda não tem uma conta no NPM:

1. Acesse: https://www.npmjs.com/signup
2. Crie sua conta
3. Verifique seu email

### 2. Fazer Login no NPM

```bash
npm login
```

Será solicitado:
- **Username**: seu-usuario-npm
- **Password**: sua-senha
- **Email**: seu-email@example.com

## 🚀 Como Publicar o Pacote

### Primeira Publicação

```bash
# 1. Certifique-se de estar na branch main e atualizado
git checkout main
git pull

# 2. Faça login no NPM (se ainda não estiver logado)
npm login

# 3. Publique o pacote
npm publish --access public
```

**Nota**: O flag `--access public` é necessário para scoped packages (@blips/eslint-config) na primeira publicação.

### Publicações Subsequentes

```bash
# 1. Atualize a versão (escolha uma opção)
npm version patch  # 1.0.0 -> 1.0.1 (correções)
npm version minor  # 1.0.0 -> 1.1.0 (novas funcionalidades)
npm version major  # 1.0.0 -> 2.0.0 (breaking changes)

# 2. Publique
npm publish

# 3. Faça push das tags
git push && git push --tags
```

## 📥 Como Usar o Pacote em Outros Projetos

### Instalação Simples

```bash
npm install @blips/eslint-config --save-dev
# ou
pnpm add @blips/eslint-config -D
# ou
yarn add @blips/eslint-config -D
```

**Nota**: Como o pacote é público, não é necessário nenhuma configuração especial de autenticação!

### Uso no Projeto

**Para projetos Next.js**, crie/edite `.eslintrc.json`:

```json
{
  "extends": ["@blips/eslint-config/next"]
}
```

**Para projetos React**, crie/edite `.eslintrc.json`:

```json
{
  "extends": ["@blips/eslint-config/react"]
}
```

## 🌍 Acesso e Visibilidade

### Quem pode instalar?

- ✅ **Qualquer pessoa** pode instalar e usar este pacote
- ✅ Pacote disponível publicamente no NPM registry
- ✅ Não requer autenticação para instalação

### Quem pode publicar?

- 🔒 Apenas membros com acesso ao repositório **Blips-ativos/eslint-config-blips**
- 🔒 Apenas usuários autorizados no NPM com permissões para o scope `@blips`

## 🔐 Gerenciar Permissões no NPM

Para adicionar colaboradores que podem publicar:

1. Acesse: https://www.npmjs.com/settings/blips/packages
2. Clique no pacote `@blips/eslint-config`
3. Vá em "Collaborators" ou "Settings"
4. Adicione colaboradores com permissão de publicação

## 🔄 CI/CD (GitHub Actions)

Para usar em pipelines de CI/CD, o processo é simples:

```yaml
- name: Setup Node.js
  uses: actions/setup-node@v3
  with:
    node-version: '18'

- name: Install dependencies
  run: npm ci
```

Não é necessário configurar tokens ou autenticação para instalar o pacote.

## ❓ Troubleshooting

### Erro: "404 Not Found"
- Verifique se o pacote foi publicado corretamente
- Confirme o nome do pacote: `@blips/eslint-config`
- Tente limpar o cache do npm: `npm cache clean --force`

### Erro: "403 Forbidden" ao publicar
- Você pode não ter permissões para publicar no scope `@blips`
- Verifique se está logado: `npm whoami`
- Entre em contato com um administrador do scope `@blips` no NPM

### Erro: "You must sign up for private packages"
- Isso pode acontecer se o `publishConfig.access` não estiver configurado como `public`
- Verifique o `package.json` ou use: `npm publish --access public`

## 📝 Notas Importantes

1. O pacote é **público** e pode ser instalado por qualquer pessoa
2. Apenas membros autorizados podem publicar novas versões
3. Sempre use versionamento semântico (SemVer)
4. Mantenha o changelog atualizado
5. Teste as mudanças antes de publicar
6. Use `npm publish --access public` na primeira publicação

## 🔗 Links Úteis

- [NPM Package Page](https://www.npmjs.com/package/@blips/eslint-config)
- [NPM Documentation](https://docs.npmjs.com/)
- [Semantic Versioning](https://semver.org/)
- [Repository](https://github.com/Blips-ativos/eslint-config-blips)
