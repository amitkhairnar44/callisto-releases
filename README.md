# Callisto releases

Installers and in-app updates for **Callisto**, an offline-first desktop API client for HTTP, GraphQL, WebSocket, Server-Sent Events and gRPC, and pre-releases of **Callisto Preview**.

Callisto keeps your work on your device. Collections are plain files you can keep in Git, secrets stay encrypted with a key in your system keychain, and nothing leaves your machine unless you send it.

## Download

Get the latest version from **[Releases](https://github.com/amitkhairnar44/callisto-releases/releases/latest)**. The current version is **0.3.0**, for macOS, Windows and Linux.

| Platform | File |
|---|---|
| macOS, Apple silicon | `Callisto_<version>_aarch64.dmg` |
| macOS, Intel | `Callisto_<version>_x64.dmg` |
| Windows | `Callisto_<version>_x64-setup.exe` (installs for your user) or the `.msi` |
| Linux | `.AppImage`, `.deb` or `.rpm` |

The builds aren't code-signed yet:

- **macOS:** the app isn't notarized. Open it once, then allow it in System Settings → Privacy & Security.
- **Windows:** SmartScreen may ask you to confirm: More info, then Run anyway.

Each release lists every file's SHA-256 checksum in `SHA256SUMS.txt`. Updates installed from inside Callisto are signed separately, and the app checks the signature before installing.

## Callisto Preview

Callisto Preview is Callisto built on GPUI, a native UI toolkit, instead of a webview. It has the same features as Callisto and installs beside it rather than replacing it. It's a pre-release to try out: get it from **[Callisto Preview 0.3.0](https://github.com/amitkhairnar44/callisto-releases/releases/tag/preview-v0.3.0)**, for macOS for now. Windows and Linux builds will follow.

| Platform | File |
|---|---|
| macOS, Apple silicon | `Callisto-Preview_<version>_aarch64.dmg` |
| macOS, Intel | `Callisto-Preview_<version>_x64.dmg` |

How it differs from Callisto:

- **Its own data:** its own list of workspaces, history, settings and secrets. It opens the same workspace folders, but a secret set in one app isn't readable in the other, and neither app can remove the other's secrets.
- **No updates:** it doesn't check for or install updates. Download a newer preview from the releases page.
- **No HTML preview:** HTML responses show their source.

Like Callisto, it isn't notarized yet: open it once, then allow it in System Settings → Privacy & Security.

## What's in Callisto 0.3.0

### HTTP requests

- Every method, including custom ones. Query parameters stay in step with the URL as you type either.
- Headers, and request bodies of every kind: raw text (JSON, XML, HTML or plain), URL-encoded and multipart forms, a binary file, or GraphQL.
- Auth: Basic, Bearer and API key (in a header or the query string). Requests can also inherit auth from their folder or collection, and the editor shows what they inherit.
- `{{variables}}` anywhere: the URL bar highlights them, shows each one's value when you hover over it, and underlines any that aren't defined.
- Per-request options: follow redirects, verify TLS certificates, and a timeout.
- Proxies: the system's, none, or one you set (HTTP, HTTPS or SOCKS5, with a user name and a password kept in the vault, and hosts to reach directly).
- Your own CA certificates and client certificates, and cookies kept per workspace.
- Format a JSON body in one click: only whitespace changes, so numbers and `{{variables}}` stay as typed.

### Responses

- Status, time and size at a glance, with a timing breakdown (DNS, connecting and TLS, waiting for the server, download) and the redirects followed.
- The body pretty-printed (JSON, XML and HTML) or raw, with search, copy and save. Large bodies stream to disk instead of filling memory.
- A JSONPath filter to pick out parts of a JSON response.
- HTML responses previewed in a sandbox, never run in the app.
- Response headers and cookies, and the request headers that were actually sent.

### GraphQL

- Queries and mutations over a JSON POST, or GET with the operation in the URL.
- The schema fetched by introspection and cached per endpoint, with autocomplete, checks as you type, and highlighting.
- A docs explorer with search; ⌘-click or Ctrl-click a field to open its docs.
- An operation picker, variables checked against the operation's types, Insert variables, and Prettify.
- Errors the server returns with HTTP 200 shown as errors, with their message, path and position, and whether partial data came back.
- Subscriptions over WebSocket, with a connection payload for servers such as Hasura and Apollo.

### WebSocket and Server-Sent Events

- **WebSocket:** connect, send saved text, JSON or binary messages (with `{{variables}}`), and disconnect. Close codes and reasons are shown.
- **Server-Sent Events:** any method and body, so streaming `POST` APIs work. Each event arrives with its type and ID.
- A live message log you can filter by text and direction. Open any message to see its JSON pretty-printed or binary data as a hex dump, and copy it.
- Proxy, certificate and cookie settings apply as they do for HTTP.

### gRPC

- All four kinds of call: unary, server streaming, client streaming and bidirectional.
- Services from server reflection, or from proto files you import into the workspace (a folder, or single files). No `protoc` needed.
- A method picker grouped by service, and an Example message button that fills in every field.
- Messages as JSON with `{{variables}}`. Metadata goes in the header table, and auth becomes metadata.
- For client and bidirectional streams, send saved messages while the call runs, then end the stream.
- The status and its message, response metadata and trailers, decoded error details, a deadline per call, and gzip.
- Copy a call as a `grpcurl` command.

### Collections, environments and secrets

- Collections and folders in a tree with search, drag and drop, inline rename, and delete with undo. Workspaces are folders of plain YAML files that you can keep in Git.
- Variables at five levels: global, workspace, collection, environment and request. Switch environments from the top of the window.
- Secrets (passwords, tokens, keys) are encrypted on your device with a key in your system keychain, and shown only when you choose to reveal them. They never go into collection files, exports, history or anything that syncs.

### Sync through Git

- Connect a workspace to a Git repository and sync it with one shortcut (Cmd+Shift+Y on macOS, Ctrl+Shift+Y elsewhere). Callisto uses the Git you already have, so your SSH keys and sign-in work as usual.
- When two people change the same request, both versions are kept, and a dialog shows what to review.
- Open from Git brings a shared workspace onto this device.
- Secret values, history and settings never leave your device.

### Workspaces

- Create a workspace from the workspace switcher or the command palette, kept in Callisto's app data or in a folder you choose, or open any folder as a workspace.
- The Workspaces section in Settings lists every workspace on this device, where it's kept and how it stands with its Git remote. Open, sync, rename or show the folder of any of them, or remove one from the list, without switching to it. Removing a workspace never touches its folder.
- Sync all syncs every workspace that has a remote in one go, and shows what happened to each.

### Scripts and the collection runner

- Pre-request and test scripts in JavaScript, on a request, a folder or a whole collection: set variables, check the response with tests, and log to the console. The Tests tab shows what passed and what failed.
- Scripts run in a sandbox with no access to your files or network, except `pm.sendRequest`.
- Collections imported from Postman keep their scripts. They come in turned off, so you can read them before they run.
- Run… on a collection or folder sends its requests in order, once or many times, or once for each row of a CSV or JSON file. Watch the results and tests as they come in, stop a run at any time, and export the results as JSON or JUnit XML. Runs don't fill your history.

### History

- Every request you send, grouped by day, with a filter.
- Reopen any entry in a new tab and save it into a collection, or delete entries. Choose how many days and entries to keep.

### Import and export

- **Import** from Postman (collections, environments, globals and data exports), Insomnia, Hoppscotch, Thunder Client, OpenAPI 3.0 and 3.1, Swagger 2.0, HAR and cURL commands.
  - Choose, paste or drop a file; Callisto detects the format.
  - A preview shows what will be created, what's skipped, and which credentials go to the vault instead of into files.
- **Export** collections and environments to Postman, or a whole workspace as a zip. Secret values are never included.
- Copy any request as a cURL command, with secrets hidden unless you ask for them.

### Working in the app

- A command palette (⌘K or Ctrl+K) for every action and every request.
- Keyboard shortcuts throughout, all listed in Settings.
- Tabs that show unsaved changes, can be dragged to reorder, and are kept per workspace.
- A workspace switcher at the top of the sidebar.
- Callisto's own right-click menus for text, editors and responses.
- Light and dark themes, or follow the system.
- A What's new dialog after each update.

### Privacy and updates

- Callisto works offline and sends nothing on its own: requests go out only when you send them.
- At the first launch, Callisto asks once whether to check for new versions automatically. It contacts the update server only if you say yes or check for updates yourself.
- Updates are signed, and Callisto checks the signature before installing.

## About this repository

This repository holds releases only; the source is private. Each release's notes list what changed in that version.
