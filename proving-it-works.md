# Proving It Works

By the end of this chapter you have four
checks that together prove the whole
chain — server, login, agent, control —
and each check is one you can run
yourself, in order, the first time a
machine matters. Every check here is one
this guide's lab actually ran; the
transcript numbers are beside them, so
you can compare your answers with real
ones.

Do these on a machine you can walk over
to and reboot by hand. Proving is for
before it matters.

## Check 1: the page answers

```bash
curl -sk -o page.html -w "HTTP %{http_code}\n" https://your-server/
grep -o "<title>[^<]*</title>" page.html
```

**Pass:** `HTTP 200` and
`<title>MeshCentral - Login</title>`
(the lab's page: 200, 75,730 bytes, t02).
**Fail means:** the server is not
running, or not reachable — nothing
later can work, so nothing later is
worth trying yet.

## Check 2: the login is real

Sign in, and judge by the landing page
(chapter 4's trap): **your account name
and a logout link** mean you are in; a
fresh password box — with the word
**Invalid** on it, under the same calm
200 — means you are not.

**Pass:** the console, with your name on
it (t05). **Fail means:** wrong
password, or the account does not exist.
Note the shape of the failure for later:
MeshCentral fails politely and plainly,
on the page, never in the status code.

## Check 3: the device is online

In the console, open the group and look
at the machine: it should show as
connected, with the system and address
the agent reported. Under the page, the
record the lab read said it in two
fields (t09):

```
"conn": 1   (connected now)
"pwr": 1    (powered on)
```

**Pass:** the machine listed, marked
connected, details fresh.
**Fail means:** the agent is not
connected — and now the agent's own
words are the evidence. Run it in the
foreground on the machine and read:
`Connected.` passes; `Mesh Server
Connection Error` sends you to
chapter 14 with the error number in
hand. Never skip to reinstalling: the
agent almost always says what is wrong,
in the one line everyone scrolls past.

## Check 4: a marker command comes home

The decisive one. From the console's
Terminal on the machine, run:

```bash
echo MC-REMOTE-OK && hostname && whoami
```

**Pass:** your exact marker line comes
back, followed by the *machine's* name
and the account the command ran as
(t10: "root" on the lab machine, because
its agent ran as root). **Fail means:**
the machine is listed but not truly
under control — a stale record, a
half-connected agent — and the honest
state is "not proven", however green
the page looked.

Why a marker: outputs like a hostname
can be guessed or cached; a string you
invented on the spot cannot come back
unless the command ran there and the
answer travelled home. Insist on it.

## What "proven" covers — and what it doesn't

Four passes prove: the server serves,
your login is real, one agent is
connected and checked the server's
fingerprint, and control flows in both
directions. They do **not** prove the
Desktop picture is smooth, that files
transfer at a useful speed, or that any
of it survives the server's reboot —
test those separately, on purpose, the
same way: one claim, one check, one
answer you can read (chapter 13 lists
the edges to test against). And they
prove nothing about *who else* can do
what you just did — that is a different
chain, and the next chapter holds it up
to the light.
