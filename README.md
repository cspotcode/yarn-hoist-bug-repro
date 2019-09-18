|  |  |
|---|---|
package.json | depends on @cspotcode/yarn-hoist-bug-example-subpackage "latest" (this is a package stored in this monorepo, but we are installing the latest published version from npm)
packages/other-subpackage/package.json | depends on find-up v3 |
packages/yarn-hoist-bug-example-subpackage/package.json | depends on find-up v4 |


## Expected behavior:

yarn installs dependencies like this: (or otherwise satisfies everyone's find-up dependency)

|  |  |
|---|---|
`node_modules/find-up` | v3 |
`packages/yarn-hoist-bug-example-subpackage/node_modules/find-up` (**) | v4 |
`node_modules/@cspotcode/yarn-hoist-bug-example-subpackage` | latest version downloaded from npmjs.com |
`node_modules/@cspotcode/yarn-hoist-bug-example-subpackage/node_modules/find-up` | v4 |

## Actual behavior:

yarn does *not* install a copy of find-up v4 for packages/yarn-hoist-bug-example-subpackage (indicated by ** above)

## Repro:

Clone this repo.

```
yarn
node ./packages/other-subpackage
node ./packages/yarn-hoist-bug-example-subpackage # <-- assertion fails
```
