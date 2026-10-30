# Protecting the Console

By the end of this chapter your console
is defended the way its power deserves —
and you can recite the defence as a
checklist, because that is what it is.
The check: point at each item below and
say, out loud, "done" or "deliberately
not, because…". Anything you cannot say
either about is a hole with a name.

The framing, one last time, without
softening: **this console can control
every machine you own, as their most
powerful user, from one login.** An
attacker who owns it does not need to
attack your machines at all. So the
console gets the care you would give a
password vault — because to anyone
attacking you, it is better than one.

## 1. Name the server, and mean it

Chapter 3's lesson is a security control,
not a cosmetic one. A named server has
certificates an agent can check — and
the agents *do* check (t08), refusing a
server that cannot prove itself. That
refusal is what stands between your
machines and a fake server harvesting
them. Never teach an agent, or yourself,
to skip it.

For a server other people will use,
replace the self-signed certificate with
one from a real authority (Let's Encrypt
is the usual route), under the DNS name
they will actually visit. Browsers then
stop warning — which matters, because a
warning everyone is trained to click
past is a door left open. The lab ran
self-signed on loopback only; real
certificates are documented-only in this
guide, and they are not optional in
real life.

## 2. Passwords worthy of the door

- Every account: long, unique, never
  used anywhere else, kept in a password
  manager.
- Administrator accounts: longer. These
  are the passwords your whole fleet
  hangs from.
- **Turn on two-factor sign-in**,
  especially for administrators —
  MeshCentral supports authenticator-app
  codes and security keys. The lab did
  not enable it in its sandbox;
  it is documented here, plainly, as the
  single highest-value switch it left
  unflipped. Do not leave it unflipped
  on a real server.

## 3. Count your administrators

List them. For each one, say why. Site
administrators can reset passwords,
grant anything, and make more
administrators (chapter 9); the honest
number for most homes is one or two.
Everyone else is an ordinary user with
grants. If a name surprises you on the
list, that surprise is the audit working.

## 4. Grant narrow, review sometimes

Chapter 9's rules, from the defence
side: per-group grants, the fewest
rights that let the helper help —
remote control without files, view-only
where watching is enough — and a
recurring moment (put it on a calendar)
where you walk the grants and remove
the stale ones. Access that outlives
the favour is the commonest real-world
hole in systems exactly like this.

## 5. Think before the internet can see it

On your home network, the console's
login page is reachable by your network.
On the open internet, it is reachable by
*everyone's* scripts, all day, forever.
If you need access from the road, prefer
in this order:

1. **Reach the server through a private
   network you control** — a VPN, or a
   mesh network such as Tailscale (there
   is a guide in this series) — and leave
   port 443 closed to the world.
2. If it must be public: real name, real
   certificate, two-factor on, strong
   passwords, and the server kept
   updated. Understand that your login
   page is now a public door, and treat
   the event log (next item) as required
   reading.

What not to do: port-forward 443 to a
self-signed, single-password console
because it was convenient on a Tuesday.
That is the configuration this chapter
exists to prevent.

## 6. Read the event log

The server writes down accounts, grants,
connections and commands (chapter 2).
Skim it the way you would skim a bank
statement: rarely exciting, and that is
the point. A login at an hour you were
asleep, a grant you did not make — the
log is where a bad week announces itself
early. The lab saw its own comings and
goings recorded there (t09); yours will
record everyone's.

## 7. Keep it updated, and back up the folder

MeshCentral is updated through npm like
it was installed; apply updates the way
you apply system updates — promptly,
after a backup. The backup is one
folder: **`meshcentral-data`** holds the
accounts, the groups, the machine
records and the very keys the agents
trust. Back it up like a vault, store
the copies like one too — a backup of
the master key is a master key.

Do these seven and the console's power
works for you alone. Skip them, and you
have built — carefully, with good
software — the single best target in
your house.
