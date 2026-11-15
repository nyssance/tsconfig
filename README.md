# tsconfig

[![npm version](https://img.shields.io/npm/v/%40nyssance%2Ftsconfig)](https://www.npmjs.com/package/@nyssance/tsconfig)

The one TypeScript configuration shared by every project. A project's own `tsconfig.json` extends it and
adds only what is specific to that project: `types`, `paths`, `jsx` and `include`.

The options are Vite's `react-ts` template, minus everything that is already a TypeScript 7 default.

## Usage

```sh
bun add -d @nyssance/tsconfig
```

A project that runs in the browser:

```json
{
  "extends": "@nyssance/tsconfig",
  "compilerOptions": {
    "types": ["vite/client"],
    "jsx": "react-jsx"
  },
  "include": ["src"]
}
```

A project that runs only on Bun, with no DOM types:

```json
{
  "extends": "@nyssance/tsconfig/bun.json"
}
```

## Options

| Option | Why it is set |
| --- | --- |
| `target: "ESNext"` | Brings the ESNext library and ESNext modules; the default stops at ES2025. |
| `skipLibCheck` | Errors inside a dependency's `.d.ts` are not the project's to fix. |
| `allowImportingTsExtensions`, `noEmit` | Imports may name `.ts` files; the bundler or Bun emits, not TypeScript. |
| `verbatimModuleSyntax` | Type-only imports must say `import type`. |
| `moduleDetection: "force"` | Every file is a module, including one with no imports or exports. |
| `noUnusedLocals`, `noUnusedParameters` | Unused code is an error. |
| `erasableSyntaxOnly` | No `enum`, `namespace` or constructor parameter properties. |
| `noFallthroughCasesInSwitch` | A `case` must end in `break`, `return` or `throw`. |

`bun.json` adds `lib: ["ESNext"]` and `types: ["bun"]`: without the DOM library, Bun's own types apply, such as
`.text()` on a subprocess stream.

Options that are TypeScript 7 defaults are not repeated: `strict`, `esModuleInterop`, `resolveJsonModule`,
`moduleResolution`, `forceConsistentCasingInFileNames`.
