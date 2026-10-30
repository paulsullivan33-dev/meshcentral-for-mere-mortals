# Limits

What MeshCentral cannot do, stated the
way chapter 8 would want: plainly,
before you depend on it. Some of these
are the tool's edges; the last section
is this guide's own, kept separate so
the two never blur.

## No agent, no control

The agent is installed software. A
machine without it — a fresh computer,
a locked-down work laptop you may not
install on, most phones and tablets,
anything whose owner says no — is a
machine MeshCentral cannot reach, full
stop. The one exception is Intel AMT
hardware management, which this guide
points at and does not teach. "I can see
every machine I own" is only ever true
of the machines you were able to put
the agent on.

## No screen, no desktop

The Desktop door shows a graphical
session. Headless machines offer
Terminal and Files only — which, as
chapter 11 argues, is usually enough.
But if your plan for a box *is* its
screen, and the box's screen is off,
asleep in a way the agent cannot wake,
or stuck at a login the agent cannot
see past, the console will not save
you. Test the ugly cases while you can
still walk to the machine.

## One server, twice a single point

The server is a **single point of
failure**: it stops, remote control
stops — the agents wait politely for
its return, but nothing passes. And it
is a **single point of compromise**:
chapter 10's master key, which is why
that chapter is the longest shadow in
this guide. MeshCentral can be set up
with redundant servers and shared
databases; that is enterprise plumbing
this guide deliberately does not teach,
and for a home fleet the honest answer
is a good backup of `meshcentral-data`
and a server machine you trust to stay
on.

## Certificates tell the truth slowly

With self-signed certificates, browsers
warn — correctly — every time, and
agents (rightly) refuse servers that
cannot prove themselves. All of that is
the system working. The limit is human:
a household trained to click past
warnings has un-trained its own alarm.
The real fix is a real name and a real
certificate; until then, expect the
friction and do not pave over it.

## Built for administering, not for playing

The Desktop door is for fixing and
helping: office work, dialogs, settings.
It is not a gaming or video stream —
latency and frame rates are an admin's,
not a player's. Judge it by "could I
install this update from a train", not
by "could I watch a film through it".

## Agents run with the keys to each machine

By design the agent runs as each
machine's most powerful user. There is
no low-power mode, no agent that can
only look. Your defence is not a weaker
agent but a protected console and narrow
rights (chapters 9 and 10). Anyone for
whom that design is unacceptable should
not install the tool — and deserves to
have read it here, not discovered it
later.

## This guide's own limits

The lab that wrote this guide ran one
server and one agent, **on the same
sandbox machine**, over loopback. So
these are described, not proven, in
these pages: the graphical **Desktop**
session and the **Files** tab in a real
browser; installing agents as system
services; agents for Windows and macOS;
reaching the server across a real
network or the internet; real
certificates and two-factor sign-in,
both prescribed in chapter 10 and
neither clicked through in the lab.
`criteria.md` keeps the full ledger.
Everything the lab *did* run — install,
accounts, login, group, agent,
connection, remote command, rights in
both directions — is in the transcripts,
and the chapters say "the lab" only
about those.
