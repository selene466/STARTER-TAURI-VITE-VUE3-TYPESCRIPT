# Vue starter project for Tauri

This is a starter template [tauri](https://tauri.app/) + [VUE.js 3](https://vuejs.org/) + [VITE](https://vitejs.dev/).  
It will create a local app with Rust as backend and VITE + VUE3 as front-end.

Don't install ANY Vue router, it will not work with Tauri, instead use `App.vue` directly.

## Whats new

- Added Tailwind v3
- Integrated UI with daisyUI v4
- Automatic class sorting with Prettier
- Auto import components & layouts
- Auto import icons
- Support for theme changer
- Installed iconify-json to work offline: bxs, fluent, ic, mdi, noto
- Test dialog

Check `vite.config.ts`.

## Start a new app

Copy this repo and you are ready to start.

### Installation

Copy this repo and install dependencies with `yarn`.

```cmd
yarn
```

### Develop front-end

Run `yarn tauri dev` to start the front-end.

```cmd
yarn tauri dev
```

Also read how to [mocking Tauri APIs](https://tauri.app/v1/guides/testing/mocking)

### Building the full app

This will build the front-end and then the app as one `.exe` file.

```cmd
yarn tauri build
```

Build location is in `src-tauri/target/release`.  
For the bundle installer in `src-tauri/target/release/bundle`.

# Tauri + Vue + TypeScript

This template should help get you started developing with Vue 3 and TypeScript in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) + [Tauri](https://marketplace.visualstudio.com/items?itemName=tauri-apps.tauri-vscode) + [rust-analyzer](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer)

## Type Support For `.vue` Imports in TS

Since TypeScript cannot handle type information for `.vue` imports, they are shimmed to be a generic Vue component type by default. In most cases this is fine if you don't really care about component prop types outside of templates. However, if you wish to get actual prop types in `.vue` imports (for example to get props validation when using manual `h(...)` calls), you can enable Volar's Take Over mode by following these steps:

1. Run `Extensions: Show Built-in Extensions` from VS Code's command palette, look for `TypeScript and JavaScript Language Features`, then right click and select `Disable (Workspace)`. By default, Take Over mode will enable itself if the default TypeScript extension is disabled.
2. Reload the VS Code window by running `Developer: Reload Window` from the command palette.

You can learn more about Take Over mode [here](https://github.com/johnsoncodehk/volar/discussions/471).
