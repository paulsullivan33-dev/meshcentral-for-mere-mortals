# Glossary

**Agent (MeshAgent)** — the small program
installed on each managed machine. It
connects outward to the server, proves
the server's fingerprint, and answers
for the machine's screen, terminal and
files. It runs as the machine's most
powerful user.

**Agent certificate** — the server
certificate whose public key the agents
check. Its fingerprint is the ServerID.

**AMT (Intel Active Management
Technology)** — management hardware built
into some business PCs, which
MeshCentral can also drive, even with
the machine off. Pointed at in this
guide; not taught.

**Consent** — a group setting that makes
the server notify the person at a
machine, or ask their permission, before
a remote session begins.

**Control channel** — the browser's
encrypted WebSocket connection to the
server (`/control.ashx`), opened after
sign-in, over which console requests and
answers travel.

**Device group (mesh)** — the bucket a
machine belongs to, and the border at
which rights stop. Has a permanent
MeshID, a type, and a list of who holds
which rights in it.

**Event log** — the server's diary:
accounts, grants, connections, commands,
kept in its events database. Your audit
trail.

**Files tab** — the console door that
browses a machine's file system and
moves files to and from it.

**Fingerprint** — a short hash standing
for a long key, safe to compare at a
glance. The ServerID is a SHA-384
fingerprint of the agent certificate's
public key.

**Hybrid mode** — the server mode (name
set to an IP address, in the lab's case)
in which LAN and WAN behaviour combine
and settings files carry real addresses.

**LAN mode** — the unnamed server's
default mode; settings files carry the
word "local" instead of an address.
Fine for a first look in a browser; not
a state to issue agents from.

**MeshID** — a group's permanent identity
(`mesh//…`), carried in every settings
file for that group. Names can change;
the ID cannot.

**meshcentral-data** — the folder beside
the server holding its config, databases
and certificates. Back it up and guard
it like the vault it is.

**MPS** — the server component (port
4433) that Intel AMT machines connect
to. Present in the logs; exercised
nowhere in this guide.

**Node** — the server's word for one
machine's record: its name, system,
connection state (`conn`), power state
(`pwr`) and agent details.

**Rights** — the per-group, per-user set
of switches deciding what an account may
do: remote control, files, managing
devices, and their negative twins (no
terminal, no files, view only). Stored
as a bitmask; all switches on is
4294967295.

**ServerID** — the fingerprint an agent
pins: SHA-384 of the agent certificate's
RSA public key. If the server cannot
match it, the agent refuses to connect —
by design.

**Settings file (`meshagent.msh`)** — the
small text file that travels with the
agent and tells it its group (MeshID),
its server (MeshServer) and its server's
fingerprint (ServerID). Half the install;
useless alone, essential together.

**Site administrator** — an account that
can do everything on the server,
including resetting passwords and making
more administrators. Keep their number
tiny.

**Terminal tab** — the console door that
opens a command line on a machine, with
the agent's authority.

**WAN mode** — the mode of a server with
a proper DNS name: the mode real
installs should run in.

**xid / xid.sig** — the two session
cookies set at login: the token, and its
signature. Together they are the
browser's proof it signed in.
