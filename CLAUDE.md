# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

`@blips/eslint-config` is a public npm package providing shared ESLint configurations for Blips projects. It uses ESLint v9+ Flat Config format and provides three configuration presets: base (TypeScript), react, and next (Next.js).

## Configuration Architecture

The package exports three configuration presets through a layered composition pattern:

1. **base.js** - Foundation configuration
   - ESLint recommended rules
   - TypeScript ESLint recommended rules
   - Prettier integration
   - Simple import sort plugin
   - Used as the foundation for all other configs

2. **react.js** - Extends base with React support
   - Imports and extends base.js
   - React recommended rules
   - React Hooks rules
   - Browser + Service Worker globals
   - Disables `react/react-in-jsx-scope` (new JSX transform)
   - Disables `react/prop-types` (TypeScript handles types)

3. **next.js** - Extends base with Next.js + React
   - Imports base.js directly (does NOT extend react.js)
   - React + React Hooks + Next.js plugins
   - TypeScript parser configuration with JSX support
   - Core Web Vitals rules
   - Prettier errors (not just warnings)
   - Disables `@typescript-eslint/no-explicit-any`

**Important**: The Next.js config does NOT extend the React config - it composes base.js directly and includes React plugins separately. This means changes to React-specific rules must be duplicated in next.js if needed there.

## Package Exports

The package.json defines three export paths:
- `@blips/eslint-config/base` → base.js
- `@blips/eslint-config/react` → react.js
- `@blips/eslint-config/next` → next.js

Consumers import configs using: `import { config } from "@blips/eslint-config/next"`

## Development Commands

Test the package locally in another project:
```bash
# In this repo - link the package
npm link

# In consuming project - use the linked package
npm link @blips/eslint-config
```

## Publishing Workflow

Version and publish (requires npm auth and @blips scope permissions):
```bash
# Update version (creates git tag)
npm version patch  # Bug fixes (1.0.0 -> 1.0.1)
npm version minor  # New features (1.0.0 -> 1.1.0)
npm version major  # Breaking changes (1.0.0 -> 2.0.0)

# Publish to npm
npm publish

# Push with tags
git push && git push --tags
```

First-time publish requires: `npm publish --access public`

## Key Constraints

- ESLint v9+ required (Flat Config format only)
- TypeScript is an optional peer dependency
- Package is public - anyone can install, only authorized users can publish
- All configs use ES modules (not CommonJS)
- Each config file exports a `config` constant that is an ESLint Flat Config array

## Legacy Project Support

For projects with many ESLint errors, the README recommends using `eslint-plugin-only-warn` to convert all errors to warnings during migration.
