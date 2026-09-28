# ancr samples

## Sample workspace

**[`ancr-sample-workspace.ancr.json`](./ancr-sample-workspace.ancr.json)** is
a ready-made workspace for exploring everything ancr can do. Every request
points at a free public test service, so it all works straight after
importing, with no sign-up or API keys. The one exception is the four local
messaging brokers, which you start with Docker.

### Importing it

1. Download [`ancr-sample-workspace.ancr.json`](https://github.com/ashokkumarta/ancr-releases/raw/main/samples/ancr-sample-workspace.ancr.json).
2. In ancr, open **⚙ → Import workspace…** and choose the file. To keep it
   apart from your own work, choose **Into a new workspace**: switch between
   them from the workspace list in the header.
3. In the preview, tick **Import scripts**. Every HTTP and GraphQL sample
   has test scripts, and some have pre-request scripts; they're left out
   unless you tick this.
4. Click **Import**, then pick **Sample — httpbin** in the environment
   switcher.

Everything is added alongside your own work. Nothing you already have is
changed.

### What's inside

| Section   | Collection                             | What it shows                                                                                                            |
| --------- | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| API       | **Sample — HTTP** (56 requests)        | See the breakdown below.                                                                                                 |
| API       | **Sample — GraphQL** (7)               | See the breakdown below.                                                                                                 |
| API       | **Sample — Server-Sent Events** (3)    | Named events with ids, and the same with tests on what arrives; a busy live stream (Wikimedia recent edits).                                                      |
| API       | **Sample — gRPC** (10)                  | See the breakdown below.                                                                                                 |
| API | **Sample — SOAP** (3) | See the breakdown below. |
| API | **Sample — AI APIs** (4) | See the breakdown below. |
| WebSocket | **Sample — WebSocket** (5)             | Echo servers, plus connections with custom headers and a bearer token, and one whose URL is a `{{variable}}`, with tests on what comes back. Connect, send a message, and watch it echo back.  |
| MCP       | **Sample — MCP** (3)                   | See the breakdown below.                                                                                                 |
| Messaging | **Sample — Messaging** (9 connections) | MQTT, Kafka, Socket.IO, AMQP and NATS: five public test broker connections that work straight away (one with tests on what arrives), and four local ones. See below. |

**Sample — HTTP** covers:

- every method: GET, POST, PUT, PATCH, DELETE, HEAD and OPTIONS
- query params and headers, including disabled rows
- `{{variables}}` in the path, params and headers
- JSON, raw text, urlencoded and multipart bodies
- **Files:** a binary body, and a multipart form with a file field, both
  sending [`sample-upload.txt`](https://github.com/ashokkumarta/ancr-releases/raw/main/samples/sample-upload.txt).
  A file's path is kept as it was, so after importing, download it (or use
  any file of yours) and choose it on the request's **Body** tab
- **Data-driven runs (Pro):** the folder **Data-driven run** looks up a
  user by `{{userId}}` and checks their `{{username}}`, both from
  [`sample-users.csv`](https://github.com/ashokkumarta/ancr-releases/raw/main/samples/sample-users.csv)
  (five rows). With a Pro licence, click the table icon on the folder,
  choose the file and run it: each row is one iteration, and its tests read
  the row as `ancr.iteration.data` (one written for Postman uses
  `pm.iterationData`). Run once without data, it fails, since `{{userId}}`
  has no value
- **Response examples:** **REST CRUD → Get one post** keeps two, *Found*
  and *Not found*, under it in the sidebar: click the arrow beside it
- Basic, Bearer and API-key auth, sent as a header or in the query string;
  Digest auth; OAuth 2.0 client credentials (set `oauthTokenUrl`,
  `oauthClientId` and `oauthClientSecret` in the environment for your
  provider); and a client certificate (mutual TLS, see *Things to try*)
- **Cookies:** a response that sets a cookie (through a redirect), a
  request that sends it back, and one with the cookie jar turned off
- a test script written for Postman (`pm.test`, `pm.expect`,
  `pm.response`), which runs as written
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
- server streaming, client streaming and bidirectional calls: send, send
  messages, **End**, and watch the replies
- a request with no `.proto`: it loads the service from the server itself
  (server reflection); click **Load services from the server**
- all against the public grpcb.in server

**Sample — SOAP** covers:

- a SOAP 1.1 call and a SOAP 1.2 call, each with its action, to a public
  calculator service
- a fault (dividing by zero), shown with its code and reason

**Sample — AI APIs** covers:

- streaming an answer from OpenAI's chat completions and from Anthropic's
  Messages API: an SSE request that POSTs a JSON body, with tests that
  pass once the stream has ended: **Answer** shows the text as it arrives, with the tokens used and their cost
- the same OpenAI request, not streamed, as a plain HTTP request, which shows its tokens and cost under the response
- a local model through Ollama's OpenAI-compatible API, which needs no key
  (`ollama run llama3.2` first)

They need your own API keys: set `openaiApiKey` and `anthropicApiKey` in
the environment (they're empty in the sample, and exports leave keys out).
`openaiBaseUrl`, `anthropicBaseUrl` and `localModelUrl` point the same
requests at another compatible service. Without a key, the error shows the
API's own explanation.

**Sample — MCP** covers:

- the reference "Everything" server, which has tools, resources and
  prompts
- the Memory server
- the remote DeepWiki server

Two environments come with it: **Sample — httpbin** and
**Sample — Postman Echo**. Switch between them to send the same requests
to a different server.

**Sample — Messaging** covers every messaging protocol:

- **Public test brokers**, which work straight away: the Mosquitto test
  broker over MQTT 3.1.1 and over WebSocket with TLS (`wss://`), HiveMQ's
  public broker over MQTT 5, and the NATS demo server. Each subscribes to
  `ancr-sample/#` (NATS: `ancr.sample.>`), so publish to, say,
  `ancr-sample/hello` and watch it come back. These brokers are shared with
  everyone: don't send anything private.
- **Local brokers** for Kafka, RabbitMQ, NATS and a Socket.IO server, with
  their subscriptions set up: reading a Kafka topic from the beginning,
  declaring a RabbitMQ queue and binding a private one to `amq.topic`, and
  a NATS queue group. Start the brokers with Docker (or Podman):

  ```
  docker run -d --name kafka -p 9092:9092 apache/kafka-native:4.1.0
  docker run -d --name rabbitmq -p 5672:5672 rabbitmq:4-alpine
  docker run -d --name nats -p 4222:4222 nats:2.11-alpine
  ```

  (RabbitMQ's `guest` user only signs in from the broker's own machine,
  which a port published on localhost counts as.) For Socket.IO, point the
  connection at your own server.

### Things to try

- **Tabs:** click a few requests. A single click opens a preview tab (in
  italics) that the next click replaces; send a request, or double-click
  its tab, to keep it. Connect a WebSocket sample, then switch to another
  tab: it stays connected in the background.
- **Command palette:** press `Ctrl+K` (**⌘K** on a Mac) and type part of a
  sample's name, e.g. _every matcher_.
- **Collection runner:** run **Sample — HTTP** to send every request and
  see all the test results in one place.
- **Timing:** send **Scripts & tests → Response headers, size and timing**
  and open the response's **Timing** tab. Send it again: the connection is
  reused, so DNS, connect and TLS drop to 0. Its test script logs the same
  numbers.
- **History:** everything you send is in the activity bar's **History**.
- **Connection tests:** connect **Sample — WebSocket → Echo via
  {{wsEchoUrl}}, with tests** and send a message: its **Tests** tab goes
  from failing to passing as the echo arrives.
- **Variables:** type `{{nope}}` in a URL: it turns red, since the
  environment doesn't set it; `{{baseUrl}}` is green.
- **A client certificate (mutual TLS):** **Authentication → Client
  certificate** calls badssl.com's test server, which answers 400 until you
  send it a certificate. Download
  [`badssl.com-client.pem`](https://badssl.com/certs/badssl.com-client.pem)
  (the certificate and its key in one file, passphrase `badssl.com`), then
  open **⚙ → Network…**, add a client certificate for host
  `client.badssl.com` (PEM, choosing that file as both the certificate and
  the key, with the passphrase), **Save**, and send it again: 200.
- **AI answers, tokens and cost:** set `openaiApiKey` in the environment
  and connect **Sample — AI APIs → OpenAI: stream a chat completion**. The
  answer appears as it's written, then the tokens it used and what they
  cost, from **⚙ → AI model prices…** (add a model there to price it).
- **Workspaces:** make a second one from the header's workspace list
  (**⋯ → New workspace…**) and switch back: each keeps its own requests,
  environments, history and open tabs.
- **Save a response as an example:** send any request, click **Save as
  example**, and find it under the request in the sidebar.
- **A SOAP service from its WSDL:** open **Import → WSDL (SOAP)** and paste
  `http://www.dneonline.com/calculator.asmx?WSDL`: you get the calculator's
  four operations for SOAP 1.1 and 1.2, each with its envelope ready to
  fill in.
- **A proxy:** **⚙ → Network…** uses the proxy in `HTTPS_PROXY` if one is
  set, the system's proxy settings (a PAC script included), or one you
  enter there.

### Good to know

- The local MCP servers need [Node.js](https://nodejs.org). The first time
  you connect one, it's downloaded automatically, which can take a minute.
- The sample credentials (`ancr-user`, `sample-token`, `sample-api-key`,
  and so on) are placeholders that the public test services accept. They
  aren't real accounts.
- **Scripts & tests → "A failing test (on purpose)"** is meant to fail, so
  you can see what a failed test looks like. **Authentication → Client
  certificate** fails too until you add its certificate, the two file
  requests until you choose the file, and **Sample — AI APIs** until you
  give it your API keys (or run Ollama for the local model). Every other
  test passes against both environments.
- Scripts run for HTTP and GraphQL requests, so the SSE, gRPC, WebSocket
  and MCP samples have none.
- A value a script sets in `ancr.variables` is used by that request only.
  One set in `ancr.environment` is saved to the environment you picked, so
  **Keeping values in the environment** adds `sessionToken`, `loggedInAt`
  and `callCount` to it (the logout removes the first two).
- These are free public services run by others. If one is slow or briefly
  unavailable, try again later, or switch to the other environment.
