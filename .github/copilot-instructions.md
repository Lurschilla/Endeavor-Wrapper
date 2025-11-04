## Quick orientation for AI coding agents

This repository is an Expo (React Native) app using the Expo Router (file-based routing) and TypeScript.
Provide concise, repository-specific edits only. Preserve existing style and small utility components.

Key facts (do not assume otherwise):

- Entry & routing: the app uses `expo-router` and file-based routing. Main layout files:
  - `app/_layout.tsx` sets up a `Stack` and a `ThemeProvider`.
  - `app/(tabs)/_layout.tsx` configures bottom-tabs with `Tabs` and custom `tabBarButton` (`HapticTab`).
  - Add new routes by creating files under `app/` (e.g. `app/new-route.tsx` or `app/(group)/page.tsx`).

- TypeScript path alias: imports use `@/...` (see `tsconfig.json` where `@/*` -> `./*`). Use this alias for new imports.

- Theming & platform hooks:
  - Color mode is provided by a small hook at `app/hooks/use-color-scheme.ts` and consumed by `ThemeProvider` in `app/_layout.tsx`.
  - The repository favors `ThemedView` / `ThemedText` primitives (in `app/components/`) for consistent styles. Prefer them when adding UI.

- Important components/examples to reference when editing or adding UI:
  - `app/components/themed-text.tsx`, `app/components/themed-view.tsx` — patterns for text and view variants.
  - `app/components/haptic-tab.tsx` — custom tab button used by tabs layout.
  - `app/components/ui/icon-symbol.tsx` — icon component used in tab icons.
  - `app/components/parallax-scroll-view.tsx` — example of a complex custom scroll container.

- Reanimated: file `app/_layout.tsx` imports `'react-native-reanimated'` at top-level. Keep that import when touching layout/entry code.

- External content: `app/index.tsx` uses `react-native-webview` to load an external URL. Be cautious editing code that affects WebView origin/permissions or data flow.

- Scripts & developer workflows (from `package.json`):
  - Install: `npm install`
  - Start Metro / Expo dev tools: `npx expo start` (or `npm start`)
  - Platform shortcuts: `npm run android`, `npm run ios`, `npm run web`
  - Reset starter content: `npm run reset-project` (moves current `app` -> `app-example` and replaces `app`)
  - Lint: `npm run lint` (runs `expo lint`)

- Dependency surface: relies on Expo SDK (~54) and common React Navigation + Expo packages. Avoid adding native modules unless necessary.

Repository conventions and patterns to follow

- Prefer small focused components. Follow existing file-level organization: most UI lives in `app/components/` and `app/components/ui/`.
- Use the `@/` alias for imports (e.g. `import { ThemedText } from '@/components/themed-text'`).
- Keep layout/top-level imports minimal and stable: `app/_layout.tsx` and `app/(tabs)/_layout.tsx` control navigation and theming.
- When adding routes, mirror the file-based routing structure used by expo-router (group folders like `(tabs)` are significant).

Examples (explicit):

- To add a new modal route that the stack can present:
  - Create `app/modal.tsx` (it already exists). Stack screens are registered by file name; the layout declares a `modal` screen name.

- To add a new tab page:
  - Place `app/(tabs)/settings.tsx` and export default a React component. Tabs are wired by name in `app/(tabs)/_layout.tsx`.

Safety and reviewer notes for AI edits

- Do not remove or change the top-level `'react-native-reanimated'` import in `app/_layout.tsx` unless you understand the plugin setup.
- Avoid upgrading SDK or native deps in PRs without explicit user approval — changes to `expo` / `react-native` are high-risk.
- For network or external URL edits (see `app/index.tsx` WebView), call out privacy/security implications in PR description.

Files to reference when in doubt

- `app/_layout.tsx` (routing & ThemeProvider)
- `app/(tabs)/_layout.tsx` (tabs configuration)
- `app/(tabs)/index.tsx`, `app/index.tsx` (home screens)
- `app/components/*` (UI primitives)
- `package.json`, `tsconfig.json`, `README.md` (scripts, aliases, and developer notes)

If any guidance here is unclear or you need more examples (component signatures, story-like examples, or test patterns), ask the repository owner for preferred testing/linting rules and any PR checklist items to include.

— End of copilot instructions —
