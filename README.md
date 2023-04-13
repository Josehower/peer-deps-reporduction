# peer-deps-reporduction

This repo shows an unexpected behaviour by pnpm when using peerdependencies not listed in package.json

to reproduce:

1. clone this repo
2. install dependencies with `pnpm install`
3. `pnpm run test`

you would recieve an error like this:

```console
➜  test-json pnpm install
Packages: +193
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
Packages are hard linked from the content-addressable store to the virtual store.
  Content-addressable store is at: /home/josehower/.local/share/pnpm/store/v3
  Virtual store is at:             node_modules/.pnpm
Progress: resolved 193, reused 193, downloaded 0, added 193, done

dependencies:
+ stylelint-config-upleveled 0.0.6

Done in 5.5s
➜  test-json pnpm run test

> @ test /home/josehower/upleveled-projects/test-json
> stylelint "**/*.css"

sh: 1: stylelint: not found
 ELIFECYCLE  Test failed. See above for more details.
```

if you use npm instead of pnpm the stylelint works as expected:

1. clone this repo
2. install dependencies with `npm install`
3. `npm run test`

```console
➜  test-json npm install

added 193 packages, and audited 194 packages in 8s

37 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
➜  test-json git:(main) ✗ npm run test

> test
> stylelint "**/*.css"


index.css
 1:1  ✖  Unexpected unknown type selector "lol"  selector-type-no-unknown
 1:5  ✖  Unexpected empty block                  block-no-empty

2 problems (2 errors, 0 warnings)
```
