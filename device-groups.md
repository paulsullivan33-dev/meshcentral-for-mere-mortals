# Device Groups

By the end of this chapter you have your
first device group, and you understand
the two jobs groups do: they collect
machines, and they fence rights. The
check: the group appears in **My
Devices**, and you can point at its
permanent ID. The lab's group, "Lab
Machines", was created and read back in
transcript t06.

## What a group is

A device group is a named bucket. A
machine belongs to exactly one group —
the group named in its settings file
(chapter 2) — and the group is where
everything about it is decided: who can
see it, who can drive it, what the agent
may do without asking the person at the
keyboard.

Make groups the way you would cut keys.
One group per *circle of trust*, not per
machine type:

- **Home machines** — yours, full stop.
- **The office PCs** — the ones a
  colleague may also need to reach.
- **Family** — machines you look after
  for relatives, which a helper may
  share but your office colleague should
  never even see.

Three small groups beat one big one,
because rights are granted per group
(chapter 9). A group costs nothing;
make them freely.

## Creating one

Signed in as administrator, open **My
Devices** and add a device group. You
will be asked for:

- a **name** — the human label, changeable
  later;
- a **type** — choose the **agent** type
  (the code's type 2). The other family,
  Intel AMT groups, manages machines
  through their built-in management
  hardware instead of an installed agent;
  it is outside this guide's teaching,
  as chapter 1 said.

Under the page, the server does what the
lab did through the control channel
(t06): it creates the group and answers
with its permanent identity:

```
{"action":"createmesh","result":"ok",
 "meshid":"mesh//QULmJBUNl186SgWQq7FCsFE5ckL9brONEtJqvKQygGz...",
 "links":{"user//labadmin":{"name":"labadmin","rights":4294967295}}}
```

Two things to read in that reply, because
you will meet both again:

- The **MeshID** — `mesh//` followed by
  a long base64 string — is the group's
  true name. Rename the group all you
  like; the ID never changes, and it is
  the ID that settings files carry.
- The **links** — the list of who holds
  what in this group. The creator starts
  with rights **4294967295**, every right
  there is (the number is a bitmask with
  all its bits on; chapter 9 takes it
  apart). Anyone not in the links holds
  *nothing* here. Not read-only. Nothing.

## An empty group is a working group

A new group sits empty, and that is a
complete, correct state — the server is
ready to hand out agents *for this
group* and to accept their connections.
Nothing is broken because no machines
have arrived. Chapter 6 does the
arriving: you will open this group's
page, ask it for an agent, and watch a
machine join. The group's side of that
bargain — its ID in the settings file,
its door open on the server — is
already done, and it was done the moment
you created it.
