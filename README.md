I am operating inside a Typescript Monorepo. I want to add an Angular 8 frontend with Jest testing to the Monorepo. But I am encountering some issues.

I am using

```
Angular CLI: 8.3.5
```

# What I did

> I will use [this repository](https://github.com/flolude/stackoverflow-monorepo-angular-jest/tree/5e6b316b3be5f02a596735eeeb48e6c18dca10a2) as a starting point!

## 1. Create Angular Application

Then in `<root>/services` I ran:

```
ng new frontend
```

After the Angular application was created I was able to run `ng test` with the following result:
![ng test](pictures/ng-test-default.png)
Everything works fine.

## 2. Add Jest

> I am using https://github.com/briebug/jest-schematic to easily add Jest to my Angular application

```
yarn global add @briebug/jest-schematic
ng add @briebug/jest-schematic
```

This results in the following changes

![changes](pictures/schematics-changes.png)

The in `<root>/services` I ran

```
yarn test
```

This results in the following error:

```
$ jest
 FAIL  src/app/app.component.spec.ts
  ● Test suite failed to run

    File not found: <rootDir>/src/tsconfig.spec.json (resolved as: /home/flo/Desktop/stackoverflow-monorepo-angular-jest/services/frontend/src/tsconfig.spec.json)

      at ConfigSet.resolvePath (node_modules/ts-jest/dist/config/config-set.js:712:19)
      at ConfigSet.get (node_modules/ts-jest/dist/config/config-set.js:202:67)
      at ConfigSet.tsJest (node_modules/ts-jest/dist/util/memoize.js:43:24)
      at ConfigSet.get (node_modules/ts-jest/dist/config/config-set.js:297:41)
      at ConfigSet.versions (node_modules/ts-jest/dist/util/memoize.js:43:24)
      at ConfigSet.get (node_modules/ts-jest/dist/config/config-set.js:583:32)
      at ConfigSet.jsonValue (node_modules/ts-jest/dist/util/memoize.js:43:24)
      at ConfigSet.get [as cacheKey] (node_modules/ts-jest/dist/config/config-set.js:598:25)
      at TsJestTransformer.getCacheKey (node_modules/ts-jest/dist/ts-jest-transformer.js:126:36)
      at ScriptTransformer._getCacheKey (node_modules/@jest/transform/build/ScriptTransformer.js:266:23)

Test Suites: 1 failed, 1 total
Tests:       0 total
Snapshots:   0 total
Time:        1.267s
Ran all test suites.
```

Jest tries to find the `tsconfig.spec.json` in a wrong folder.
