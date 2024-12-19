# Reproduction of Expo tree shaking not removing unused code when using namespace imports

1. To reproduce the issue, first run an `npm install`.
2. Then, bundle the application for web by running `npx expo export --platform web`.
3. Notice that the final bundle (inside `dist/_expo/static/js/web`) includes
   both the function `foo` and the function `bar`, even though only `foo` is
   used inside `index.ts`.
4. Change the import in `index.ts` to a named import (`import { foo } from './utils'`)
   and re-run `npx expo export --platform web`.
5. Notice that now the final bundle includes only the function `foo`, which
   clearly indicates that namespace imports are not tree-shaken in the same way
   as named imports.
