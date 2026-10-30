# Installing MeshCentral

By the end of this chapter MeshCentral is
running on your server machine, its login
page answers, and it has an administrator
account that is yours. The check is one
command whose answer you can read: a
status of 200 and the words
"MeshCentral - Login".

Everything here was done for real by this
guide's lab — MeshCentral **1.3.1**, on
Node.js v24, installed the official npm
way (transcripts t00 to t03).

## What you need first

- A machine that stays on, with
  **Node.js** installed (a current LTS
  release is fine; the lab used v24).
- A folder the server can call its own.
- Ten quiet minutes, and one decision
  made *before* the first run: **the
  server's name**.

## The decision: name the server first

A MeshCentral server has a name — the
name its certificates are made for. In
real life it is a DNS name you control,
such as `console.example.org`, pointed
at the server. In this guide's lab,
locked to loopback, it was an IP address,
`127.0.0.1`, which MeshCentral also
accepts.

Set it in `meshcentral-data/config.json`,
which the first run creates, like this:

```json
"settings": {
  "cert": "console.example.org"
}
```

Why before anything else? Because the
agents check the server's certificate
against a fingerprint (chapter 2), and a
server nobody named generates a
certificate for "un-configured" — and
its own agents then refuse to connect to
it. The lab learned this the loud way:
it skipped the name, watched its agent
fail with `Mesh Server Connection Error
[13]`, diagnosed the certificate by hand,
and fixed it by naming the server and
letting it make fresh certificates
(transcript t08). Naming the server also
moves it out of plain **LAN mode** into
**WAN** or **Hybrid** mode, which is
what puts a real address — not the word
"local" — into the settings files your
agents will download. Do it first and
the whole problem class never happens.

If you already ran the server unnamed:
stop it, move the old `*-cert-*` files in
`meshcentral-data` aside, set the name,
start it again. New certificates are
made; any agents already issued must
download fresh settings files.

## The install

```bash
mkdir meshcentral
cd meshcentral
npm install meshcentral
node ./node_modules/meshcentral
```

That is the whole of it. The first run
takes a few minutes: the server generates
its certificates, creates
`meshcentral-data`, and downloads the
stock agent files for every platform
(about 119 MB) so it can hand them out
later. Its log tells the story (t01):

```
Generating certificates, may take a few minutes...
MeshCentral v1.3.1, LAN mode.
MeshCentral HTTPS server running on port 443.
```

(With the name set, expect "WAN mode" or
"Hybrid mode" in place of LAN mode.)

Two things in a first-run log are normal
and safe to ignore in a lab: a series of
warnings about failing to *sign* Windows
agent files because a "time stamp request
timed out". Code-signing reaches out to
an internet timestamp service; without
one, the Windows agents stay unsigned.
Nothing else depends on it.

To run the server permanently — as a
system service that starts at boot — is
the normal next step on a real machine;
the exact service setup for your system
is in the project's own administrator
guide and is documented-only here. The
lab ran the server in the foreground,
which is the right way to watch a first
run in any case.

## The administrator account

A fresh server has no users, and its log
says so: "Server has no users, next new
account will be site administrator." You
have two honest routes:

- **In the browser:** open the login
  page, create the first account there.
  It becomes the site administrator
  automatically.
- **On the command line** (the route the
  lab verified, t03): *stop the server
  first* — these commands refuse to work
  while it runs, and say so — then:

```bash
node ./node_modules/meshcentral --createaccount adminname --pass <your-strong-password> --email you@example.org
node ./node_modules/meshcentral --adminaccount adminname
```

```
Done.
Done. This command will only work if MeshCentral is stopped.
```

Pick the password like it matters: this
account can do *everything*, on every
machine the console will ever manage.
Long, unique, and kept in a password
manager — chapter 10 says it again with
more company.

## The check

With the server running:

```bash
curl -sk -o page.html -w "HTTP %{http_code}\n" https://127.0.0.1/
grep -o "<title>[^<]*</title>" page.html
```

```
HTTP 200
<title>MeshCentral - Login</title>
```

The `-k` tells curl not to check the
self-signed certificate — acceptable for
this one loopback check, and the reason
it is there should stay visible: a
browser will show the same warning, for
the same reason, until the server has a
certificate from a real authority
(chapter 10). The page answering 200
with that title means the server is up
and waiting for you. Chapter 4 walks in.
