# The Remote Desktop — Desktop, Terminal and Files

By the end of this chapter you know what
each of a connected machine's three tabs
hands you, and which of them this guide
proves rather than describes. The check
needs no equipment: you can say, for
each tab, *what the person at the
machine sees* while you use it. That
question — what it looks like from the
other chair — is the one that decides
whether a tool like this is used with
people or merely on machines.

Open any online machine in the console
and three doors stand in a row.

## Desktop: the screen itself

The **Desktop** tab shows the machine's
screen, live, in your browser — and your
mouse and keyboard drive it. It is the
full remote desktop: open programs, read
dialogs, click the button the person at
the machine cannot find. The server
passes the picture down the agent's
connection and your input back up it;
you can adjust quality against bandwidth,
and view without controlling when
watching is enough.

Two honest labels belong on this door.
First, it needs a screen to show: the
machine must be running a graphical
session. A headless server has no
desktop to send you, and offers the
other two doors instead. Second, this
guide's lab machine had no graphical
session of its own, so the lab never
drove a Desktop session — **this door is
taught from the project's documentation,
not from a transcript**, and
`criteria.md` says so in the ledger.

What the person at the machine sees:
you, working. Their screen moves, their
pointer moves. Groups can be set to
**notify** the user, or to **ask
consent**, before a desktop session
begins — set that deliberately, per
group, in line with whose machine it
is (chapter 10). Remote help given
openly is a favour; the same session
unannounced is a surveillance tool, and
the difference is a setting you chose.

## Terminal: a shell, as if you were there

The **Terminal** tab opens a command
line on the machine — a shell on Linux,
a command prompt or PowerShell on
Windows — running with the agent's own
authority, which is to say the machine's
highest. Type, read, fix, leave. For
servers and for quick surgery it is the
door you will use most, and it asks
nothing of the machine's screen at all.

This door the lab **did** prove, end to
end (transcript t10). Through the same
control machinery the tab uses, the lab
sent one machine a single line —

```
echo MC-LAB-REMOTE-OK && hostname && whoami && uptime
```

— and the machine's own answer came back
through the server: the marker line, its
name, the account the command ran as,
its uptime. A marker like that is the
honest test of any remote tool: it
cannot come home unless the command
truly ran *there* and the truth travelled
back. Chapter 8 builds the full set of
such checks. (The interactive tab itself
— typing live into a browser window —
was not driven in the sandbox; the
command path beneath it was, and is the
part that can fail silently.)

What the person at the machine sees:
nothing on screen, by default. All the
more reason the event log (chapter 2)
matters: the server writes sessions
down, and a machine's owner can be
shown that record.

## Files: the machine's folders, in the browser

The **Files** tab shows the machine's
file system as a list you can walk:
download a log, upload a fixed config,
rename, delete. It is the slowest of the
three doors to admire and the one that
saves the most afternoons — fetching a
file from a machine you cannot otherwise
reach needs no screen and no shell
craft.

Like the Desktop tab, this one is
**documented-only** in this guide's lab:
described from the project's
documentation, not driven. The machinery
under it is the same agent channel the
lab proved for terminal work; the tab's
own behaviour is labelled, not claimed.

What the person at the machine sees:
nothing, again — which is why rights
(chapter 9) can take this door away
separately: a helper can hold remote
control *without* files, or files
without control, and the difference is a
checkbox you set on purpose.

## One connection, three doors

Notice what the three doors share: the
agent's single outward connection, the
ServerID check at its start, and the
rights check at yours. If a machine is
online, all three doors exist; your
rights decide which of them open for
you. That is the whole architecture of
daily use — and it is why the next
chapter does not admire the doors, but
tests the hinges.
