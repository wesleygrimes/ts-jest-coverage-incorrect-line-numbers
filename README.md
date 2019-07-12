# ts-jest-coverage-incorrect-line-numbers

Having an issue when running `yarn test` with `jest.config.js` `collectCoverage: true`. The line number and stack reported are incorrect.

Actual Output:

```sh
$ jest
 FAIL  src/foo.test.ts
  ✕ will it blow up? (4ms)

  ● will it blow up?

    Uh oh!



      at Object.ifCalledWillBlowUp (src/foo.ts:100:9)
      at Object.<anonymous> (src/foo.test.ts:4:3)

Test Suites: 1 failed, 1 total
Tests:       1 failed, 1 total
Snapshots:   0 total
Time:        1.591s
Ran all test suites.
error Command failed with exit code 1.
```

Expected Output:

```sh
$ jest
 FAIL  src/foo.test.ts
  ✕ will it blow up? (4ms)

  ● will it blow up?

    Uh oh!

      1 | export function ifCalledWillBlowUp() {
    > 2 |   throw new Error('Uh oh!');
        |         ^
      3 | }
      4 |

      at Object.ifCalledWillBlowUp (src/foo.ts:2:9)
      at Object.<anonymous> (src/foo.test.ts:4:3)

Test Suites: 1 failed, 1 total
Tests:       1 failed, 1 total
Snapshots:   0 total
Time:        1.424s
Ran all test suites.
error Command failed with exit code 1.
```

## Reproducing Issue

Issue can be reproduced running `yarn test` or `npm run test`

## Env Info

```json
// package.json
{
  "@types/jest": "^24.0.15",
  "jest": "^24.8.0",
  "ts-jest": "^24.0.2",
  "typescript": "^3.5.3"
}
```
