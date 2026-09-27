# ancr samples

## Sample workspace

**[`ancr-sample-workspace.ancr.json`](./ancr-sample-workspace.ancr.json)** is a
ready-made workspace for exploring everything ancr can do. Every request
points at a free public test service, so it all works straight after
importing, with no sign-up or API keys.

### Importing it

1. Download [`ancr-sample-workspace.ancr.json`](https://github.com/ashokkumarta/ancr-releases/raw/main/samples/ancr-sample-workspace.ancr.json).
2. In ancr, open **⚙ → Import workspace…** and choose the file.
3. In the preview, tick **Import scripts**. Every HTTP and GraphQL sample
   has test scripts, and some have pre-request scripts; they're left out
   unless you tick this.
4. Click **Import**, then pick **Sample — httpbin** in the environment
   switcher.

Everything is added alongside your own work. Nothing you already have is
changed.

### What's inside

| Section | Collection | What it shows |
|---|---|---|
| API | **Sample — HTTP** (45 requests) | See the breakdown below. |
| API | **Sample — GraphQL** (7) | See the breakdown below. |
| API | **Sample — Server-Sent Events** (2) | Named events with ids; a busy live stream (Wikimedia recent edits). |
| API | **Sample — gRPC** (6) | See the breakdown below. |
| WebSocket | **Sample — WebSocket** (4) | Echo servers, plus connections with custom headers and a bearer token. Connect, send a message, and watch it echo back. |
| MCP | **Sample — MCP** (3) | See the breakdown below. |

**Sample — HTTP** covers:

- every method: GET, POST, PUT, PATCH, DELETE, HEAD and OPTIONS
- query params and headers, including disabled rows
- `{{variables}}` in the path, params and headers
- JSON, raw text, urlencoded and multipart bodies
- Basic, Bearer and API-key auth, sent as a header or in the query string
- 401, 404, 500 and 418 responses, redirects, a slow response, a large
  (~1 MB) response, and HTML and XML responses
- a full REST CRUD set (list, get, create, update, delete) on
  JSONPlaceholder
- **Pre-request scripts:** generating values (a timestamp, a random id, a
  number computed from the environment), a value that depends on the
  environment, an `Authorization` header built from variables, and logging
  the request before it's sent
- **Keeping values in the environment:** a login that keeps a token in
  the environment, a request that uses it, a counter that goes up on every
  send, and a logout that removes the token. Send them in order, or run
  the folder
- **Scripts & tests:** every `ancr.expect()` matcher on one response,
  checking every item in a list, response headers, size and timing (with the
  DNS, connect, TLS, wait and download phases the Timing tab shows), and a
  test that fails on purpose
- a test on every request, from checking the status to checking what the
  server echoed back

**Sample — GraphQL** covers:

- simple queries, and queries with variables
- picking one of several operations by name
- nested fields and filters
- an error response, and a test that checks it
- pagination
- a test on every request, including checks for GraphQL errors
- all against the Countries and Rick and Morty APIs; use **Fetch schema**
  to browse them

**Sample — gRPC** covers:

- a plaintext call and a TLS call
- an empty request
- a message using every field type: strings, numbers, enums, nested and
  repeated messages, booleans and floats
- request metadata
- an error status
- all against the public grpcb.in server

**Sample — MCP** covers:

- the reference "Everything" server, which has tools, resources and
  prompts
- the Memory server
- the remote DeepWiki server

Two environments come with it: **Sample — httpbin** and
**Sample — Postman Echo**. Switch between them to send the same requests
to a different server.

### Things to try

- **Tabs:** click a few requests. A single click opens a preview tab (in
  italics) that the next click replaces; send a request, or double-click
  its tab, to keep it. Connect a WebSocket sample, then switch to another
  tab: it stays connected in the background.
- **Command palette:** press `Ctrl+K` (**⌘K** on a Mac) and type part of a
  sample's name, e.g. *every matcher*.
- **Collection runner:** run **Sample — HTTP** to send every request and
  see all the test results in one place.
- **Timing:** send **Scripts & tests → Response headers, size and timing**
  and open the response's **Timing** tab. Send it again: the connection is
  reused, so DNS, connect and TLS drop to 0. Its test script logs the same
  numbers.
- **History:** everything you send is in the activity bar's **History**.

### Good to know

- The local MCP servers need [Node.js](https://nodejs.org). The first time
  you connect one, it's downloaded automatically, which can take a minute.
- The sample credentials (`ancr-user`, `sample-token`, `sample-api-key`,
  and so on) are placeholders that the public test services accept. They
  aren't real accounts.
- **Scripts & tests → "A failing test (on purpose)"** is meant to fail, so
  you can see what a failed test looks like. Every other test passes
  against both environments.
- Scripts run for HTTP and GraphQL requests, so the SSE, gRPC, WebSocket
  and MCP samples have none.
- A value a script sets in `ancr.variables` is used by that request only.
  One set in `ancr.environment` is saved to the environment you picked, so
  **Keeping values in the environment** adds `sessionToken`, `loggedInAt`
  and `callCount` to it (the logout removes the first two).
- These are free public services run by others. If one is slow or briefly
  unavailable, try again later, or switch to the other environment.
