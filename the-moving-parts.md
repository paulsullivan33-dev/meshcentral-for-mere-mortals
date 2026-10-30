# The Moving Parts

By the end of this chapter you can name
every part a later chapter touches — the
server, its data folder, the certificates,
the agent, the settings file, the device
group — and say which part holds what.
The check: when chapter 14 says "the
agent refused the certificate", you will
know exactly which two parts are arguing.

## The server

MeshCentral itself is a program written
for **Node.js** — the same JavaScript
runtime that powers a great many web
tools. You install it with npm, Node's
package manager, and you run it with one
command. It is the only part that needs
to be reachable: it listens on port
**443** (HTTPS) for browsers and agents
alike, on port **80** just to redirect
visitors to the secure address, and —
for the Intel AMT hardware features this
guide does not teach — on port 4433.

Everything the server knows lives in one
folder it creates beside itself:
**`meshcentral-data`**. Inside it:

- **`config.json`** — the server's
  settings. One setting matters before
  all others: the server's **name**
  (`settings.cert`), the name its
  certificates are made for. Chapter 3
  explains why you set it first and
  transcript t08 shows what happens if
  you don't.
- **The databases** — plain files
  (`meshcentral.db`, `meshcentral-events.db`
  and friends) holding the accounts, the
  groups, the machines and the event log.
- **The certificates** — the subject of
  the next section.

Backing up that one folder backs up the
console: accounts, groups, machines and
the keys they trust. Protecting it
protects all of it, too.

## The certificates

On its first run the server makes itself
a small family of certificates, all
self-signed — signed by the server's own
private **root certificate**, which it
also generates:

- the **web certificate**, presented to
  browsers on port 443;
- the **agent certificate**, the identity
  agents check;
- an **MPS certificate** for Intel AMT,
  and a **code-signing certificate** used
  to sign the Windows agents it builds.

Your browser will complain about a
self-signed web certificate — rightly;
it cannot verify a stranger's word. The
agents are stricter and smarter. Each
agent carries a **ServerID**: a
fingerprint (a SHA-384 hash) of the
agent certificate's public key. When an
agent connects, it checks the server
against that fingerprint — not against a
name a stranger could copy, but against
the key itself. The lab verified the
match by hand in transcript t08, hashing
the lab server's own certificates until
one matched the fingerprint exactly.

That is why the server's *name* still
matters, even though agents check keys:
the certificate must be *for* something —
a name or an address — before there is a
key worth fingerprinting in the right
form, and a certificate generated for
"un-configured" (the server's own word
for a server nobody named) leaves the
agent nothing it can accept. Name first.
Agents second.

## The agent

The **MeshAgent** is a small program —
the Linux x86-64 build the lab downloaded
is about 3.7 MB — that runs on each
managed machine, normally installed as a
system service, running as the machine's
most powerful user (root on Linux, SYSTEM
on Windows). That power is the point: it
can show you the screen, open terminals
and move files *because* nothing on the
machine is above it. It is also why
chapter 10 exists.

The agent is only half of an install.
Beside it sits a small text file,
**`meshagent.msh`**, the settings file:

```
MeshName=Lab Machines
MeshType=2
MeshID=0x4142E6...
ServerID=FCBDE99A...
MeshServer=wss://127.0.0.1:443/agent.ashx
```

Five lines do the work. **MeshName** and
**MeshID** say which device group this
machine belongs to. **ServerID** is the
fingerprint to check. **MeshServer** is
the address to connect to — a WebSocket
address (`wss://`), ending in
`/agent.ashx`, the server's agent door.
(The rest of the file is a long tail of
interface translations; the five lines
are the ones to read.) The generic agent
binary contains no settings at all — the
lab confirmed the download is the
server's stock agent, byte-size for
byte-size — so an agent without its
settings file is a key with no door in
mind. Your server hands out both together,
per group, from the group's page.

## The device group

A **device group** (the code calls it a
*mesh*) is the bucket machines live in:
"Lab Machines" in the lab, or in real
life perhaps "Home machines", "The
office PCs", "Mum's house". A group has
a permanent ID (the MeshID above), a
type — **agent-based** groups (type 2,
everything this guide teaches) or
Intel AMT groups — and a list of which
users hold which rights in it.

Groups are not just tidiness. They are
the border rights stop at: a user with
no rights in a group cannot see its
machines *at all* — not greyed out, not
read-only, simply absent (transcripts
t11 and t12). Design your groups the way
you would design who gets which keys,
because that is literally what they are.

## The two channels

Everything travels on two connections,
both encrypted WebSockets to the same
port:

- **`/agent.ashx`** — the agent's channel.
  The agent opens it, proves the server's
  fingerprint, and waits. Down it come
  your keystrokes, your mouse, your
  commands; back up it come the screen,
  the output, the files.
- **`/control.ashx`** — the browser's
  channel, opened by the console page
  after you sign in. Down it you send
  requests — list the machines, run this
  command — and back come the answers.

The lab never drove a graphical browser
session; it spoke both channels directly,
with curl and a small script, which is
why the transcripts can show you the
server's answers word for word. Nothing
in the chapters depends on that trick —
the web page does the same talking on
your behalf — but when chapter 8 proves
things, it proves them on these channels.

## The event log

Last part, easy to overlook: the server
**writes down what happens** — accounts
created, groups changed, machines
connecting, commands run — into its
events database. The lab saw its own
footsteps there in transcript t09. On a
real install that log is your audit
trail: if the console is a master key,
the event log is the list of when the
key turned. Chapter 10 returns to it.
