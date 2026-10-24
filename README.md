# Callisto releases

Installers and in-app updates for **Callisto**, an offline-first desktop API client for HTTP, GraphQL, WebSocket, Server-Sent Events and gRPC.

Download the latest version from **[Releases](https://github.com/amitkhairnar44/callisto-releases/releases/latest)**:

| Platform | File |
|---|---|
| macOS, Apple silicon | `Callisto_<version>_aarch64.dmg` |
| macOS, Intel | `Callisto_<version>_x64.dmg` |
| Windows | `Callisto_<version>_x64-setup.exe` (installs for your user) or the `.msi` |
| Linux | `.AppImage`, `.deb` or `.rpm` |

The builds aren't code-signed yet. On macOS, open the app once, then allow it in System Settings → Privacy & Security. On Windows, SmartScreen may ask you to confirm: More info, then Run anyway.

Each release lists every file's SHA-256 checksum in `SHA256SUMS.txt`. Updates installed from inside Callisto are signed separately and checked by the app before installing.

This repository holds releases only; the source is private.
