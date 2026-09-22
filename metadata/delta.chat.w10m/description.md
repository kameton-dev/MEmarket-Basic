# DeltaChat for Windows 10 Mobile

A [Delta Chat](https://delta.chat) client for Windows 10 Mobile (Lumia and friends,
build 14393 and later), written in C# as a UWP app.

The starting point was the Miranda NG
[DeltaChat protocol plugin](https://github.com/miranda-ng/miranda-ng/tree/master/protocols/DeltaChat).
That plugin is a thin wrapper over the Rust `deltachat-core` C library, and there is no
build of that library for ARM32 Windows 10 Mobile. So this repository contains two
things:

* **`src/DeltaChat.Core`** — the plugin's logic translated to C#, plus a from-scratch
  implementation of the part of deltachat-core it calls: IMAP, SMTP, MIME, OpenPGP with
  Autocrypt, the Delta Chat chat-mail header protocol, SecureJoin, the Autocrypt Setup
  Message, read receipts, reactions, editing and deleting, and a small JSON store.
  It targets `netstandard1.4`, the ceiling for Windows 10 Mobile, and has no dependency
  apart from Portable.BouncyCastle (used only for SHA/AES/RSA/X25519/Ed25519 primitives;
  all OpenPGP packet handling is in `Pgp/`).
* **`src/DeltaChat.W10M`** — the phone UI: chat list, chat view with bubbles, reply,
  reactions, files, groups, contact verification with QR codes (shown and scanned),
  settings, live tiles, toasts and background fetching.

It talks to current Delta Chat (tested against Delta Chat core 2.60 through
`deltachat-rpc-server`) and to GnuPG.

## Status

Working, verified end to end against a genuine Delta Chat peer over a chatmail relay
(`nine.testrun.org`) with a Gmail account on this side:

* sign in with address and password, or with a `DCACCOUNT:` / `DCLOGIN:` code
* first contact via SecureJoin (paste or scan the other side's invite link / QR, or show
  your own) — the contact ends up *verified* on both sides
* end-to-end encrypted 1:1 and group chats in both directions, with padlocks and
  read receipts
* reactions, edits, "delete for everyone", forwarding, files and images
* Autocrypt Setup Message export/import (key transfer to/from another Delta Chat)
* **"Add second device"**: import a whole account — address, key, contacts and chats —
  from another Delta Chat over the local Wi-Fi, by scanning or pasting its
  Settings → Add Second Device code (`DCBACKUP…`). Verified end to end against genuine
  Delta Chat 2.60, including a real Android phone as the source.
* background fetching (15-minute timer, or a held extended-execution session on
  "always")
* **Interface languages**: English, Russian, Ukrainian and Hebrew — the last mirrors the
  whole layout right-to-left. Chosen in Settings → Language.

Not done: calls, webxdc apps, multi-account, IMAP folder configuration beyond INBOX
and the spam folder, and anything else the Miranda plugin does not do either.

### Add second device — what it involves

Delta Chat transfers the backup over **iroh** (a QUIC connection authenticated by the
device's node key, with an iroh "disco" ping first), and Windows 10 Mobile has none of
that stack — no QUIC, no TLS 1.3, and no SQLite to read the account it hands over. So
`DeltaChat.Core/Transfer` and `DeltaChat.Core/Tls` implement, on top of a UDP/TCP socket
and BouncyCastle primitives:

* **TLS 1.3** (RFC 8446) — the full 1-RTT handshake with X25519, AES-GCM records and
  certificate verification, used both for the QUIC transfer and (see below) for chatmail
  relays that no longer accept TLS 1.2;
* **QUIC** (RFC 9000/9001) — enough of a client to fetch one stream: the handshake over
  Initial/Handshake packets, 1-RTT with header protection, ACKs, loss recovery and
  flow-control pacing so a phone-sized receiver is not overrun;
* **iroh** node identity — the libp2p-style self-signed node-key certificate and the
  "disco" crypto_box ping/pong (X25519 + HChaCha20 + XChaCha20-Poly1305, all by hand);
* a read-only **SQLite** file reader, to turn the `dc_database_backup.sqlite` the peer
  sends into this app's own store (contacts with their keys and verification, chats,
  messages, reactions).

Both devices must be on the same Wi-Fi with client-to-client traffic allowed (no AP
isolation). The manifest declares `privateNetworkClientServer` for it.

## Notes on talking to today's Delta Chat

Things learned the hard way while making this interoperate with Delta Chat 2.x; they
explain some choices in `Sync/`:

* Chatmail relays refuse unencrypted mail. The only plaintext they let through is the
  SecureJoin `vc-request`, and only in the exact shape Delta Chat sends it (a
  `multipart/mixed` with a single `text/plain` part). Delta Chat 2.x will also not
  write an unencrypted message to a contact whose key it does not have. So the first
  contact between two accounts practically has to be a QR/invite-link SecureJoin,
  which is why the app pushes the "Verify contact" flow before "New chat by address".
* Delta Chat 2.x puts its `Autocrypt` header only inside the encrypted part. The
  receiver has to try the inner header's key for signature verification.
* On SecureJoin steps Delta Chat looks in `Autocrypt-Gossip` for the recipient's own
  key and checks the OpenPGP *Intended Recipient* signature subpacket; both are
  therefore always produced.
* Gmail files the relay's handshake and first messages under Spam. The IMAP loop
  looks for the `\Junk` folder (LIST special-use, falling back to names) and moves
  chat mail it finds there back to INBOX. A Gmail filter "from contains
  `nine.testrun.org` → never send to spam" avoids the round trip entirely.
* Root certificates: Windows 10 Mobile's store predates Let's Encrypt's ISRG roots,
  so both are declared in the manifest (`Assets/Certificates`) and installed with the
  app.
* TLS 1.3: chatmail relays (`nine.testrun.org` and others) no longer accept TLS 1.2,
  which is all Windows 10 Mobile's Schannel speaks. When the system handshake fails the
  connection is remade in the clear and the library's own TLS 1.3 (`Tls/`) runs over it;
  a Settings toggle forces it. The trust decision is still the phone's certificate store
  (plus the built-in ISRG anchors) via `PlatformCertificateVerifier`.
* The UDP receive loop must survive a Windows ICMP "connection reset" (WSAECONNRESET
  from a port-unreachable): left unhandled it kills the socket read and the QUIC transfer
  stalls silently. Disable `SIO_UDP_CONNRESET` and keep reading.

## License

GPL-2.0-or-later, like the Miranda NG plugin it is derived from. See `LICENSE`.

### See also:

- [4PDA](https://4pda.to/forum/index.php?showtopic=1126266) 
- [GitHub](https://github.com/Symnok/DeltaChatW10M/tree/main)