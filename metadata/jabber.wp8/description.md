An XMPP (Jabber) chat client for **Windows Phone 8.1**, written against the
**Silverlight 8.1** app model.

Tested against xabber.org, talking to Conversations on Android and to UWPX on
Windows 10 Mobile.

## What works

- Connect: TCP, STARTTLS, SASL PLAIN, resource binding, legacy session
- Roster and live presence, with an availability dot per contact
- Send and receive chat messages
- Send pictures (from the library or the camera) via XEP-0363 HTTP upload
- Received image links render inline; any link in a message is tappable
- Presence subscriptions in both directions: accept/decline incoming requests, and
  add a contact (which sends one)
- Rename a contact by long-pressing it — a server-side roster rename, so it follows
  the account to other clients
- Toast notifications for messages that arrive while the app is in the background;
  tapping one opens that conversation
- Keeps running in the background (see below), plus a periodic agent that checks for
  messages when the app is not running at all
- Editable account, and a settings switch to turn background mode off

## Not implemented

- **No end-to-end encryption.** The connection is TLS-protected; message content is
  not encrypted. No OMEMO.
- No group chat (MUC)
- **Message history is in memory only** — closing the app loses the conversation.
  The roster survives; the messages do not.
- No account backup/export, no contact removal, single account only

## Things worth knowing before changing this

**Stanza ids must be unique across sessions, not just within one.** `NextId()` uses a
random per-connection prefix plus a counter. It originally used a bare counter, so the
third message of every session was `jw3` — and receivers that key stored messages on
the sender's stanza id (UWPX uses id + chat id as a primary key, written with
`InsertOrReplace`) silently *overwrote* an older message instead of adding a new one.
The far end stopped showing new messages while notifications still arrived.

**The stream restarts after STARTTLS and after SASL.** Each restart is a brand new XML
document and needs a fresh `DataReader`/`DataWriter`; the parser buffer is reset too.
Getting this wrong is the usual reason a hand-written XMPP client hangs after auth.

**The stream parser is hand-written** because an XMPP session is one XML document that
never ends, so `XDocument.Load` would block forever. It splits on tag boundaries,
respecting quoted attributes, and treats the unclosed `<stream:stream>` header as a
special case. Each stanza is then parsed inside a synthetic root that declares the
`stream` and `jabber:client` namespaces, without which fragments like
`<stream:features>` do not parse.

**Toasts never appear while the app is in the foreground** — the platform suppresses an
app's own toasts. They are a background feature, so testing them means backgrounding
the app.

**A second resource confuses some clients.** The agent's short-lived `-bg` session
broadcasts available then unavailable on every run. Clients that collapse presence to
the bare JID and take the last stanza will show this account as *offline* while the
foreground session is still connected. That was a bug in UWPX (since fixed there by
tracking presence per resource), but other clients may behave the same way.

**Choosers must be constructed in the page constructor.** `PhotoChooserTask` takes the
app away and the page can be recreated before the result arrives, so a handler attached
later never fires.

**Back-stack handling is deliberate.** `ContactsPage` clears the back stack on arrival,
so it is always the app's root: BACK there leaves the app rather than returning to the
login page. `ChatPage` overrides `OnBackKeyPress` and redirects to the contact list when
it has nothing to go back to, which is the case when a toast deep-linked straight into
a conversation.

**Accepting a subscription also requests one back.** Subscriptions are one-directional;
answering `subscribed` alone would let the contact see you while they stayed
permanently "offline" in your list.

--- 

### See also:

- [4PDA]() 
- [GitHub]()