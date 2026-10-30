# MeshCentral for Mere Mortals

Every computer you own already knows how to
be reached one at a time: a remote desktop
here, an SSH login there, a different tool
for every machine. **MeshCentral** replaces
that pile with one web page. You run one
small **server**, you install a small
**agent** on each machine you own, and the
agents connect to your server and wait.
Open the server's page in any browser and
every machine is simply *there* — its
screen, its terminal, its files — behind
one login, on hardware you control. No
account with anyone, no subscription, and
no company's cloud in the middle: your
machines answer to your server, and to
nobody else.

Say the quiet part first, because this
guide will keep saying it: **a console
that can control every machine you own
is a master key.** Whoever signs in to
it can read files, run commands and watch
screens across your whole fleet. That is
exactly why it is useful — and exactly
why this guide names the server properly,
gives helpers narrow rights instead of
the keys to everything, and spends a
whole chapter (chapter 10) on protecting
the console *before* it teaches you to
share it. Treat the console like a
password vault, because that is what it
is.

The lab behind this guide ran the real
thing: **MeshCentral 1.3.1**, installed
the official way with npm, on a small
Linux machine, talking to itself over the
loopback address with its own self-signed
certificates. Against it the lab created
an administrator and a deliberately
powerless second user, built a device
group, downloaded a genuine agent from
the server, and got that agent to connect
and appear online in the group — then
drove the machine through the console,
running a command whose output travelled
back through the server. It also broke
things on purpose: the agent at first
*refused* to connect, because a server
with no name has a certificate no agent
can check, and chapter 14 tells that
story with the error messages quoted.

What the lab could not do, it did not
fake. Its machine had no screen of its
own, so the remote *desktop* — seeing
and driving another machine's display —
is taught from the documentation and
labelled as such wherever it appears;
the terminal path underneath it is the
one the lab proved end to end. Agents
for other operating systems, internet
exposure, real certificates and
two-factor sign-in are likewise labelled.
`criteria.md` keeps the full ledger of
what was run and what was only read.

## What this guide covers

- [**What MeshCentral is**](what-meshcentral-is.md) —
  the mental model: one server, one agent
  per machine, one web page — and why the
  console is a master key
- [**The moving parts**](the-moving-parts.md) —
  the server and its data folder, the
  certificates, the agent and its settings
  file, the device group, and the two
  channels everything travels on
- [**Installing MeshCentral**](installing-meshcentral.md) —
  the npm install, the first run, naming
  the server before anything trusts it,
  and the administrator account
- [**Your first login**](your-first-login.md) —
  the login page, what a successful login
  really looks like, and the two cookies
  that carry your session
- [**Device groups**](device-groups.md) —
  the buckets machines live in, and why a
  group is also the border that rights
  stop at
- [**Adding a machine**](adding-a-machine.md) —
  downloading the agent and its settings
  file from your own server, and what the
  agent does when it first runs
- [**The remote desktop**](the-remote-desktop.md) —
  the Desktop, Terminal and Files tabs:
  what each one hands you, and which of
  them this guide's lab proved
- [**Proving it works**](proving-it-works.md) —
  the checks, in order: the page answers,
  the login is real, the device is online,
  and a marker command comes home
- [**Users and rights**](users-and-rights.md) —
  accounts, site administrators, and the
  per-group rights that decide who can
  even *see* a machine
- [**Protecting the console**](protecting-the-console.md) —
  names and certificates, strong
  passwords, few administrators, narrow
  grants, and thinking before the
  internet can see your login page
- [**Recipes**](recipes.md) — one group
  per household for helping family, a
  headless box driven by terminal alone,
  reaching home from the road, and one
  command sent to many machines
- [**The neighbours**](the-neighbours.md) —
  RustDesk, SSH, VNC, the cloud remote
  tools and Cockpit: what each does that
  MeshCentral doesn't, and vice versa
- [**Limits**](limits.md) — no agent, no
  control; no screen, no desktop; one
  server as a single point of failure and
  of compromise; and the lab's own edges
- [**Troubleshooting**](troubleshooting.md) —
  the agent that refuses your
  certificate, the settings file that
  points at "local", the login that says
  Invalid, and the empty group that is
  rights, not a bug
- [**Glossary**](glossary.md) — the
  terms, collected in one place

## What it doesn't cover

Intel AMT — the management engine built
into some business PCs, which MeshCentral
can also drive, even with the machine
switched off. It is real, it is powerful,
and it needs the right hardware and its
own careful setup; this guide points at
it and teaches the agent-based path
instead. Public exposure done properly —
a real domain name, a Let's Encrypt
certificate, a reverse proxy — is
described far enough to plan it, not
clicked through. Supporting other
people's machines for a living, with
ticketing and billing, is a business this
guide does not start.

## How to use this guide

Read chapter 1 for the model and
chapter 2 before installing anything —
knowing which part holds what turns
later confusion into a named problem,
and chapter 2 contains the one decision
(the server's name) that is painful to
change later. Chapters 3 to 6 get you a
server, a login, a group and your first
machine; chapter 8 is the one to read
slowly, because its checks catch the
silent failures — an agent that never
connects, a login that looks fine and
isn't — before anything depends on them.
The lab's transcripts live in
`meshcentral-lab/transcripts/`, numbered
in the order the work happened.

---

## Part of the series

This guide is one of the [For Mere Mortals](https://paulsullivan33-dev.github.io/mere-mortals/) guides: plain-language guides to the tools programmers and makers use.

Related guides:

- [RustDesk for Mere Mortals](https://paulsullivan33-dev.github.io/rustdesk-for-mere-mortals/)
- [SSH for Mere Mortals](https://paulsullivan33-dev.github.io/ssh-for-mere-mortals/)
- [Tailscale for Mere Mortals](https://paulsullivan33-dev.github.io/tailscale-for-mere-mortals/)

## License

The writing in this guide is licensed under [CC BY 4.0](https://github.com/paulsullivan33-dev/meshcentral-for-mere-mortals/blob/main/LICENSE). Code examples and lab scripts are licensed under the [MIT License](https://github.com/paulsullivan33-dev/meshcentral-for-mere-mortals/blob/main/LICENSE-CODE).
