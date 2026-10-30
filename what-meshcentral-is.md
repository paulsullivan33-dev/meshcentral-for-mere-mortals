# What MeshCentral Is

By the end of this chapter you can say,
in one breath, what runs where: one
server you run yourself, one small agent
on each machine you own, and one web page
that ties them together. No commands yet
— the check at the end is that the
picture in your head has three parts and
no cloud in it.

## The problem it solves

Reaching your own machines, one at a
time, works until it doesn't. The desktop
PC is reached with one tool, the little
server in the cupboard with another, the
laptop in another house with a third —
and every one of them has its own
password, its own quirks, and its own
idea of how you prove you are you. What
you actually want is boring: open one
page, see every machine, click the one
you need.

MeshCentral is that page, with the
machinery behind it yours. It is free,
open-source software. You install the
server on a machine that stays on — an
old desktop, a small home server, a cheap
rented box. You install its agent on each
machine you want to reach. From then on,
the relationship is simple and it points
the way that makes everything else easy:

**The agents call the server. The server
never calls them.**

Each agent opens a connection *outward*
to your server and holds it open, the
way your browser holds a connection to a
chat service. That one decision is why
MeshCentral works across home routers
and office firewalls without opening any
ports on the machines being managed: an
outward connection is the kind every
network already allows. Your browser
also talks only to the server. When you
click "terminal" on a machine, the
server passes your keystrokes down the
agent's waiting connection, and the
answers travel back the same way.

## What you get when it works

From the one console page, for each
machine, you can:

- **See and drive its screen** — the
  Desktop tab, a live remote desktop in
  the browser.
- **Open a terminal on it** — a real
  shell or command prompt, as if you
  were sitting at it.
- **Browse its files** — list, download,
  upload, delete, through the Files tab.
- **Ask what it is** — hardware, system
  version, when it last booted, whether
  it is on mains or battery.
- **Run a command across many machines**
  at once, and read what came back.

And you decide who else may do any of
that, machine group by machine group,
right by right — chapter 9 is devoted to
it, because it matters.

## The part to hold onto

A tool that can do all of that, on every
machine you own, from one login, is not
a convenience item. It is a **master
key**. If someone guesses or steals the
password of an administrator account on
your console, they do not get one
machine — they get all of them, with the
agents running as the most powerful user
each machine has. MeshCentral's design
knows this: its agents refuse to talk to
a server whose certificate they cannot
verify (this guide's lab watched an
agent do exactly that refusing, in
transcript t08), and its rights system
can hide whole groups of machines from a
user completely (transcript t11).

So the rule of this guide, stated here
where it belongs: **protect the console
like a password vault.** A proper name
and certificate for the server. A strong,
unique password for every account, and
two-factor sign-in for the
administrators. The fewest administrators
you can manage with. Helpers get their
own accounts with rights only where they
help. Chapter 10 goes through it in
order; everything before it keeps the
rule in view.

## What it is not

MeshCentral is not a cloud service —
there is no MeshCentral company holding
your machines for you; the server is
yours, on your hardware, and if you
switch it off, remote control stops
(chapter 13 is honest about that single
point of failure). It is not a way to
reach machines you have no right to
manage: the agent is installed software,
put there by someone with access to the
machine, and it says so on the machine.
And it is not the only way to reach a
machine — chapter 12 sets it beside
RustDesk, SSH, VNC and the commercial
cloud tools, plainly, so you can pick
with your eyes open.
