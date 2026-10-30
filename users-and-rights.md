# Users and Rights

By the end of this chapter you can hand
someone access to exactly the machines
they help with — no more — and prove the
fence holds in both directions. The
check: a second account exists that can
sign in, look around, and find *nothing*
you did not give it. This guide's lab
built that account and watched it see
nothing, then something, then nothing
again (transcripts t11 and t12).

## Two kinds of user

Every account is one of two kinds:

- A **site administrator** sees and can
  do everything: every group, every
  machine, every account, the server's
  settings. The first account is always
  one of these. Keep their number tiny —
  each one is a master key with a
  password, and chapter 10 will count
  yours.
- An **ordinary user** sees nothing by
  default. Nothing at all — no groups,
  no machines, no hint they exist.
  Everything an ordinary user can do is
  there because an administrator granted
  it, group by group. This default is
  the best sentence in this chapter:
  access is *given*, never *leftover*.

Accounts are made by an administrator,
from the console's account management
(or the `--createaccount` command from
chapter 3). Give every human their own
account. A shared login makes the event
log useless and a resignation awkward.

## Rights live on groups

A grant says: *this user*, in *this
group*, holds *these rights*. The rights
are a set of separate switches — the
server stores them as one number, a
bitmask; the lab's transcripts show the
raw values, and the ones worth knowing
by name are:

- **remote control** — use the Desktop
  and Terminal doors (the lab granted
  exactly this one: value **8**);
- **agent console** — talk to the agent
  itself;
- **server files** — the Files door;
- **manage devices** — add and remove
  machines in the group;
- **manage users** — change who holds
  rights in the group;
- **edit the group** itself;
- and the *negative* switches that take
  a door away — **no terminal**, **no
  files**, **desktop view only** — for
  grants that must be narrower than the
  defaults.

All switches on is **4294967295** — the
number the group's creator starts with,
and the number to be stingy with.

## The lab's proof, in three acts

The lab's second account, **labtech**,
was created ordinary and given nothing
(t11). Signed in successfully — the
login itself worked; the console opened
— it asked for the device list and the
server answered, in full:

```
{"action":"nodes","nodes":{}}
```

An empty world. The online machine from
chapters 6 to 8 *existed*; to labtech it
did not. Then the administrator granted
labtech **remote control only** on the
one group (t12), and the same question
returned the group with the machine
inside it. Then the grant was removed,
and the answer was `{}` again —
invisible, visible, invisible, each
change immediate.

That is the whole rights system, and it
is stronger than it looks: there is no
"can see but not touch" leak, no list of
names to covet. What you are not granted
is not hidden from you. It is *absent*.

## Admin powers to respect

Two administrator abilities deserve a
plain sentence each, because both are
master-key shaped:

- An administrator can **reset any
  user's password** (the lab did this
  too, when labtech's first password
  wasn't kept — t11). Convenient when a
  helper is locked out; sobering when
  you count who holds it.
- An administrator can **grant
  themselves anything**, including making
  new administrators. There is no higher
  court inside the tool. Choose
  administrators the way you would
  choose who holds the spare house key,
  because the analogy is exact.

## The working rules

- One account per person; never share.
- Ordinary by default; grant per group,
  per right, on purpose.
- Prefer two narrow grants to one wide
  one — the helper for your relatives'
  machines needs that group, not yours.
- When help ends, remove the grant.
  The lab's third act — invisible again
  — takes seconds, and it is the part
  everyone forgets.

Chapter 10 now steps back and protects
the whole console the way these accounts
deserve.
