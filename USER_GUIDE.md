<img src="public/logo.svg" alt="a.n.c.r" height="72">

# a.n.c.r — Fast. Local. Reliable.

**User Guide · version 0.2.0**

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
- Organize everything into collections and folders.
- Use **environments** and `{{variables}}` to switch between setups such as
  local, staging and production.
- Write **pre-request and test scripts**, and **run a whole collection** as a
  test suite with a pass/fail report.
- **Import** from Postman, OpenAPI and cURL, and generate **code snippets**
  from any request.
- **Export and import** ancr files to share your work with teammates.

---

## Installing ancr

ancr runs on Windows. To install it:

1. Download the installer, `ancr Setup 0.2.0.exe`, from
   [github.com/ashokkumarta/ancr-releases](https://github.com/ashokkumarta/ancr-releases/releases),
   and run it.
2. If Windows shows *"Windows protected your PC"*, click **More info**, then
   **Run anyway**.
3. Follow the installer. You can choose the install folder.
4. Start ancr from the Start menu or the desktop shortcut.

### Updates

ancr checks for a new version each time it starts. When one is available,
it downloads in the background and a banner offers **Restart to update**.
You can also check at any time with **⚙ → Check for Updates**. If you're
offline, the check just doesn't happen; it never gets in your way.

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
  - **API:** saved HTTP, GraphQL, SSE and gRPC requests.
  - **WebSocket:** saved WebSocket connections.
  - **MCP:** saved MCP servers.
  - **History:** the requests you've sent (see [History](#history)).

  Click the section already shown to hide the sidebar, and any section to
  show it again. At the bottom, **{ }** opens the environments and **?** this
  guide.
- **Sidebar:** the chosen section's collections. Drag its right edge to make
  it wider or narrower. ancr remembers the section, the width and whether
  the sidebar is hidden.
- **Main panel:** what you've opened, one tab each (see [Tabs](#tabs)).
  That can be a request and its response, a WebSocket connection, an MCP
  server, or the details of a collection or folder.
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
  *preview* tab (its name in italics), which the next item you click
  replaces, so browsing doesn't pile up tabs. A tab is kept once you edit
  it, send it or connect it, or when you double-click the tab. New requests
  and connections, and cURL imports, open in kept tabs.
- **Switching:** click a tab, or use the arrow keys once a tab has focus.
  Each tab keeps its own edits and response, and a WebSocket or MCP
  connection keeps running while its tab is in the background.
- **Closing:** click **×** on a tab, middle-click it, or press **Delete**
  while it has focus. Closing a tab closes its connection. If the tab has
  unsaved changes, ancr asks whether to save them first.
- **Reordering:** drag a tab to a new place.

Deleting an item closes its tab, and renaming it renames the tab.

---

## Collections and folders

Every saved request, connection and server lives in a **collection**.
Collections can contain **folders**, and folders can contain sub-folders.
Each section starts with one collection: **My Collection** (API),
**My Connections** (WebSocket) and **My MCPs** (MCP). You can rename or
delete these like any other collection.

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
folder. Choose the protocol (**HTTP**, **GraphQL**, **SSE** or **gRPC**) and
give it a name. The protocol is fixed once the request is created.

The toolbar above a request shows its name, where it lives, and buttons to
**undo**, **redo**, **rename** and **delete**. Click the name to rename it
in place. A dot next to the name means you have unsaved changes; click
**Save** to keep them. If you close the tab, or close ancr, while changes
are unsaved, ancr asks whether to save them first.

The request tabs are **Params**, **Auth**, **Headers**, a body tab
(**Body**, **Query** or **Message**, depending on the protocol),
**Pre-request Script**, **Tests** and **`</> Code`**. A dot on a tab means
it has content. Click a tab again to close it.

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
4. Choose a **Body**:
   - **JSON** or **Raw** text
   - **x-www-form-urlencoded** or **Form Data** (key/value rows)

   ancr sets a matching `Content-Type` header for you.
5. Click **Send**.

The response shows the status, time taken and size, then four tabs:
**Body**, **Headers**, **Tests** (with how many passed) and **Timing**. Very
large responses (over about 500 KB) show a preview of the body first, with a
button to load the full response.

**Timing** shows where the time went: **DNS** (looking up the host name),
**Connect**, **TLS** (the secure handshake), **Waiting** (from sending the
request to the first byte of the response) and **Download**. A request that
reused an open connection has no DNS, connect or TLS time.

The request and the response share the main panel. Drag the line between
them to give either more room, and click **Side by side** (or **Stacked**)
to put the response beside the request or under it. ancr remembers both.

### GraphQL

Write your query in the **Query** tab. Add an operation name if the query
defines more than one operation, and variables as JSON if you need them.
Click **Fetch schema** to load the server's schema and browse its types and
fields while you write. If the server returns GraphQL errors, they're listed
clearly above the response.

### Server-Sent Events (SSE)

Enter the stream URL and click **Connect**. Events appear live as they
arrive. Click **Disconnect** to close the stream.

### gRPC

1. Enter the server address, e.g. `localhost:50051`.
2. In the **Message** tab, paste the service's `.proto` definition.
3. Pick the service and method.
4. Fill in the request message using the generated form.
5. Leave **Use plaintext** on for local and development servers, or turn it
   off for servers that use TLS.

The response shows the status code, time taken, the response message, and
any metadata the server sent back.

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

---

## Environments and variables

An **environment** is a named set of variables, for example *Local*,
*Staging* and *Production*. Pick the active one from the switcher in the
header, or **No Environment**. Click **Manage** to create, rename and delete
environments and edit their variables.

In HTTP and GraphQL requests, write `{{variableName}}` anywhere: the URL,
params, headers, body, auth or GraphQL query. When you send, it's replaced
with the value from the active environment. A variable with no value is left as-is, e.g. `{{typo}}`, so
mistakes are easy to spot.

Scripts can also set variables for a single run (see below).

---

## Pre-request and test scripts

For HTTP and GraphQL requests, you can write JavaScript in the
**Pre-request Script** and **Tests** tabs. It runs before the request is
sent or after its response arrives. Scripts use
the `ancr` object:

```js
// Pre-request script: runs before the request is sent
ancr.variables.token = "abc123";   // use it in this request as {{token}}

// Test script: runs after the response comes back
ancr.test("status is 200", () => {
  ancr.expect(ancr.response.status).toBe(200);
});

ancr.test("body has the right id", () => {
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

- `ancr.variables`, also available as `ancr.environment`: set a value here
  to create a variable for this run.
- `ancr.request`: the request being sent (read-only: changing it doesn't
  change what's sent; set variables instead).
- `ancr.response`, in test scripts. It has `.status`, `.headers`, `.body`,
  `.timings`, and `.json()` to parse the body.
- `console.log(...)`: output appears in the **Logs** panel.

Test results appear on the response's **Tests** tab as a pass/fail list.

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
- **cURL command:** paste a `curl ...` command (for example, copied from
  your browser's developer tools). It opens in the request builder with its
  method, URL, headers, body and auth filled in, ready to save.
- **ancr export:** see [Sharing your work](#sharing-your-work).

Postman scripts are imported as they are. Scripts that use Postman's own
`pm.*` commands need small edits to use `ancr.test` and `ancr.expect`.

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
- **A whole section:** click the **export** icon on the API, WebSocket or
  MCP section header.
- **Everything:** **⚙ → Export workspace…** exports every collection in all
  three sections, plus all environments.

The export dialog offers these options:

- **Include secrets** (off by default). While it's off, the file doesn't
  contain passwords, tokens or API keys. The same goes for any header,
  param or variable whose name suggests a secret: *Authorization*,
  *Cookie*, or names containing *token*, *secret*, *key*, *password*,
  *credential* or *session*. A value that is only a `{{variable}}` is
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
the copy is named e.g. *Users API (imported)*. An import either completes
fully or changes nothing.

---

## Settings menu (⚙)

- **Theme:** **System** (the default) follows your computer's light or dark
  setting and switches when it does. **Dark** and **Light** keep ancr in one
  theme. Your choice is remembered.
- **Export workspace… / Import workspace…:** see
  [Sharing your work](#sharing-your-work).
- **Reload:** reloads the window.
- **Actual Size**, **Zoom In** and **Zoom Out:** change the text size.
- **Toggle Full Screen**
- **Check for Updates**
- **Diagnostics:** shows the ancr version and system details, and any crash
  reports. Crash reports stay on your computer and are never sent anywhere.
  You can open their folder or clear them from here.
- **Help:** opens this guide inside ancr, over the right side of the window (like **?** on the activity bar). It works offline. **Open the
  online guide** at the top opens the same guide, for your version, in your
  browser; each release publishes its guide at
  [github.com/ashokkumarta/ancr-releases](https://github.com/ashokkumarta/ancr-releases).

## History

The **History** section of the activity bar lists the HTTP and GraphQL
requests you've sent, newest first and grouped by day, with each one's
status and time. Search by name or URL at the top. Click an entry to open it
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

## Your data and privacy

- Everything you create is stored only on your computer.
- ancr has no telemetry and never sends your data anywhere. It connects
  only to the APIs you send requests to, and to check for ancr updates.
- To back up your work or move it to another computer, use
  **⚙ → Export workspace…**, then **Import workspace…** on the other
  computer. If you want the backup to include passwords and tokens, turn on
  **Include secrets** when you export.
