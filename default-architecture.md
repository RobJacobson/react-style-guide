# Default architecture

Use these defaults for new React and React Native apps and for architecture changes the user requests. A project's `AGENTS.md` or an explicit user instruction in chat may override them. Keep an existing app's stack until the user requests a migration.

## Platform defaults

| Target | Framework | Styling | UI components |
| --- | --- | --- | --- |
| Web only | [TanStack Start](https://tanstack.com/start/latest) | [Tailwind CSS 4](https://tailwindcss.com/docs/installation) | [shadcn/ui](https://ui.shadcn.com/docs/installation) |
| Native, including native and web | [Expo default template](https://docs.expo.dev/get-started/create-a-project/) | [NativeWind 5](https://www.nativewind.dev/v5/getting-started/installation) | [Expo UI](https://docs.expo.dev/versions/latest/sdk/ui/) and [React Native Reusables](https://reactnativereusables.com/docs/installation) |

Use TanStack Start's Router for web apps. Prefer other TanStack packages when their capability is needed, and install only those the app uses. Initialize shadcn/ui during setup, then add only the components the app uses.

Start native apps from Expo's default template and keep its default packages, including Expo Router and TypeScript. Add NativeWind 5, `@expo/ui`, and React Native Reusables during setup, then add individual reusable components as needed. When an app targets native and web, use one Expo project for those targets by default. A different structure requires an explicit user instruction.

For Android and iOS controls, prefer `@expo/ui` when it provides the needed native component. Use its universal components when one UI tree should also run on web. Use React Native Reusables for complementary shared or custom controls. When implementing native UI, consult the [Expo UI documentation](https://docs.expo.dev/versions/latest/sdk/ui/) for the project's Expo SDK and the examples and guidance linked from `~/code/expo-native-ui/README.md` when that local reference project is available.

## Shared defaults

- Use [Bun](https://bun.sh/docs) for package management and local scripts. Commit its lockfile. Let the framework and hosting platform determine the deployed runtime.
- Use [Vite+](https://viteplus.dev/guide/) for compatible build, test, lint, formatting, and task workflows. Expo retains Metro for bundling.
- Add [Convex](https://docs.convex.dev/) when the app needs a database, backend functions, real-time data, or another Convex feature. Do not initialize it before that need exists.
- Prefer [Cloudflare R2](https://developers.cloudflare.com/r2/) for file and object storage, including uploads, when the app needs it. Do not provision a bucket before that need exists. Prefer R2 over Convex file storage.
