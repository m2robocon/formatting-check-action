# formatting-check-action
Checks whether the code is formatted according to project guidelines.

Based on [jidicula/clang-format-action](https://github.com/jidicula/clang-format-action).
Currently only checks formatting of C/C++ source codes, will be extended soon to check Python formatting using `black`.

## Usage

Example workflow file:
```yaml
name: my-workflow

on:
  workflow_dispatch:
  pull_request:
  push:
    branches:
      - master

jobs:
  formatting-check:
    name: Formatting Check
    runs-on: ubuntu-20.04
    strategy:
      matrix:
        path:
          - 'src'
    steps:
      - uses: actions/checkout@v2
      - name: Formatting Check
        uses: m2robocon/formatting-check-action@v1
        with:
          clang-format-version: '13'
          clang-format-check-path: ${{ matrix.path }}
          clang-format-exclude-regex: ''
          clang-format-fallback-style: 'GNU'
```

## Inputs

- `clang-format-version`
  - Optional. Specifies what clang-format version to use.
- `clang-format-check-path`
  - Optional. Specifies what path to check formatting.
- `clang-format-exclude-regex`
  - Optional. Specifies what Regex pattern to exclude formatting check.
- `clang-format-fallback-style`
  - Optional. Specifies what fallback style to use if there is no `.clang-format` file.

## License
Licensed under the Apache 2.0 License.