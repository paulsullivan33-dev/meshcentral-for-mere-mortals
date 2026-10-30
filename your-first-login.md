# Your First Login

By the end of this chapter you have
signed in to your console and — just as
important — you know what a *real* login
looks like, as opposed to one that merely
looks fine. The check: the page after
login shows **your account name** and a
**logout** link, not another password
box. This guide's lab did the whole flow
with its sleeves rolled up, in transcript
t05.

## Signing in

Open the server's address in a browser —
`https://` and the name you gave it. The
browser warns about the self-signed
certificate; for your own server, on
your own network, at this stage, that
warning is expected (chapter 10 deals
with making it go away properly). Past
it sits a plain page: "MeshCentral -
Login", a username, a password, a button.

Type the administrator account from
chapter 3 and sign in. You land on the
console: your account name on the page,
the **My Devices** view (empty, for
now), and a logout link. That is the
whole ceremony — deliberately. The
interesting part is underneath.

## What actually happened

Your browser sent the username and
password to the server's `/login`
address, and the server answered with
two **cookies** — small named values the
browser stores and presents from then
on, so you do not type the password on
every click:

- **`xid`** — your session token, the
  proof you signed in;
- **`xid.sig`** — its signature, so the
  token cannot be edited into someone
  else's.

The lab captured exactly this with curl
(t05): the same two cookie names in the
jar, and the reply carrying the
application page itself. Every later
thing the console does — listing
machines, running commands — rides on
those cookies over the control channel
(chapter 2). Two consequences worth
knowing now:

- **Whoever holds the cookies holds the
  session.** It is the web's usual
  bargain; it is why the console should
  only ever be reached over HTTPS, and
  why you log out on a machine that is
  not yours.
- **The cookies outlive the server's
  restart.** Sessions are signed, not
  stored as secrets on the server, so a
  restart does not sign everyone out.

## The trap: a failed login looks calm

Here is the detail that bites. A *wrong*
password does not produce an error page
or a different status code. The server
answers **200** — the same as success —
but returns the **login page again**,
with the word **Invalid** on it. Any
check that only asks "did the page
answer?" will call a failed login a
success. The lab met this while signing
in as its second user (t11) and it is
worth meeting early, in a chapter,
rather than late, in a script:

**Judge a login by the page you land on,
never by the status code alone.** Your
name and a logout link mean in. A
password box means out, whatever the
number said.

## Looking around, briefly

Signed in as administrator, the page
offers more than a non-administrator
will ever see — account management among
it (chapter 9). For now, note three
landmarks and move on: **My Devices**,
where your groups and machines will
live; **My Account**, where your own
password and sign-in options sit; and
the **event views**, where the server
shows its diary. The next chapter makes
the first group, so My Devices stops
being empty.
