# Default architecture

Use these defaults for new React and React Native apps and for architecture changes the user requests. A project's `AGENTS.md` or an explicit user instruction in chat may override them. Keep an existing app's stack until the user requests a migration.

## Platform defaults

| Target | Framework | Styling | UI components |
| --- | --- | --- | --- |
| Web only | [TanStack Start](https://tanstack.com/start/latest) | [Tailwind CSS 4](https://tailwindcss.com/docs/installation) | [shadcn/ui](https://ui.shadcn.com/docs/installation) |
| Native, including native and web | [Expo default template](https://docs.expo.dev/get-started/create-a-project/) | [NativeWind 5](https://www.nativewind.dev/v5/getting-started/installation) | [Expo UI](https://docs.expo.dev/versions/latest/sdk/ui/) and [React Native Reusables](https://reactnativereusables.com/docs/installation) |

- On web, prefer other TanStack packages when their capability is needed, and install only those the app uses. Add only the shadcn/ui components the app uses.
- On native, keep the Expo template's default packages. Prefer `@expo/ui` universal components when one UI tree should also run on web. Use React Native Reusables for complementary shared or custom controls, adding each component as needed.
- Use one Expo project when an app targets native and web.
- For native controls, see `~/code/expo-native-ui/README.md` when that local reference project is available.

## Shared defaults

- Use [Bun](https://bun.sh/docs) for package management and local scripts. Commit its lockfile. Let the framework and hosting platform determine the deployed runtime.
- Use [Vite+](https://viteplus.dev/guide/) for compatible build, test, lint, formatting, and task workflows. Expo retains Metro for bundling.
- Add [Convex](https://docs.convex.dev/) only once the app needs a database, backend functions, real-time data, or another Convex feature.
- Prefer [Cloudflare R2](https://developers.cloudflare.com/r2/) over Convex file storage for files and uploads, and add a bucket only once the app needs one.
