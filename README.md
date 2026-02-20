Starter React Vitest Stryker

Steps to reproduce the repository

node -v
v22.12.0
npm -v
11.10.0

`ng new starter-angular-vitest-stryker`

vitest is now default in angular 21, so no need to install anything.

`npm install --save-dev @stryker-mutator/core @stryker-mutator/vitest-runner @stryker-mutator/typescript-checker`

Edit **package.json** in root folder
```json
{
  "name": "starter-angular-vitest-stryker",
  "version": "0.0.0",
  "scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "watch": "ng build --watch --configuration development",
    "test": "ng test",
    "mutation": "stryker run" // 🚨
  },
  "prettier": {
    "printWidth": 100,
    "singleQuote": true,
    "overrides": [
      {
        "files": "*.html",
        "options": {
          "parser": "angular"
        }
      }
    ]
  },
  "private": true,
  "packageManager": "npm@11.10.0",
  "dependencies": {
    "@angular/common": "^21.1.0",
    "@angular/compiler": "^21.1.0",
    "@angular/core": "^21.1.0",
    "@angular/forms": "^21.1.0",
    "@angular/platform-browser": "^21.1.0",
    "@angular/router": "^21.1.0",
    "rxjs": "~7.8.0",
    "tslib": "^2.3.0"
  },
  "devDependencies": {
    "@angular/build": "^21.1.4",
    "@angular/cli": "^21.1.4",
    "@angular/compiler-cli": "^21.1.0",
    "@stryker-mutator/core": "^9.5.1",
    "@stryker-mutator/typescript-checker": "^9.5.1",
    "@stryker-mutator/vitest-runner": "^9.5.1",
    "jsdom": "^27.1.0",
    "typescript": "~5.9.2",
    "vitest": "^4.0.8"
  }
}

Create file **stryker.config.json** in root folder
```json
{
    "checkers": [
        "typescript"
    ],
    "tsconfigFile": "tsconfig.json"
}
```

`npm run mutation`
```bash
npm run mutation

> starter-angular-vitest-stryker@0.0.0 mutation
> stryker run

07:54:57 (25372) INFO ProjectReader Found 6 of 25 file(s) to be mutated.
07:54:57 (25372) INFO Instrumenter Instrumented 6 source file(s) with 5 mutant(s)
07:54:57 (25372) INFO ConcurrencyTokenProvider Creating 10 checker process(es) and 9 test runner process(es).
07:55:10 (25372) INFO DryRunExecutor Starting initial test run (command test runner with "perTest" coverage analysis). This may take a while.
07:55:15 (25372) INFO DryRunExecutor Initial test run succeeded. Ran 1 tests in 4 seconds (net 4782 ms, overhead 1 ms).
Mutation testing  [] 100% (elapsed: <1m, remaining: n/a) 5/5 Mutants tested (2 survived, 0 timed out)    

All tests
  ✓ All tests (killed 1)

[Survived] ArrayDeclaration
src/app/app.config.ts:7:14
-     providers: [
-       provideBrowserGlobalErrorListeners(),
-       provideRouter(routes)
-     ]
+     providers: []

[Survived] ArrowFunction
src/main.ts:6:10
-     .catch((err) => console.error(err));
+     .catch(() => undefined);

Ran 0.60 tests per mutant on average.
----------------|------------------|----------|-----------|------------|----------|----------|
                | % Mutation score |          |           |            |          |          |
File            |  total | covered | # killed | # timeout | # survived | # no cov | # errors |
----------------|--------|---------|----------|-----------|------------|----------|----------|
All files       |  33.33 |   33.33 |        1 |         0 |          2 |        0 |        2 |
 app            |  50.00 |   50.00 |        1 |         0 |          1 |        0 |        2 |
  app.config.ts |   0.00 |    0.00 |        0 |         0 |          1 |        0 |        1 |
  app.routes.ts |    n/a |     n/a |        0 |         0 |          0 |        0 |        1 |
  app.ts        | 100.00 |  100.00 |        1 |         0 |          0 |        0 |        0 |
 main.ts        |   0.00 |    0.00 |        0 |         0 |          1 |        0 |        0 |
----------------|--------|---------|----------|-----------|------------|----------|----------|
07:55:20 (25372) INFO HtmlReporter Your report can be found at: file:///C:/Users/thoma/projects/perso/tests_sandbox/starter-angular-vitest-stryker/reports/mutation/mutation.html
07:55:20 (25372) INFO MutationTestExecutor Done in 23 seconds.
```