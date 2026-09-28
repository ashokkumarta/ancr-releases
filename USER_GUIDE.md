<img src="public/logo.svg" alt="a.n.c.r" height="72">

# a.n.c.r — Fast. Local. Reliable.

**User Guide · version 0.8.0**

ancr is a desktop API client for building, sending, testing and sharing API
requests. It works entirely on your own computer: there's no account, no
sign-in and no cloud sync. Your collections, environments and settings are
stored locally. ancr only connects to the APIs you send requests to, plus a
check for new versions of ancr itself.

**What you can do with ancr:**

- Send **HTTP**, **GraphQL**, **Server-Sent Events (SSE)** and **gRPC**
  requests, with full control over query params, headers, body and
  authentication.
- Open live **WebSocket** connections and talk to **MCP servers** (Model
  Context Protocol): browse and call their tools, read resources and get
  prompts.
- Connect to message brokers and event servers (**MQTT**, **Kafka**,
  **Socket.IO**, **AMQP** such as RabbitMQ, and **NATS**): subscribe,
  publish, and watch every message in one timeline.
- Organize everything into collections and folders.
- Use **environments** and `{{variables}}` to switch between setups such as
  local, staging and production.
- Write **pre-request and test scripts**, and **run a whole collection** as a
  test suite with a pass/fail report.
- **Import** from Postman, OpenAPI, WSDL and cURL, and generate **code snippets**
  from any request.
- **Export and import** ancr files to share your work with teammates.

---

## Installing ancr

ancr runs on Windows. To install it:

1. Download the installer, `ancr Setup 0.8.0.exe`, from
   [github.com/ashokkumarta/ancr-releases](https://github.com/ashokkumarta/ancr-releases/releases),
   and run it.
2. If Windows shows _"Windows protected your PC"_, click **More info**, then
   **Run anyway**.
3. Follow the installer. You can choose the install folder.
4. Start ancr from the Start menu or the desktop shortcut.

### Updates

ancr checks for a new version each time it starts. When one is available,
it downloads in the background and a banner offers **Restart to update**.
You can also check at any time with **⚙ → Check for Updates**. If you're
offline, the check just doesn't happen; it never gets in your way.

**⚙ → Automatic updates** (on by default) turns this off: ancr then doesn't
check when it starts, and **Check for Updates** tells you about a new version
and downloads it only if you click **Download**.

With a perpetual [a.n.c.r Pro](#ancr-pro) licence, automatic updates turn
off by themselves once the licence's updates have ended, and stay off: a
newer version wouldn't run Pro, and the one you have keeps working with it.
You can still check and download by hand; the banner says the new version
won't run Pro. A renewed licence turns them back on as you had them.

If you have version 0.1.0, it can't update itself: download the latest
installer once from
[github.com/ashokkumarta/ancr-releases](https://github.com/ashokkumarta/ancr-releases/releases)
and install it over your current version. Your requests and settings are
kept. From then on, updates arrive automatically.

### Uninstalling

Open Windows **Settings → Apps**, find **ancr**, and choose **Uninstall**.

To keep your work, export your workspace first (see
[Sharing your work](#sharing-your-work)).

---

## First launch

The first time ancr opens, a short welcome screen introduces its main
features. Dismiss it to start working. It won't appear again.

ancr remembers the tabs you had open and reopens them the next time you
start the app.

## The main window

- **Header:** the environment switcher (the set of variables currently in
  use), **Manage** to edit environments, and the **⚙** settings menu.
- **Activity bar** (the icon strip on the far left): picks what the sidebar
  shows, one section at a time:
  - **API:** saved HTTP, GraphQL, SSE, gRPC and SOAP requests.
  - **WebSocket:** saved WebSocket connections.
  - **MCP:** saved MCP servers.
  - **Messaging:** saved broker connections (MQTT, Kafka, Socket.IO, AMQP,
    NATS).
  - **History:** the requests you've sent (see [History](#history)).

  Click the section already shown to hide the sidebar, and any section to
  show it again. At the bottom, **{ }** opens the environments and **?** this
  guide.

- **Sidebar:** the chosen section's collections. Drag its right edge to make
  it wider or narrower. ancr remembers the section, the width and whether
  the sidebar is hidden.
- **Main panel:** what you've opened, one tab each (see [Tabs](#tabs)).
  That can be a request and its response, a WebSocket connection, an MCP
  server, a messaging connection, or the details of a collection or folder.
- **Bottom panel:** tabs under the sidebar and main panel.
  - **Logs** is always there: a running log of every request sent,
    connection events and script output. Turn on **Trace** to log full
    requests and responses (headers, params and body) instead of just the
    status line. Click **Clear** to empty the log.
  - A collection run opens in a **Runner** tab, and **⚙ → Diagnostics** in a
    **Diagnostics** tab. Close either with the **×** on its tab.
  - The panel starts collapsed; click the arrow on its header to expand or
    collapse it. Drag its top edge to change its height.
- **Manage** (environments) and **Import** open in a panel over the right
  edge of the window. Press **Escape**, or click outside it, to close it.

### Tabs

Everything you open gets a tab above the main panel, showing its protocol,
its name and, when there are unsaved changes, a dot.

- **Preview tabs:** a single click in the sidebar opens the item in a
  _preview_ tab (its name in italics), which the next item you click
  replaces, so browsing doesn't pile up tabs. A tab is kept once you edit
  it, send it or connect it, or when you double-click the tab. New requests
  and connections, and cURL imports, open in kept tabs.
- **Switching:** click a tab, press `Ctrl+Tab` and `Ctrl+Shift+Tab`, or
  use the arrow keys once a tab has focus.
  Each tab keeps its own edits and response, and a WebSocket or MCP
  connection keeps running while its tab is in the background.
- **Closing:** click **×** on a tab, middle-click it, press **Delete**
  while it has focus, or press `Ctrl+W`. Closing a tab closes its connection. If the tab has
  unsaved changes, ancr asks whether to save them first.
- **Reordering:** drag a tab to a new place.

Deleting an item closes its tab, and renaming it renames the tab.

---

## Workspaces

A **workspace** holds everything you work on: its collections, folders,
requests and connections, its environments, its **History**, cookies and
OAuth 2.0 tokens, its response examples, the tabs you had open and this
session's logs. ancr starts with one, **My Workspace**, and you can add
more, for example one per project or client. One is open at a time, and
ancr reopens the last one you used.

The workspace list is in the header, next to the environments:

- **Switch** by choosing another workspace. Its tabs come back as you left
  them. If a tab has unsaved changes, ancr asks whether to save them first.
- **⋯ → New workspace…** makes an empty one and opens it.
- **⋯ → Rename workspace…** renames the open one.
- **⋯ → Delete workspace…** deletes the open one, with everything in it,
  and opens another. If it's the only workspace, it's emptied instead and
  gets the name **My Workspace** back.

Settings (the theme, **Network…**, History limits) are the same for every
workspace. When you import an ancr export, you choose whether it goes into
the open workspace or a new one.

## Collections and folders

Every saved request, connection and server lives in a **collection**.
Collections can contain **folders**, and folders can contain sub-folders.
Each section starts with one collection: **My Collection** (API),
**My Connections** (WebSocket), **My MCPs** (MCP) and **My Brokers**
(Messaging). You can rename or delete these like any other collection.

**Working with the tree**

- Click the **arrow** next to a collection or folder to expand or collapse
  it.
- Hover over a collection or folder to see its quick actions:
  - **New request / connection / server** here
  - **New folder**
  - **▶ Run** (API only)
  - **Rename**
  - **Delete**

  Every icon has a tooltip.

- Click a collection or folder's **name** to see its details in the main
  panel:
  - its type and creation date
  - how many folders and items it holds
  - a clickable list of its contents
  - buttons for every action: **New**, **New folder**, **Run all** (API),
    **Export**, **Rename** and **Delete**

  In the details view, you can also click the name at the top to rename it.

- The **new collection** icon on a section's header creates a new top-level
  collection. The header also has **import** and **export** icons.
- **Double-click** any name in the tree to rename it.
- **Drag and drop** to:
  - reorder collections or folders among their siblings
  - reorder items within a folder
  - move an item into a different folder of the same section

---

## Building and sending requests

Create a request with the **new request** icon on any API collection or
folder, and click its protocol: **HTTP**, **GraphQL**, **SSE** or **gRPC**
(**Cancel** closes the dialog). It's created at once with a default name,
such as _New HTTP request_; click the name to rename it. The protocol is
fixed once the request is created.

The toolbar above a request shows its name, where it lives, and buttons to
**undo**, **redo**, **rename** and **delete**. Click the name to rename it
in place. A dot next to the name means you have unsaved changes; click
**Save** to keep them. If you close the tab, or close ancr, while changes
are unsaved, ancr asks whether to save them first.

The request tabs are **Params**, **Auth**, **Headers**, a body tab
(**Body**, **Query** or **Message**, depending on the protocol),
**Settings**, **Pre-request Script**, **Tests** and **`</> Code`**. A dot on
a tab means it has content. Click a tab again to close it.

### TLS certificates

ancr checks the server's TLS certificate for every `https://` and `wss://`
connection, and refuses a server whose certificate is self-signed, expired
or issued for another host. The error in **Logs** says why, for example
`self-signed certificate (DEPTH_ZERO_SELF_SIGNED_CERT)`.

To test a server like that, untick **Verify TLS certificates**: on the
**Settings** tab of a request, a WebSocket connection or a messaging
connection, or the **Headers / TLS** tab of an MCP server over HTTP. A
warning shows while it's off, and a dot marks the tab. The connection is
still encrypted, but ancr no longer checks who it's talking to, so only do
this for servers you control, and save it only where you need it.

Importing a cURL command with `-k` or `--insecure`, or a Postman request
with SSL certificate verification off, turns the check off too, and the
**`</> Code`** snippets include each language's equivalent.

### Proxy and client certificates

**Settings** (⚙) → **Network…** sets how ancr reaches servers, for every
request and connection:

- **Proxy.** By default ancr uses the proxy in the `HTTPS_PROXY` or
  `HTTP_PROXY` environment variable, if one is set, except for the hosts in
  `NO_PROXY`. Choose **This proxy** to enter one (`http://proxy.example.com:3128`),
  with a username and password if it needs them, and the hosts to reach
  directly under **No proxy for** (`localhost, .example.com`: a host covers
  its subdomains). **The system's proxy settings** uses the proxy your
  operating system is set up with (on Windows, **Settings → Network &
  internet → Proxy**), including a setup script (PAC) or automatic
  detection, which is how most company networks set it: each request asks
  the system which proxy its address goes through. **No proxy** turns it
  off. HTTP, GraphQL, SSE, WebSocket,
  gRPC and MCP requests go through the proxy, and so do MQTT over WebSocket
  (`ws://`, `wss://`) and Socket.IO; Kafka, AMQP, NATS and MQTT over TCP
  connect directly.
- **Certificate authorities.** Add a CA certificate (PEM) your company signs
  its servers' certificates with, and ancr trusts it as well as the system's,
  so you don't have to turn **Verify TLS certificates** off.
- **Client certificates.** For servers that ask for one (mutual TLS): the
  host it's for, and either a PEM certificate and its key or a PFX / PKCS #12
  file, with its passphrase if it has one. `api.example.com` covers its
  subdomains, `*.example.com` only the subdomains, and `:8443` after a host
  limits it to that port. Every protocol that uses TLS sends it, messaging
  brokers included.

ancr keeps only the files' paths, so the certificates stay where they are.
Passwords and passphrases are encrypted with your system's key store and are
never exported. The settings apply to requests and connections from the next
one you send or open.

### Cookies

ancr keeps cookies the way a browser does. When a response sets a cookie,
it's kept, and sent with later requests to the same site: log in once and
the requests after it are logged in too, including in a collection run.
A cookie goes only to its own domain (and its subdomains, if it says so)
and path, a **Secure** one only over `https://` (or to your own machine),
and it's dropped when it expires or the server clears it. Redirects keep
cookies too, so a cookie set by a login's redirect isn't lost. A cookie with
no expiry is kept until you delete it.

The response's **Cookies** tab shows what that response set. To see every
kept cookie, open **Settings (⚙) → Cookies…** (or **Cookies: Manage** in the
command palette): they're listed by domain, and you can add, edit or delete
one, or delete all of a domain's. Each workspace has its own cookies.

To send a request without them, untick **Use the cookie jar** on its
**Settings** tab: it then sends no kept cookies and keeps none it's given.
A `Cookie` header you add yourself is always sent; for a cookie in both,
yours wins.

### HTTP

1. Pick a method (GET, POST, PUT, PATCH, DELETE, HEAD or OPTIONS) and enter
   the URL.
2. Add **Params** and **Headers** as key/value rows. Untick a row to switch
   it off without deleting it.
3. Choose **Auth**:
   - **No Auth**
   - **Basic Auth** (username and password)
   - **Bearer Token**
   - **API Key**, sent as a header or a query parameter
   - **Digest Auth** (username and password): ancr answers the server's
     Digest challenge and sends the request again
   - **OAuth 2.0**: see [OAuth 2.0](#oauth-20) below
4. Choose a **Body**:
   - **JSON** or **Raw** text
   - **x-www-form-urlencoded** or **Form Data** (key/value rows). In Form
     Data, a row's **Type** can be **File**: choose the file, and it's sent
     as a file part named after the file, with a `Content-Type` from its
     extension.
   - **Binary**: a file, sent as it is. Click **Choose file…**; ancr shows
     its name and size. Only the file's path is saved, and the file is read
     each time you send, so a changed file sends its new contents (and a
     moved one shows **File not found**).

   ancr sets a matching `Content-Type` header for you. For a binary body it
   comes from the file's extension (`.png` sends `image/png`), unless you set
   one in **Headers**.

5. Click **Send**.

The response shows the status, time taken and size, then five tabs:
**Body**, **Headers**, **Tests** (with how many passed), **Cookies** and
**Timing**. Very large responses (over about 500 KB) show a preview of the
body first, with a button to load the full response.

**Body** shows JSON and XML **Pretty** (formatted and coloured) or **Raw** (as
received), and an HTML page as a **Preview** too. The preview runs no
scripts and loads nothing from the network, so it's safe to look at any page.
**Search** marks every match (**Enter** and **Shift+Enter**, or the arrows,
step through them), and **Copy** copies the whole body.

**Cookies** lists the cookies the response set: name, value, domain, path,
when they expire, and their flags (Secure, HttpOnly, SameSite).

**Timing** shows where the time went: **DNS** (looking up the host name),
**Connect**, **TLS** (the secure handshake), **Waiting** (from sending the
request to the first byte of the response) and **Download**. A request that
reused an open connection has no DNS, connect or TLS time.

The request and the response share the main panel. Drag the line between
them to give either more room, and click **Side by side** (or **Stacked**)
to put the response beside the request or under it. ancr remembers both.

### Response examples

To keep a response as an example of what a saved request returns (the
happy path, a 404, an error), click **Save as example** next to its status
and give it a name. Examples are listed under their request in the sidebar
(click the arrow beside the request to show or hide them); click one to
open it in a tab of its own, with its status, headers and body. From there
you can **Rename** or **Delete** it, or go back to its request.

Examples are saved with the request, go with it into exports (with secret
headers such as `Set-Cookie` blanked unless you include secrets), and are
deleted with it. A Postman collection's saved responses import as examples.

### OAuth 2.0

Pick **OAuth 2.0** on the **Auth** tab of an HTTP or GraphQL request, then a
**Grant type**:

- **Authorization code (with PKCE)**, for signing in as a user: fill in the
  provider's **Authorization URL**, **Token URL** and **Client ID** (and
  **Client secret**, unless it's a public client). When there's no token,
  your browser opens the provider's sign-in page; after you sign in, it
  sends you back to ancr on this computer (`http://127.0.0.1`, on a free
  port, unless you give a **Redirect URI**, for a provider that only
  accepts a registered one).
- **Client credentials**, for one service calling another: the **Token URL**,
  **Client ID** and **Client secret**.
- **Password**, for older APIs that take a username and password.

**Scope** and **Audience** are sent if you fill them in. The token goes in
the `Authorization` header as `Bearer …` (change **Header prefix** if the
API wants another word), or in the `access_token` query parameter.
**Send the client ID and secret** chooses how they reach the token URL: as
a Basic auth header (the usual way) or in the request body. Any field can
use `{{variables}}`, so the client secret can live in your environment.

ancr gets a token when you first send the request, keeps it, and uses it
until it expires; then it uses the refresh token, if the provider gave one,
or gets a new token. Requests with the same provider, client and scope share
one token, so you sign in once. Under the settings, **Access token** shows
the token and when it expires, with **Get new access token**, **Copy token**
and **Clear token**. Tokens are kept with the workspace, never in the saved
request, so they're not in exports.

### GraphQL

Write your query in the **Query** tab. Add an operation name if the query
defines more than one operation, and variables as JSON if you need them.
Click **Fetch schema** to load the server's schema and browse its types and
fields while you write. If the server returns GraphQL errors, they're listed
clearly above the response.

### Server-Sent Events (SSE)

Enter the stream URL and click **Connect**. Events appear live as they
arrive. Click **Disconnect** to close the stream.

#### Streaming an AI API's answer

AI APIs (OpenAI, Anthropic, and the many compatible with OpenAI's, such as
local model servers, and Gemini) stream their answers as events in reply to
a POST. To test one, create an **SSE** request, choose **POST**, and on the
**Body** tab write the request as **JSON**, with streaming turned on:

```json
{
  "model": "gpt-4o-mini",
  "stream": true,
  "messages": [{ "role": "user", "content": "Say hello" }]
}
```

Put the API key where the API wants it: **Auth → Bearer Token** for
OpenAI, or an `x-api-key` header (and `anthropic-version`) for Anthropic.
Click **Connect**: above the events, **Answer** shows the text put together
as it arrives, and which API's format it's in. A request without
`"stream": true` gets the whole answer at once; it shows the same way. If
the API refuses the request (a wrong key, an unknown model), the error
shows the API's own explanation.

#### Tokens and cost

When an AI API's answer says how many tokens it used (OpenAI, Anthropic
and Gemini all do), ancr shows them under the answer: input, output and
total, with the model. For OpenAI's streams, ask for them with
`"stream_options": { "include_usage": true }` in the body. It works for a
plain **HTTP** request to an AI API too, under the response's status.

The **cost** is shown when the model is in the price table, **⚙ → AI model
prices…**. It starts with the main OpenAI, Anthropic and Gemini models, at
the prices their price pages gave on the date shown there; prices change,
so check yours. Edit a price, **+ Add model** for any other (a local model,
another provider), or remove one, then **Save**; **Use the starter prices**
goes back to the table ancr came with. A price covers its model's dated
versions too (`claude-haiku-4-5` covers `claude-haiku-4-5-20251001`), but
not other models whose names start the same way. Discounts for prompt
caching and batches aren't counted.

### SOAP

For a SOAP web service, create a **SOAP** request and enter the service's
address. On the **Envelope** tab:

- **SOAP version:** **1.1** sends the envelope as `text/xml` with a
  `SOAPAction` header; **1.2** as `application/soap+xml`, with the action in
  the content type.
- **Action:** the operation's action URI, as the service's WSDL gives it
  (`soapAction`). Some services need it; others ignore it.
- The **envelope** itself, which starts from a template: put the operation
  in its `Body`. `{{variables}}` work here too.

ancr POSTs the envelope. The response body shows as formatted XML, and if
the service answers with a **fault**, its code and reason (and detail) show
above the response. A `Content-Type` or `SOAPAction` header you add yourself
is sent as you wrote it. Code snippets, collection runs and History treat a
SOAP request as the HTTP request it's sent as.

To start from the service's **WSDL** instead, import it (**Import** →
**WSDL (SOAP)**, from its URL or a file): you get a request for each
operation with the address, version and action filled in, and an envelope
with the operation's elements. Each value is a `?` or a sample (`0`, `false`,
a date, an enumeration's first value) to replace; optional elements are
marked `<!--Optional:-->` and repeated ones `<!--One or more:-->`. A service
with both SOAP 1.1 and 1.2 ports gets a folder for each.

### gRPC

1. Enter the server address, e.g. `localhost:50051`.
2. In the **Message** tab, say where the service definitions come from:
   - **Proto file:** paste the service's `.proto` definition (one file,
     without imports).
   - **Server reflection:** click **Load services from the server**, and
     ancr asks the server itself, so you need no `.proto` file. The server
     must have gRPC server reflection turned on (most frameworks have a
     one-line switch for it). **Reload from the server** picks up changes.
3. Pick the service and method. Streaming methods say which kind they are.
4. Fill in the request message using the generated form.
5. Leave **Use plaintext** on for local and development servers, or turn it
   off for servers that use TLS.

For a unary call, the response shows the status code, time taken, the
response message, and any metadata the server sent back.

**Streaming calls** show every message as it goes, **→ Sent** or
**← Received**, and then how the call ended (its status code and name, with
the server's headers and trailers):

- **Server streaming:** **Send** sends the message and the replies arrive
  one by one.
- **Client streaming** and **bidirectional:** **Send** opens the call. Then
  **Send message** sends the message in the form (edit it and send again as
  often as you like), and **End** tells the server you're done. A
  bidirectional call's replies arrive as they come; a client-streaming
  call's one reply comes after **End**.
- **Cancel** stops a call at any time.

---

## WebSocket connections

Create a connection with the **new connection** icon on a WebSocket
collection or folder, then enter its URL (e.g. `wss://example.com/socket`).

- Set up **Auth** and **Headers** as for HTTP requests. Under
  **Subprotocols**, list the subprotocols to offer.
- Click **Connect**. Type a message and press **Enter** (or click
  **Send**).
- Sent and received messages appear in a timeline.
- Click **Save** to keep the connection's settings, and **Disconnect** when
  you're done.

## MCP servers

Create a server with the **new server** icon on an MCP collection or folder.

- Choose how to reach it:
  - **stdio:** ancr starts the server on your computer. Enter the command,
    its arguments and any environment values it needs.
  - **HTTP:** enter the server's URL and any headers it needs.
- Click **Connect**. Then:
  - **Tools:** pick a tool, fill in its arguments and call it.
  - **Resources:** pick a resource and read it.
  - **Prompts:** pick a prompt, fill in its arguments and get it.
  - **Log:** see notifications and connection events.

A stdio server runs as a program on your own computer, so only connect to
servers you trust.

## Messaging connections

Create a connection with the **new connection** icon on a Messaging
collection or folder, and click its kind: **MQTT**, **Kafka**,
**Socket.IO**, **AMQP** (RabbitMQ) or **NATS** (**Cancel** closes the
dialog). It's created at once with a default name, such as _New MQTT
connection_, which you can click to rename, and a local address you can
change:

| Kind              | Address                                                                    | A channel is                               |
| ----------------- | -------------------------------------------------------------------------- | ------------------------------------------ |
| MQTT (3.1.1 or 5) | `mqtt://`, `mqtts://`, `ws://` or `wss://`                                 | a topic (`+` and `#` wildcards)            |
| Kafka             | `kafka://host:9092` (several brokers comma-separated), `kafkas://` for TLS | a topic                                    |
| Socket.IO         | `http(s)://host/namespace`                                                 | an event name (`*` for all of them)        |
| AMQP              | `amqp://` or `amqps://`, the vhost as the path                             | a queue, and a routing key when publishing |
| NATS              | `nats://` or `tls://`                                                      | a subject (`*` and `>` wildcards)          |

- **Auth:** a username and password (**Basic**) for every kind, which
  Kafka sends with SASL, or a token (**Bearer**) for NATS and Socket.IO.
- **Settings:** the kind's own options, such as the MQTT version and client
  ID, Kafka's SASL mechanism, or Socket.IO's path and auth payload, and
  **Verify TLS certificates** (see [TLS certificates](#tls-certificates)).
- **Headers:** sent with the connection's handshake, for Socket.IO and for
  MQTT over `ws://` or `wss://`.
- **Subscriptions:** add a channel with its options (MQTT's QoS, a Kafka
  consumer group or reading from the beginning, an AMQP exchange to bind a
  queue to, a NATS queue group). Subscriptions are saved with the
  connection and made again each time you connect; ● marks the active ones.
  If the broker refuses one, the reason shows next to it.
- **Publish:** enter the channel and the payload, a key (Kafka) and headers
  where the kind has them, and its options (QoS and retain, a partition,
  waiting for a Socket.IO acknowledgement, an AMQP exchange, a NATS request
  that waits for a reply). The result, or the broker's reason for refusing,
  shows under **Publish**.
- **Timeline:** every message sent (↑) and received (↓), with connection
  events. Filter it by channel, and click a message to see its key,
  headers, details (QoS, partition and offset, delivery tag…) and payload,
  with JSON laid out.

A payload that isn't text is shown, and can be sent, as base64. A lost
connection isn't reconnected by itself: the timeline shows it ending, and
**Connect** opens it again. Click **Save** to keep the connection's
settings and subscriptions.

---

## Environments and variables

An **environment** is a named set of variables, for example _Local_,
_Staging_ and _Production_. Pick the active one from the switcher in the
header, or **No Environment**. Click **Manage** to create, rename and delete
environments and edit their variables.

In requests, write `{{variableName}}` anywhere: the URL, params, headers,
body, auth or GraphQL query. When you send, it's replaced with the value
from the active environment. A variable with no value is left as-is, e.g.
`{{typo}}`, so mistakes are easy to spot.

Connections use them too: a WebSocket, MCP or messaging connection's URL,
headers, auth and settings when it connects, and what it sends while
connected (WebSocket messages, MCP arguments, messaging subscriptions and
publishes). The saved connection keeps the `{{variables}}`, so switching
environments points it somewhere else.

**Which variables are set** shows as you type. In the URL, params,
headers, auth, body and SOAP envelope fields, and a connection's URL and
messages, a `{{variable}}` the active environment sets is **green**, with a
dotted underline, and one it doesn't set is **red**, with a wavy underline:
it would be sent as written. Hover over the field to see each variable's
value and where it comes from. Switch environments and the colours follow.
Password fields aren't coloured, so their text stays hidden. A variable a
pre-request script sets shows as red until then, since it only exists
while the request runs.

Scripts can also set variables for a single run (see below).

---

## Pre-request and test scripts

For HTTP and GraphQL requests, you can write JavaScript in the
**Pre-request Script** and **Tests** tabs. It runs before the request is
sent or after its response arrives. Scripts use
the `ancr` object:

```js
// Pre-request script: runs before the request is sent
ancr.variables.token = 'abc123'; // use it in this request as {{token}}

// Test script: runs after the response comes back
ancr.test('status is 200', () => {
  ancr.expect(ancr.response.status).toBe(200);
});

ancr.test('body has the right id', () => {
  ancr.expect(ancr.response.json().id).toBe(42);
});
```

**Checks available on `ancr.expect(value)`:**

- `.toBe()`
- `.toEqual()` (deep equality)
- `.toBeDefined()` and `.toBeUndefined()`
- `.toBeNull()`
- `.toBeTruthy()` and `.toBeFalsy()`
- `.toBeGreaterThan()` and `.toBeLessThan()`
- `.toContain()`
- `.toHaveProperty(key, value?)`

Put `.not` before any check to reverse it, e.g.
`ancr.expect(status).not.toBe(404)`.

**Also available:**

- `ancr.variables`: the active environment's values, as strings, for this
  request. Set a value here to use it as `{{name}}` in this request (its
  test script sees it too). It lasts only for this request.
- `ancr.environment`: the active environment itself. A value set here is
  used by this request too, and is **saved to the environment** afterwards,
  so later requests use it, including the next ones in a collection run.
  `delete ancr.environment.name` removes one. The Logs panel says which
  values changed (never the values themselves), and a collection run's
  summary lists them. With **No Environment** selected there's nowhere to
  save them, so nothing is saved and the log says so.

  ```js
  // Test script of a login request: keep the token for the requests after it.
  ancr.environment.token = ancr.response.json().token;
  ```

- `ancr.cookies`: the [kept cookies](#cookies) for this request's address.
  `ancr.cookies.get("session")` gives a cookie's value, `.has(name)` says
  whether there is one, `.toObject()` gives them all as `{ name: value }`,
  and `.all()` as a list with each one's domain, path, expiry and flags. In
  a test script it includes the cookies this response just set.
- `ancr.request`: the request being sent (read-only: changing it doesn't
  change what's sent; set variables instead).
- `ancr.response`, in test scripts. It has `.status`, `.statusText`,
  `.headers` (names in lower case, e.g. `headers["content-type"]`), `.body`,
  `.sizeBytes`, `.timings` and `.json()` to parse the body (it throws if
  the body isn't JSON). `.timings.durationMs` is the total time, and
  `.timings.phases` has the breakdown the Timing tab shows: `dnsMs`,
  `connectMs`, `tlsMs`, `waitMs`, `downloadMs` and `reusedConnection`.
- `console.log(...)`, and `console.info`, `console.warn` and
  `console.error`: output appears in the **Logs** panel.

The [sample workspace](#trying-the-sample-workspace) has examples of all of
these, in its **Pre-request scripts** and **Scripts & tests** folders.

Test results appear on the response's **Tests** tab as a pass/fail list.

### Tests for connections

WebSocket and messaging connections have a **Tests** tab too, and an SSE
request's **Tests** tab works the same way. There, the script checks the
messages the connection has sent and received so far, `ancr.messages`,
oldest first. Each has:

- `direction`: `"sent"` or `"received"`
- `channel`: the topic, queue, subject or event name (messaging), or the
  event's type (SSE)
- `data`: the message as text, and `json()` to parse it
- `at`: how many milliseconds after the connection opened it came
- `key` and `headers`, for messaging protocols that have them

```js
ancr.test("an order is paid within 5 s", () => {
  const paid = ancr.messages.find((m) => m.channel === "orders" && m.json().status === "paid");
  ancr.expect(paid).toBeDefined();
  ancr.expect(paid.at).toBeLessThan(5000);
});
```

The tests run again as messages arrive, so the results (under the script,
and as a summary on the other tabs) say how the connection is doing so far.
**Run tests now** runs them at once. Only the newest 1,000 messages are
checked, and a reconnect starts afresh. `ancr.request` and `ancr.variables`
are there too; `ancr.response` isn't, since a connection has no single
response.

**Scripts run in a sandbox.** Each script runs in its own small JavaScript
engine, separate from the app. It can use the `ancr` object and `console`,
and nothing else: no files, no network, no timers, and no access to your
other requests or settings. A script that runs longer than 1 second or uses
more than 64 MB of memory is stopped, and the error appears in the request's
results.

Even so, only import scripts from people you trust: a script can still read
this request's variables and response. That's why ancr doesn't bring in
scripts from shared files unless you ask it to.

## Running a collection

Click **▶ Run** on any API collection or folder (in the sidebar or its
details panel). ancr runs every HTTP and GraphQL request inside it,
including sub-folders, in order, using the active environment. You see live progress, then a
report:

- total requests
- tests passed and failed
- requests that failed to send
- total time

### Running with data (Pro)

With an [a.n.c.r Pro](#ancr-pro) licence, the **table** icon next to ▶ Run
(**Run this collection with data**, or folder) runs every request once per
row of test data, or a number of times:

- **A data file:** click **Choose data file…** and pick a CSV file (a header
  row of names, then a row per pass; commas or semicolons, and values in
  quotes where they have a comma or a line break) or a JSON file (an array
  of objects). The first rows are shown before you run.
- **Repeat:** the requests run the number of **Times** you set, with no data.
- **Delay between requests** waits that many milliseconds between one
  request and the next, and **Stop at the first failure** ends the run at
  the first request that fails to send or fails a test. **Stop** ends a run
  part-way.

In each pass, the row's values are `{{variables}}` (above the environment's
values, and never saved to it), and scripts read the pass as
`ancr.iteration` (`index` from 0, `count` and `data`); Postman scripts'
`pm.iterationData.get(name)` and `pm.info.iteration` work too. What scripts
set in `ancr.environment` carries on to the next pass and is saved to the
environment afterwards, as in a normal run.

The results show each iteration with its row's values and each request's
outcome. **Save JUnit XML…** saves them for a CI system (a test suite per
request per iteration) and **Save CSV…** for a spreadsheet (a row per request
per iteration, with a column per data value). Both, and the runner, show
who the licence is for and its id ("Licensed to …"): the JUnit file as each
suite's properties, the CSV file as a last line starting with `#`.

Without a licence the icon still opens the runner, which explains what it
does and how to add a licence.

### Running a collection in CI

To run the same tests in a CI pipeline, without ancr, use `jt`, the
command-line client of jtaak, the open-source engine ancr is built on
(Node.js 22.22 or later). [Export](#exporting) the collection (or the
workspace), then:

```bash
npx jtaak run my-api.ancr.json --format ancr-export --namespace ancr --env CI --junit results.xml
```

`--format` and `--namespace` tell `jt` it's an ancr file whose scripts use
`ancr.`. It runs the requests in order with their scripts, prints each
result, writes the results as JUnit XML (which CI systems show as test
results), and exits with a non-zero code if any test fails. `--env` picks
one of the file's environments; `--var name=value` sets a variable, say a
secret from your CI's settings. See `npx jtaak run --help` for the rest.

---

## Importing from other tools

Click the **import** icon on the **API** section header to open the Import
panel. Paste the content, or click **Choose file…** to load a file; ancr
detects the file type for you. You can import:

- **Postman Collection:** creates a collection with all its folders and
  requests, including their scripts.
- **Postman Environment:** creates an environment with its variables.
- **OpenAPI Spec** (3.x, JSON): creates a collection with one request per
  operation, grouped into folders by tag. Where the spec describes a
  request body, an example body is filled in. Path parameters such as
  `/users/{id}` become `{{id}}`.
- **WSDL (SOAP):** paste the service's WSDL URL (often its address with
  `?wsdl`), or the WSDL itself, or choose a `.wsdl` file. ancr creates a
  collection with a SOAP request per operation: its address, SOAP version,
  action and an envelope to fill in (see [SOAP](#soap)). From a URL or a
  file, the schemas and WSDLs it imports are read too; a pasted WSDL's
  can't be, so those types are left as `?`, and the panel says so.
- **cURL command:** paste a `curl ...` command (for example, copied from
  your browser's developer tools). It opens in the request builder with its
  method, URL, headers, body and auth filled in, ready to save.
- **ancr export:** see [Sharing your work](#sharing-your-work).

Postman scripts are imported as they are, and most run unchanged: scripts
have Postman's common `pm` calls too. That's `pm.test` and `pm.expect`, with
Chai's chains such as `.to.equal`, `.to.have.property` and `.to.be.true`;
`pm.response` with `.to.have.status(200)` and `.to.be.ok`; and
`pm.environment`, `pm.variables`, `pm.request` and `pm.cookies`. A few Postman
calls aren't available, such as `pm.sendRequest` (scripts can't use the
network here) and the old `postman.*` and `tests[...]` forms. After an import,
ancr lists the requests whose scripts use them, and a script that calls one
fails with a message naming it.

## Generating code snippets

Open a request's **`</> Code`** tab to see it as ready-to-use code:

- cURL
- JavaScript (`fetch` or `axios`)
- Python (`requests`)
- Go

Pick a language and click **Copy**.

---

## Sharing your work

Export your work to an **`.ancr.json`** file to share it with a teammate,
keep a backup, or keep it in version control. Exporting the same thing twice
gives the same file, so changes are easy to compare.

### Exporting

You can export at three levels:

- **One collection or folder:** click its name in the sidebar, then click
  **Export** in the details panel. An exported folder becomes its own
  collection in the file.
- **A whole section:** click the **export** icon on the API, WebSocket,
  MCP or Messaging section header.
- **Everything:** **⚙ → Export workspace…** exports every collection in all
  four sections, plus all environments.

The export dialog offers these options:

- **Include secrets** (off by default). While it's off, the file doesn't
  contain passwords, tokens, API keys or OAuth client secrets (OAuth
  access tokens are never in an export). The same goes for any header,
  param or variable whose name suggests a secret: _Authorization_,
  _Cookie_, or names containing _token_, _secret_, _key_, _password_,
  _credential_ or _session_. A value that is only a `{{variable}}` is
  always kept, so your teammate can use their own environment. Secrets
  typed directly into a request body or a script can't be detected, so
  check those yourself.
- **Include environments** (collection and section exports; off by
  default). Turn it on and choose which environments to include. A
  workspace export always includes all environments.

### Importing

- **Into one section:** use the **import** icon on the WebSocket or MCP
  section header. For API collections, use the Import panel, choose
  **ancr export**, and paste or choose the file. Only that section's
  collections are imported.
- **Everything:** **⚙ → Import workspace…**.

Nothing is changed until you confirm. First you see a preview of what will
be added, with these choices:

- **Import environments** (on by default).
- **Import scripts** (off by default). Turn this on only for files from
  people you trust. When it's off, requests are imported without their
  scripts.

The preview also warns you about:

- the commands that imported stdio MCP servers will run on your computer
  when you connect them
- secrets that were removed when the file was exported, which you'll need
  to fill in
- requests that refer to files on the exporter's computer

An import always **adds new copies** and never changes anything already in
your workspace. If a collection or environment with the same name exists,
the copy is named e.g. _Users API (imported)_. An import either completes
fully or changes nothing.

---

## Settings menu (⚙)

- **Theme:** **System** (the default) follows your computer's light or dark
  setting and switches when it does. **Dark** and **Light** keep ancr in one
  theme. **High contrast** is a black theme with white text and bright
  colours, stronger borders and a thicker focus outline, for the most
  legible text (WCAG AAA contrast). Your choice is remembered. Windows'
  own high-contrast themes (Settings → Accessibility → Contrast themes)
  work too: ancr then uses your system's colours.
- **Cookies…:** the cookies ancr keeps between requests; see
  [Cookies](#cookies).
- **Licence…:** add or remove an a.n.c.r Pro licence; see
  [a.n.c.r Pro](#ancr-pro).
- **Export workspace… / Import workspace…:** see
  [Sharing your work](#sharing-your-work).
- **Reload:** reloads the window.
- **Actual Size**, **Zoom In** and **Zoom Out:** change the text size.
- **Toggle Full Screen**
- **Check for Updates**
- **Diagnostics:** shows the ancr version and system details, and any crash
  reports. Crash reports stay on your computer and are never sent anywhere.
  You can open their folder or clear them from here.
- **Help:** opens this guide inside ancr, over the right side of the window (like **?** on the activity bar). It works offline.
  **Search the guide** at the top (or **Ctrl+F**, **⌘F** on a Mac, while
  it's open) finds text in it: every match is highlighted, **Enter** and
  **↓** go to the next, **Shift+Enter** and **↑** to the previous, and
  **Esc** clears the search. **Open the
  online guide** at the top opens the same guide, for your version, in your
  browser; each release publishes its guide at
  [github.com/ashokkumarta/ancr-releases](https://github.com/ashokkumarta/ancr-releases).

## Command palette and keyboard shortcuts

Press `Ctrl+K` (**⌘K** on a Mac) to open the command palette. Type to
search every command, and every saved request, WebSocket connection, MCP
server, messaging connection, collection and folder, by name. The letters you type only need to
appear in order, so _gtus_ finds _Get users_. Use the arrow keys to pick a
result, **Enter** to run or open it, and **Escape** to close the palette.
Each command shows its shortcut, if it has one.

The shortcuts work anywhere in the window, including while you're typing in
a field or an editor. On a Mac, use **⌘** in place of **Ctrl** (Ctrl+Tab
stays Ctrl+Tab).

| Shortcut                          | Command                                     |
| --------------------------------- | ------------------------------------------- |
| `Ctrl+K` or `Ctrl+Shift+P`        | Show all commands                           |
| `Ctrl+Enter`                      | Send the open request                       |
| `Ctrl+S`                          | Save the open request, connection or server |
| `Ctrl+N`                          | New request                                 |
| `Ctrl+W`                          | Close the tab                               |
| `Ctrl+Tab` or `Ctrl+PageDown`     | Next tab                                    |
| `Ctrl+Shift+Tab` or `Ctrl+PageUp` | Previous tab                                |
| `Ctrl+B`                          | Show or hide the sidebar                    |
| `Ctrl+J`                          | Show or hide the bottom panel               |
| `Ctrl+Shift+H`                    | Show History                                |
| `Ctrl+=`                          | Zoom in                                     |
| `Ctrl+-`                          | Zoom out                                    |
| `Ctrl+0`                          | Actual size                                 |
| `F11`                             | Full screen                                 |
| `F1`                              | This guide                                  |

The palette also has commands without shortcuts: closing other or all tabs,
keeping a preview tab, showing each sidebar section, managing environments
and cookies,
importing and exporting, clearing the logs or switching trace mode, the
themes, and Diagnostics.

## Trying the sample workspace

The sample workspace is a ready-made set of requests, connections and
servers covering everything ancr can do, with test scripts on every HTTP
and GraphQL request. Every request goes to a free public test service, so
it works straight away, with no sign-up or keys.

1. Download
   [ancr-sample-workspace.ancr.json](https://github.com/ashokkumarta/ancr-releases/raw/main/samples/ancr-sample-workspace.ancr.json).
   ([What's inside](https://github.com/ashokkumarta/ancr-releases/tree/main/samples).)
2. Open **⚙ → Import workspace…** and choose the file.
3. In the preview, tick **Import scripts**, then click **Import**.
4. Pick **Sample — httpbin** in the environment switcher.

It's added alongside your own work; nothing you already have changes.

## History

The **History** section of the activity bar lists the HTTP, GraphQL and unary
gRPC requests you've sent, newest first and grouped by day, with each one's
status and time (for gRPC, **OK** or the status code). Search by name or URL at the top. Click an entry to open it
in a preview tab, as a copy of the request as it was sent, with its
response; send it again, or change it first. Hover over an entry and click **×** to remove it, or
click **Clear** to remove them all.

**Settings** at the top of History has:

- **Record sent requests:** turn history on or off (it's on by default).
- **Keep the last … requests:** 500 by default; older ones are removed.
- **Store responses:** with this off, only each response's status, time and
  size are kept, not its body or headers.

Requests are kept as written, so `{{variables}}` stay as placeholders and
the values from your environments (which can include tokens) aren't stored.
Collection runs aren't recorded. Like everything else, history stays on your
computer.

## a.n.c.r Pro

a.n.c.r is free for any use, and everything described above stays free.
**Pro** adds what runs automatically and repeatedly, starting with
[data-driven runs](#running-with-data-pro) of a collection. Where the app
offers a Pro feature, it's marked **Pro**.

To turn Pro on, open **⚙ → Licence…** and paste your licence, or choose
**Choose licence file…** and pick the `.ancr-licence` file you were sent.
The panel then shows who it's for, its term, what it includes and when
its updates end. **Remove licence** takes it off this computer.

A licence is one of three kinds:

- **For an organisation:** works on any of its computers, for the number of
  people (seats) it was bought for.
- **For one person:** when you add it, enter the email address it was issued
  to, to activate it.
- **For one computer:** works only on the computer it was issued for. To buy
  one, send the **machine ID** shown in **⚙ → Licence…** (click **Copy**). The
  ID comes from your operating system's own id for the computer, as a hash,
  and changes if the operating system is reinstalled.

- The licence is checked on your computer, with its signature; nothing is
  sent anywhere, and there's no account.
- **Perpetual** licences keep working for good with the versions released
  until their updates end; a newer version asks for a renewed licence.
  **Subscription** and **trial** licences end on their end date.
- If a licence isn't accepted, the panel says why (for example, it's for
  another product, it has ended, this version is newer than its updates, or
  it has been withdrawn).

## Your data and privacy

- Everything you create is stored only on your computer.
- ancr has no telemetry and never sends your data anywhere. It connects
  only to the APIs you send requests to, and to check for ancr updates.
- A Pro licence is checked on your computer; ancr never sends it anywhere.
- To back up your work or move it to another computer, use
  **⚙ → Export workspace…**, then **Import workspace…** on the other
  computer. If you want the backup to include passwords and tokens, turn on
  **Include secrets** when you export.
