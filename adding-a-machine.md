# Adding a Machine

By the end of this chapter one of your
machines has joined a group and shows
itself **online** in the console. The
check: the group's page names the
machine, with its system version, and
marks it connected. The lab did this
with a real agent, downloaded from its
own server and connected back to it —
transcripts t07 and t09.

## Ask the group for its agent

Agents are not downloaded from the
project's website. They come from **your
server, for your group** — because the
settings file that travels with them
must name your group and your server's
fingerprint. Open the group's page in
the console and choose to add a device;
the page offers the agent for each
operating system and architecture, with
its settings file beside it.

The lab fetched exactly what that page
fetches (t07):

- the **agent binary** — for Linux on
  x86-64, the server calls it agent
  **type 6**; the file is the stock
  MeshAgent, about 3.7 MB, identical to
  the server's on-disk copy;
- the **settings file**, `meshagent.msh`
  — about 36 KB, mostly translations;
  the five lines that matter are at the
  top (chapter 2).

Keep the pair together. The binary
carries no settings of its own, and the
settings file is not decoration: it is
where the agent learns where home is.

## Put the pair on the machine

On the machine being added — as its
administrator, since that is who installs
system services — the normal route is to
install the agent **as a service**, so
it starts at boot and runs whether or
not anyone is signed in. On Windows that
is an installer the server builds for
you; on Linux the agent installs itself
with its install flags. (The service
installers are documented-only in this
guide's lab, which ran the agent in the
foreground instead, the better to watch
it think.)

The lab's way, which is also the right
way to *test* any new machine before
committing to the service install:

```bash
chmod +x meshagent
./meshagent
```

## What the agent does

Watch its words; they are plain:

```
Generating Certificate...
Connecting to: wss://your-server:443/agent.ashx
Connected.
```

In order: the agent makes **itself** a
certificate (agents have identities too,
and the server records which machine
holds which). It connects *outward* to
the MeshServer address from its settings
file. It checks the server's certificate
against the ServerID fingerprint — and
only then says **Connected**, and starts
its core (you may see "Server verified
meshcore"): the part that answers for
the screen, the terminal and the files.

If instead you see `Mesh Server
Connection Error` and a number, the
agent is refusing or failing, and it is
worth your full attention — chapter 14
walks the cases, including the lab's own
certificate refusal (t08), error numbers
and all. Do not wave an agent past a
certificate it rejects: that check is
the lock on the whole house.

## The machine appears

Back in the console, the group now lists
the machine — by its own hostname, with
the facts the agent reported: its system
("Ubuntu 24.04.5 LTS" in the lab), the
address it connected from, when it first
connected. The lab read the same record
off the control channel (t09); the lines
that pronounce it alive are:

```
"conn": 1,   (connected now)
"pwr": 1     (powered on)
```

Give the machine a friendlier name in
the console if its hostname is cryptic —
the console's name is yours; the agent
will keep reporting its own as well.

That is a machine added: pair downloaded
from your own server, agent running on
the machine, connection held open,
record visible. Chapter 7 opens the
three doors the connection now offers —
and chapter 8 proves the whole chain
again, slowly, the way you would check
it on a machine you actually depend on.
