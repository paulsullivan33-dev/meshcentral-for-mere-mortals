# Troubleshooting

The failures this guide's lab actually
met come first — each with the words the
software used, because matching the
words is how you know you have the same
problem. The rest are the standard traps
the earlier chapters planted flags
beside.

## The agent says "Connection Error [13]", then "[12]"

**Seen in transcript t08.** The agent
connects — the TCP connection opens —
and then refuses the server during setup.
The server was running with a
certificate made for **"un-configured"**:
nobody had given the server a name, so
there was nothing in the certificate an
agent could accept.

Check what your server presents:

```bash
echo | openssl s_client -connect your-server:443 2>/dev/null | grep subject=
```

Fix: set the server's name
(`settings.cert` in
`meshcentral-data/config.json`) to its
DNS name or IP address, move the old
`*-cert-*` files aside, restart, and
download **fresh** agent settings files
— the ServerID fingerprint changes with
the new certificates. The deeper lesson
is chapter 3's: name the server first.

## The settings file says "MeshServer=local"

An unnamed server in LAN mode writes the
word `local` into its settings files,
and a hand-run agent cannot use it.
This is the same root cause as the entry
above, seen from the other side. Name
the server; the next settings file will
carry a real address ending in
`/agent.ashx`, like the lab's fixed one
(t09):

```
MeshServer=wss://127.0.0.1:443/agent.ashx
```

Hand-editing the address into a file
whose ServerID still points at a
nameless certificate fixes the smaller
half of the problem and meets error 13
coming the other way — the lab tried
exactly that, so you don't have to.

## The agent connects once, then never again after I changed settings

The agent keeps state in **`meshagent.db`**
beside itself, including what it last
believed about the server. If you changed
the server's name or certificates, delete
`meshagent.db` while the agent is stopped
and let it generate a fresh identity
(it will say `Generating Certificate...`
on the next run). The lab did this
between its failed and successful runs.

## Login "fails" but the status said 200

It probably really failed. MeshCentral
answers a wrong password with **200 and
the login page again**, with **Invalid**
on it (chapter 4, transcript t11). Judge
by the page you land on — your name and
a logout link, or a password box — never
by the status code. Then check the
username, then the password, then
whether the account exists at all.

## "This command will only work if MeshCentral is stopped"

The account commands (`--createaccount`,
`--adminaccount`) talk to the database
directly and refuse to share it with a
running server (t03). Stop the server,
run the command, start the server. The
message is not an error in your command;
it is the tool keeping its own books
straight.

## A user signs in and sees no machines

Not a bug — rights (chapter 9,
transcripts t11–t12). The user holds no
grant on any group containing machines,
so the console shows them an empty
world. Grant the group, with the
narrowest rights that fit, and the
machines appear immediately. If *you*
see nothing as administrator, check
instead whether the agents are connected
at all (chapter 8, check 3).

## The machine is listed but nothing works

Run chapter 8's check 4 — the marker
command. If the marker does not come
home, the listing is a memory, not a
connection: the agent has stopped, the
machine slept, or the network moved.
Read the agent's own output in the
foreground on that machine before
touching the server; it announces
`Connected.` or the exact error,
every time.

## Warnings about signing Windows agents at first run

"Failed to sign … Time stamp request
timed out" means the server could not
reach an internet timestamp service
while signing its Windows agent files
(t01). Cosmetic in a lab: the agents are
still built, just unsigned. On a real
server with internet access they sign
quietly; where they cannot, expect
Windows to be extra suspicious of the
installer, and plan accordingly.

## The browser warns about the certificate

That is the self-signed certificate from
chapter 3, doing its honest job of being
unverifiable. On your own network, for
your own server, you may proceed past it
knowingly. The cure — not the habit —
is chapter 10's: a real DNS name and a
real certificate. If the warning appears
for a server that *had* a real
certificate yesterday, stop: that change
is exactly what warnings are for.
