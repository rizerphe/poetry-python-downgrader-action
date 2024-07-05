# Poetry Python Downgrader

This is a github action for [poetry-python-downgrader](https://github.com/rizerphe/poetry-python-downgrader).

[![Use action](https://img.shields.io/badge/Use_action-gray?style=flat-square&logo=GitHub%20Actions)](https://github.com/marketplace/actions/poetry-python-downgrader)
[![The original project](https://img.shields.io/badge/The_original_project-gray?style=flat-square&logo=GitHub)](https://github.com/rizerphe/poetry-python-downgrader)
[![Latest release](https://flat.badgen.net/github/release/rizerphe/poetry-python-downgrader-action)](https://github.com/rizerphe/poetry-python-downgrader-action/releases)
[![License: MIT](https://flat.badgen.net/github/license/rizerphe/poetry-python-downgrader-action)](https://opensource.org/licenses/MIT)
[![PyPI project](https://flat.badgen.net/pypi/v/poetry-python-downgrader)](https://badge.fury.io/py/poetry-python-downgrader)

## Quickstart

```yaml
- name: Downgrade Poetry packages
  uses: rizerphe/poetry-python-downgrader@v0.1.5
  with:
      python-version: "3.8"
```

This action will modify `pyproject.toml` in place, making sure it is compatible with Python 3.8.

## Usage

You can use this tool as a GitHub Action in your workflows. Here's an example of how to use it:

```yaml
- name: Downgrade Poetry packages
  uses: rizerphe/poetry-python-downgrader@v0.1.5
  with:
      python-version: "3.8"
      pyproject-path: "pyproject.toml"
      pin-versions: "false"
      repository: "https://pypi.org/pypi"
```

**Action inputs:**

-   `pyproject-path` (defaults to `pyproject.toml`): The path to the `pyproject.toml` file.
-   `python-version` (defaults to "3.6"): The target Python version to downgrade the dependencies for.
-   `pin-versions` (defaults to "false"): Set to "true" to pin package versions exactly instead of using caret ranges.
-   `repository` (optional, defaults to "https://pypi.org/pypi"): The PyPI repository URL to use for querying package information.

### Examples

**Basic usage (downgrade to Python 3.8)**

```yaml
- uses: rizerphe/poetry-python-downgrader@v0.1.5
  with:
      python-version: "3.8"
```

**Use in a version matrix**

```yaml
jobs:
    build:
        runs-on: ubuntu-latest
        strategy:
            matrix:
                python-version: ["3.6", "3.7", "3.8", "3.9", "3.10", "pypy3.10"]
        steps:
            - uses: actions/checkout@v2
            - uses: actions/setup-python@v2
              with:
                  python-version: ${{ matrix.python-version }}
            - uses: rizerphe/poetry-python-downgrader@v0.1.5
              with:
                  python-version: ${{ matrix.python-version }}
```

This action does not support all github actions python versions; it'll just skip the downgrade if it doesn't know how to handle the version.

**Downgrade with pinned versions**

```yaml
- uses: rizerphe/poetry-python-downgrader@v0.1.5
  with:
      python-version: "3.8"
      pin-versions: "true"
```

**Use a custom PyPI repository**

```yaml
- uses: rizerphe/poetry-python-downgrader@v0.1.5
  with:
      python-version: "3.8"
      repository: "https://custom-pypi.example.com/pypi"
```

**Specify a different pyproject.toml location**

```yaml
- uses: rizerphe/poetry-python-downgrader@v0.1.5
  with:
      python-version: "3.8"
      pyproject-path: "path/to/pyproject.toml"
```
