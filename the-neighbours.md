# The Neighbours

MeshCentral is one answer to "reach my
machines". These are the others you will
meet, characterised plainly — what each
does that MeshCentral doesn't, and what
MeshCentral does that it doesn't. All of
this chapter is characterisation, not
benchmarking; none of the neighbours
were run in this guide's lab.

## RustDesk

The closest neighbour. RustDesk gives
you remote *desktop* — one machine's
screen on yours — with its own apps, and
you can self-host its relay if you like.
It is superb at the single act: sit down
anywhere, drive one machine. What it
does not give you is the console: no
single page where every machine waits,
no groups with per-user rights, no
terminal-and-files doors beside the
screen, no event log of the fleet. If
your life is "drive the home PC from the
road", RustDesk may be all you need; if
it is "look after a shelf of machines
and let Sam help with two of them",
that is MeshCentral's shape. (This
series has a RustDesk guide; the two
sit comfortably side by side.)

## SSH

The oldest neighbour, and still the
best terminal ever made. SSH reaches one
machine's command line, securely,
quickly, from anywhere — for a Linux
server it may be all you ever want. It
has no screen for a desktop machine, no
fleet view, no help for the relative
whose problem is a dialog box, and every
machine is its own arrangement of keys,
ports and exceptions through NAT.
MeshCentral's Terminal door is, in
spirit, "SSH without the arrangement" —
and many people keep real SSH as well
for the machines that suit it. (There is
an SSH guide in this series.)

## VNC and RDP

The screen protocols underneath
everything: VNC (and Microsoft's RDP for
Windows) show you a machine's desktop,
full stop. Solid, venerable — and only
that. No agents phoning home, so *you*
arrange how the connection reaches the
machine; no accounts or rights beyond
the machine's own; no terminal, no files,
no fleet. MeshCentral's Desktop door is
their equal in purpose and considerably
less plumbing in practice.

## TeamViewer, AnyDesk and the cloud tools

The commercial neighbours: polished apps,
someone else's servers, accounts with a
company, free tiers with limits and
prompts. They are genuinely easy, and
for helping a stranger's machine once,
that ease wins. The trade is the one
chapter 1 named: your machines answer to
*their* cloud, under *their* account
rules, at *their* prices, forever.
MeshCentral exists for people who would
rather run that cloud themselves — and
accept the upkeep (chapter 10) as the
price of the keys staying home.

## Cockpit

A web console for *one* Linux server:
its services, logs, storage, updates,
beautifully presented. Not a rival —
Cockpit looks after the machine it lives
on; MeshCentral looks after the fleet
from one chair. They pair well: the
console to reach the box, Cockpit for
the box's own housekeeping. (This series
has a Cockpit guide.)

## Tailscale and VPNs

Not remote control at all — remote
*reachability*. A mesh VPN makes your
machines one private network wherever
they are; what you then run over it —
SSH, RustDesk, this console — is up to
you. Chapter 10's road recipe uses
exactly this pairing: the VPN provides
the road, MeshCentral provides the
driving. (There is a Tailscale guide in
this series.) If a tool on this page
ever claims the network alone is remote
management, it is selling you the road
as the car.
