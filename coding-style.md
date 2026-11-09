# React and TypeScript coding style

Apply this guide to first-party TypeScript and TSX in React web and React Native projects, including backend code, scripts, tests, and code examples. Generated files and adapted upstream code retain their required conventions and attribution. A project's `AGENTS.md` may add domain rules, name framework exceptions, or record a scoped migration, but must not silently weaken this guide.

Use TypeScript for new application logic, tests, and executable tooling. Keep platform-required formats and existing JavaScript files until a scoped change calls for migration.

## Functions and data flow

- Prefer named `const` arrow functions for functions, components, hooks, and callbacks. Use a function declaration or expression when a framework or language feature requires its semantics, such as a generator or dynamic `this`.
- Use an expression body for a single returned expression, including an object literal wrapped in parentheses. Use a block for guards, branching, multiple steps, effects, and error handling. Avoid nested ternaries and compressed error paths.
- Put exported entry points before supporting helpers. Below them, place callers before callees when initialization permits. Preserve hook order, eager setup, and resource lifetimes; these take precedence over declaration order.
- Prefer pure functions for parsing, validation, normalization, selection, and conversion. Keep network, storage, database, DOM, native SDK, and logging effects at visible boundaries. Pass clocks and changing context as arguments rather than hiding them in mutable module state.
- Use `const` by default and keep inputs unchanged. Prefer readonly collection inputs. Mutation of an accumulator or other data exclusively owned by a function is acceptable when it is clearer or avoids repeated copying.
- Use `map`, `filter`, `find`, `some`, `every`, and `reduce` when the result expresses the operation. Keep related transformations in a readable pipeline. Extract every `map`, `filter`, and `reduce` callback into a named helper, even for a one-line expression. Name callbacks to other collection methods when they contain branching, validation, or several steps. Do not discard a `map` result or use `reduce` only for side effects.
- Prefer `forEach` for a simple synchronous action on each item. Use `for...of` for early exit, `break`, `continue`, ordered cleanup, multi-step effects, and sequential `await`. Use explicit promise composition, such as `Promise.all(items.map(loadItem))`, for deliberately concurrent work. Never use `forEach(async ...)` for work that must finish.
- Give each function one clear purpose and keep it concise. A function longer than roughly ten lines prompts a search for meaningful helpers; decompose it unless the split would obscure the flow. Extract a helper when its name explains a domain step, removes repeated logic, or separates a transformation from an effect. Outside named collection callbacks, avoid wrappers that only rename an obvious expression.

## Modules and exports

- Give each module one identifiable responsibility and normally one main exported operation, component, or state owner. Keep its local types and short helpers beside it. Split by responsibility or dependency boundary, not by line count.
- Give every ordinary source folder an `index.ts` that explicitly names the values and types available outside that folder. Code outside the folder imports through its index, including when the caller is in a parent folder. Code within the folder imports the owning file directly. Do not create wildcard barrels or export private helpers merely to fill an index.
- Keep indexes free of import-time effects and avoid re-exporting modules whose import triggers work. Separate client, server, and platform-specific modules into folders with their own indexes so an import does not cross a runtime boundary or load unrelated dependencies.
- Use named exports in ordinary source modules. Reserve default exports for framework-required entry points, such as Expo Router routes. Keep implementation details unexported until a real consumer needs them.
- Framework-controlled paths may follow their required file and export conventions when an index or rename would change routing, code generation, or a deployed API. Document the exception in the project's `AGENTS.md`.
- Keep shared mutable state with one owner and expose operations on that owner. Keep acquisition and cleanup of subscriptions, connections, temporary files, and other resources close enough to review together.

## Names, types, and formatting

- Use descriptive domain names for values and operations. Name predicates with `is`, `has`, `can`, or another clear question. Include units when the type does not establish them, such as `timeoutMs` or `sizeBytes`.
- Use `camelCase` for values and functions and `PascalCase` for types, classes, and React components. Use kebab-case for ordinary `.ts` filenames. Use PascalCase for a `.tsx` file whose main export is a React component. Preserve framework-required filenames and external API spellings.
- Use two spaces, an 80-column code target, double quotes, semicolons, and trailing commas where supported. Let the repository formatter settle mechanical layout.
- Enable TypeScript strict checking for maintained source and tests. Fix type errors at their source rather than weakening the checks to make a change pass.
- Use blank lines to separate top-level declarations and distinct phases inside a function, such as validation, transformation, effects, and return construction. Use braces for multiline branches and loops.
- Define a type in the module or domain that owns its meaning. Name repeated, nested, or non-obvious contracts; leave small local shapes inline. Use `import type` and `export type` for type-only dependencies.
- Specify parameter and return types on every exported function and method. Private helpers may infer an obvious return type. Use interfaces for named object contracts that benefit from extension and type aliases for unions, tuples, and compositions; do not rewrite equivalent existing declarations merely for syntax uniformity.
- Accept `unknown` at untrusted runtime boundaries and validate or narrow it. Do not use `any`, non-null assertions, or casts to conceal an unresolved contract. Keep a necessary cast at the checked boundary and explain why TypeScript cannot establish the invariant.

## React and React Native

- Keep render paths free of storage writes, network calls, SDK commands, and other external effects. Handle user actions in event handlers and synchronize external systems in effects. Derive values from props and state during render instead of copying them into state through an effect.
- Call Hooks only at the top level of components or custom Hooks, before conditional returns. Enforce the Rules of Hooks and exhaustive effect dependencies with the project's lint checks.
- Include every reactive value an effect reads in its dependencies. Change the effect's code instead of suppressing a dependency warning. Clean up subscriptions and listeners, and cancel or ignore stale asynchronous results when dependencies change or a component unmounts.
- Declare component functions at module scope so re-renders preserve their identity. Use stable data IDs as keys for lists that can change order; use a key deliberately when a subtree's state should reset. Avoid array indexes and generated values as keys for reorderable lists.
- Add `memo`, `useMemo`, or `useCallback` for a measured cost or a required identity contract, rather than applying them to every component or expression.
- Keep pure transformations outside components when practical. Extract a focused hook when a component mixes independent lifecycles or resource ownership.
- Preserve keyboard, screen-reader, focus, and enlarged-text behavior when changing a UI flow. Follow the project's design system and platform conventions for the control being changed.

## TSDoc and implementation comments

- Put a `/** ... */` documentation comment at the owning declaration of every exported function, method, component, hook, class, and named type, including exports used only inside the project. Document project-owned public properties and interface members; short one-line comments suit obvious fields.
- Begin a callable's comment with a summary. Add `@param name - description` for every parameter and `@returns` for every non-void result. For `Promise<void>`, state what resolution acknowledges. Describe meaningful thrown errors and promise rejection conditions with `@throws`. Keep types in the TypeScript signature rather than repeating them in JSDoc annotations.
- Document units, defaults, valid ranges, ownership, effects, persistence, retry behavior, and asynchronous completion where they affect use. Document object parameter fields on their named options type, and component inputs on the props type. Use `@remarks` for longer lifecycle details. Keep contract documentation at its owner instead of copying it to implementations or index files.
- Use standalone `/**` and `*/` lines for multiline documentation, with a leading `*` on each content line and one blank starred line between the summary and tags. Keep consecutive `@param` tags together.
- Give a tricky private helper a short function-level documentation comment explaining its intent or contract. Simple local selectors need no ceremonial documentation.
- Use concise one-line `//` comments when the intent of the next code is not clear from context. Generally start with a verb that names the intended action or result, such as `// Restore the saved selection before the list re-renders.` Comments may also explain invariants, security boundaries, race protection, ordering, platform differences, and workarounds. Add meaning beyond the code's syntax. If a tricky block needs a longer explanation, extract a named helper and document its intent at the function level.
- Give a workaround its trigger and removal condition, with a source or regression test when available. Mark an intentional known limit as `shortcut: <limit>, <when to upgrade>`. Make TODOs actionable and identify the remaining work or decision. Keep comments current; remove commented-out code and debugging narratives while preserving required attribution and license notices.

A named helper makes even a one-line filter readable:

```ts
const isEven = (num: number): boolean => num % 2 === 0;

const evenNumbers = [1, 2, 3, 4].filter(isEven);
```

The documentation below names the unit, result, and failure without repeating the TypeScript types:

```ts
/**
 * Converts a duration to whole seconds.
 *
 * @param durationMs - Nonnegative duration in milliseconds.
 * @returns Whole seconds, rounded down.
 * @throws RangeError when the duration is negative or not finite.
 */
export const wholeSeconds = (durationMs: number): number => {
  if (!Number.isFinite(durationMs) || durationMs < 0) {
    throw new RangeError("durationMs must be finite and nonnegative");
  }

  return Math.floor(durationMs / 1000);
};
```

## Errors, tests, and review

- Validate external data and operator input where they enter the system. Distinguish missing data, invalid input, unsupported behavior, and failed processing. Do not report a failed operation as an empty success or silently discard a required effect.
- Keep credentials and sensitive URLs out of ordinary logs, errors, fixtures, and examples. Use argument arrays rather than interpolated shell commands when launching a subprocess with untrusted values.
- Put tests in a `tests/` folder outside `src/` for each app or package. Organize them by behavior or domain, with fixtures beside the tests that use them. Framework-required test placement may be a documented local exception.
- Give new nontrivial logic and bug fixes a focused behavioral test unless meaningful existing coverage already catches the regression. Test observable results, failure boundaries, ordering, and cleanup where relevant. Avoid tests that merely repeat implementation statements or framework guarantees.
- Review affected callers, tests, fixtures, configuration, exports, data-loss paths, and security boundaries before finishing a change. Run the relevant formatter, type checks, and focused tests using the project's commands. Report which checks ran and what remains unverified.
