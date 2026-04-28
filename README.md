# Pixi-Pack action using the `pixi-build-python` backend

Using this action you can create cross-platform self-extracting archives of pixi
environments.

It is a fork of the [pixi-pack-action] that is using the *Rattler* backend.

[pixi-pack-action]: https://github.com/Wytamma/pixi-pack-action

## Example Workflow

```yaml
name: 👷 Build & package via Pixi 🧚

on:

  release:
    types:
      - published  # A release, pre-release, or draft of a release was published.

  workflow_dispatch:

permissions:
  contents: write

jobs:

  build-and-package:

    name: Build package 📦 using pixi-build-python 🧚📦🐍

    runs-on: ubuntu-24.04

    strategy:
      matrix:
        platform: ["osx-arm64", "linux-64", "win-64"]
      fail-fast: false

    steps:
      - name: 📥 Checkout repo
        uses: actions/checkout@v6

      - name: Run Pixi-Pack 🧚📦
        uses: ehrenfeu/pixi-pack-action-python@v7
        with:
          platform: ${{ matrix.platform }}

      - name: 📤 Upload to Release
        uses: softprops/action-gh-release@v3
        with:
          files: "${{ github.event.repository.name }}-*.sh, ${{ github.event.repository.name }}-*.ps1"
```
