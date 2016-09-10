# Status

#### **Requirements**
- [ ] Satisfied with the file/directory structure
- [ ] All files have cool little headings and stuff

#### **Experiments**
- [ ] Update Typescript dep
- [ ] Update angular dep to `rc6`
- [ ] Refactor for ts2 features

# Changes

## **0.4.666**
- #### **Directories & Modules**
  - renamed `app` to `src` since this is more of a library
  - added `src/modules` to contain sub-packages in a way that works well with node module resolution. For example,  `angular2-logger/subset` will elegantly point to whatever's exported by `src/modules/subset/index.ts`. (Just copy how I set up `core`'s files and make a `src/subset.ts`.)
    - **Feature:** Bundlers like Webpack may automatically pick the proper es5 or es6 `js` depending on their target configuration. Works with the `angular-cli`.
    - **Feature:** `src/index.ts` can be used to customize what can be imported from `angular2-logger`. It could be used as an alias for `angular2-logger/core`, or it could be like the greatest-hits from a bunch of little sub-packages.
    - **Query:** _Is it even worth it to have sub-packages like 'core' and whatever else? I feel like it might just be a bunch of extra typing & memorization for consumers of the api. Since `rc5`, we have NgModules to package sets of resources together._
- #### **package.json**
  - `"main"` points at the es5 entry point, which is the umd `index.js` right now (TODO: point at bundle)
  - `"module"` points at the es6 entry point, overriding `main`. This behavior has been adopted for es6 compatible builds using Webpack (`angular-cli` uses it.)
  - `"typings"` points to the `.d.ts` entry point.
  - `"compile"` tasks now pass configuration to the compiler to avoid duplicate `tsconfig.json` files
  - `"clean"` now uses `del-cli` for safer deletes with simpler glob patterns
- #### **typings.json**
  - `src/typings.d.ts` added to reference global types and `core-js` was removed from `typings.json`. Instead, the `es6` default lib is forced for all modules. This is done by setting `noLib` in `tsconfig.json` to stop the default lib from loading, and then explicitely referencing the es6 default (`lib.es6.d.ts`) in `typings.d.ts`. Typescript 2.0.0+ lets you do this out of the box, but this hack is needed for older versions
- #### **Miscellanious**
  - Organized `.gitignore` entries

## **0.4.5**
...
