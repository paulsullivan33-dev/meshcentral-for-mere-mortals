# Recipes

Short, complete jobs built from the
parts the earlier chapters proved. Each
recipe names what it assumes and what it
leaves in your hands. The machines and
people are invented examples — a group
called *Family*, a helper called Sam —
arrange your own to taste.

## Help a relative, without handing over your house

*Assumes: chapters 5, 6 and 9 done once.*

1. Make a group for their machines —
   **Family Laptops**, say — separate
   from your own group.
2. Add their machines to it (chapter 6).
   On their group, set the **consent**
   options so a session announces itself
   on their screen.
3. Your own account needs no change: you
   created the group, so you hold all
   rights in it.
4. If Sam also helps them, Sam gets an
   account with **remote control** on
   *Family Laptops* only — not on your
   group, not as administrator.

*Result:* from one login you reach the
relatives' machines; Sam can help and
can see nothing of yours; the relatives
see sessions arrive. When Sam's help
ends, one grant removed (chapter 9).

## Look after a headless box

*Assumes: one screen-less home server —
a file box, a media server, a little
always-on machine.*

1. Install the agent as a service; skip
   every thought of the Desktop tab —
   there is no desktop.
2. Live in the **Terminal** tab for
   fixes and the **Files** tab for logs
   and configs. That pair covers nearly
   every job a headless box ever asks
   for.
3. Prove it with chapter 8's marker
   command *before* you rely on it from
   elsewhere — a headless box you cannot
   reach is just a box.

*Result:* the cupboard server is as
reachable as the machine on your desk,
and you never plug a monitor into it
again.

## Reach home from the road

*Assumes: chapter 10 read, not skimmed.*

1. Do **not** port-forward the console.
2. Put the server on a private network
   you can join from your laptop — a VPN
   into home, or a mesh tool such as
   Tailscale — and connect through that.
3. From the coffee shop, the console is
   exactly as it is from your desk —
   because to the network, you *are*
   home.

*Result:* the login page never faces the
open internet, and "remote access" stops
being a security decision you remake
every trip.

## One command, many machines

*Assumes: a group of machines that are
genuinely alike — three identical office
PCs, a shelf of the same little servers.*

1. Select the machines in the group and
   use the console's option to run a
   command on all of them — the same
   path chapter 7 proved on one machine,
   fanned out.
2. Choose commands that *report* before
   you choose commands that *change*:
   versions, free space, uptime.
   Read every answer; the fan-out sends
   faithfully to the machine that is
   different, too.
3. Keep the command in your notes with
   its date and answers.

*Result:* fleet chores become one
honest minute — and the lab's word for
the risk stands: a command run as the
agent's account, on every machine at
once, deserves a read-before-you-send
habit.

## A new machine joins the family

*Assumes: a new or rebuilt computer in
the house.*

1. Decide its group first — whose circle
   of trust is it in?
2. Download the agent *from that group*
   on your server (chapter 6), install
   as a service, watch for `Connected.`
3. Rename it in the console to the name
   humans use ("kitchen-pc"), and run
   chapter 8's four checks once.

*Result:* five minutes from box to
managed machine — and the group
decision, made first, is the security
decision, made once.
