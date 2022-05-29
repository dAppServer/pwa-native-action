# pwa-native-action

Create a native binary from a PWA, using GitHub Actions. If you like this, try Wails.io

* for now you need to build windows from mac-os *

```yaml
name: Lethean Desktop build
permissions:
  contents: write
on: [push, pull_request]

jobs:
  build:
    strategy:
      fail-fast: false
      matrix:
        build: [
          { name: Lethean, platform: linux/amd64, os: ubuntu-latest },
          { name: Lethean, platform: windows/amd64, os: macos-latest },
          { name: Lethean, platform: darwin/universal, os: macos-latest }
        ]
    runs-on: ${{ matrix.build.os }}
    steps:
      # Checkout code
      - uses: actions/checkout@v2
        with:
          repository: 'letheanVPN/lthn-app-desktop'
          submodules: recursive
      - uses: dAppServer/pwa-native-action@main
        with:
          pwa-build: ${{ github.workspace }}
          build-name: ${{ matrix.build.name }}
          build-platform: ${{ matrix.build.platform }}
```
