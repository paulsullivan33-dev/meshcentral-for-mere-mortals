# Writing criteria for this guide

Every "for Mere Mortals" guide is written to the same nine-point
standard, so a reader who trusts one can trust the rest. Here it
is, with the verification notes for this particular guide below.

1. **Fix it first.** Reader outcomes lead, not action items: each
   chapter opens by naming the outcome it delivers, shows a check
   the reader can run to confirm they got it, and a reasonable
   reader finishes able to state what was done, what it means,
   and what to try next.
2. **Plain language.** Short sentences, everyday vocabulary,
   technical terms defined on first use. No slang, and no
   idioms that only make sense in one country — the reader may
   be translating as they go.
3. **No dead ends.** A guide never tells the reader to do
   something it cannot show them how to verify. Every claim a
   reader relies on — an install, a command, an output — is
   something this guide demonstrates or clearly labels
   documented-only below.
4. **Live-verified where it matters.** Procedures are run for
   real in the guide's lab wherever the build machine allows it,
   and the transcripts kept in the repository are the evidence.
   What could not be run is listed honestly below, never
   presented as if it had been.
5. **General audiences.** Nothing in this guide — examples,
   fixtures, names, addresses — is modelled on any particular
   reader or author's real life, network, or organisations.
   The lab's accounts are labadmin and labtech; its example
   people and machines are invented.
6. **Standalone.** A reader needs this guide, its lab, and
   nothing else. Where another guide would genuinely help, it
   is pointed to once, by name, and the chapter still completes
   without it.
7. **Honest about limits.** Chapter 13 names what the tool
   cannot do: no agent means no control, no screen means no
   desktop, one server is a single point of failure and of
   compromise, agents run with each machine's highest
   privileges by design — and, separately, what this guide's
   own lab could not reach.
8. **The ethics rule is in the text, early.** A remote-control
   console is a master key, and the guide says so in the
   README and chapter 1, before any procedure: protect the
   console like a password vault, name the server so agents
   can verify it, give every person their own account, grant
   narrowly per group, and use consent settings so sessions
   on other people's machines announce themselves. Chapter 10
   turns the rule into a checklist.
9. **Builds clean.** The site builds with MkDocs in strict mode
   with no warnings, and a fresh reader following the chapters
   in order reaches the stated outcome of each.

## Verification notes for this guide

The build machine is a small Ubuntu 24.04 sandbox (x86-64,
Node.js v24.22.1, npm 10.9.4, running as root). MeshCentral
**1.3.1** was installed the official way, `npm install
meshcentral` (181 packages), and run unmodified. Server and
agent both ran on this one machine, over loopback
(127.0.0.1), with the server's self-signed certificates. All
transcripts live in `meshcentral-lab/transcripts/`, numbered
in the order the work happened (t00–t12). Passwords appearing
in the lab were throwaway lab values, labelled as such; cookie
values were never printed.

Run for real, with transcripts as evidence:

- Environment, the npm install, and the version read back
  (t00).
- First run: certificates generated (root, web, agent,
  code-signing, MPS), the data folder created, 31 stock agent
  files (119 MiB) downloaded, LAN mode, HTTPS answering on
  443 and HTTP redirecting on 80; the code-signing timestamp
  warnings recorded and explained in chapter 14 (t01).
- The login page answered by curl: HTTP 200, 75,730 bytes,
  title "MeshCentral - Login" (t02).
- Administrator account created and promoted with the server
  stopped (`--createaccount`, `--adminaccount`), and a second,
  ordinary account created the same way (t03, t04).
- The real login flow: POST to /login answered 200 with the
  application page (account name and logout links present)
  and the xid / xid.sig session cookies issued (t05).
- A device group ("Lab Machines", agent type 2) created
  through the control channel; the reply's MeshID and the
  creator's full rights (4294967295) recorded (t06).
- A genuine agent pair downloaded from the server for the
  group: the Linux x86-64 agent (type 6, ELF, 3,757,520
  bytes — byte-size identical to the server's stock agent)
  and its settings file, whose five operative lines are
  quoted in chapter 2 (t07).
- The failure, diagnosed rather than hidden: in LAN mode the
  settings file said `MeshServer=local`; with the address
  hand-corrected the agent still refused, with
  `Mesh Server Connection Error [13]` then `[12]`, because
  the server's certificate was made for "un-configured". The
  ServerID was verified by hand to be the SHA-384 of the
  agent certificate's RSA public key (PKCS#1 DER) (t08).
- The fix: the server was named (`settings.cert` set to its
  IP address; the sandbox's /etc/hosts is read-only, so no
  DNS name could be used), certificates regenerated,
  Hybrid mode, the new web certificate carrying the address
  as a subject alternative name — after which the fresh
  settings file carried a real address,
  `wss://127.0.0.1:443/agent.ashx` (t08).
- The agent connected ("Connected." / "Server verified
  meshcore"), appeared in its group through the control
  channel with `conn: 1`, `pwr: 1`, and its connection was
  written to the server's event log (t09).
- A command sent to the machine through the console's
  control path and its output returned: a unique marker,
  the hostname, the account it ran as, and uptime (t10).
- The rights fence in both directions: the ordinary user
  signed in and was shown *no* devices (`"nodes":{}`); an
  administrator password reset for that user through the
  control channel also worked (t11). A grant of the single
  remote-control right (bitmask 8) made the device visible;
  removing the grant made it invisible again (t12).

Documented only — described from the project's documentation,
not run, and the text does not claim otherwise:

- Driving the graphical **Desktop** tab and using the
  **Files** tab in a browser. The lab machine runs no
  graphical session, so no desktop existed to capture; the
  terminal command path beneath those tabs is the part the
  lab proved (t10).
- Installing agents as system services (Windows installer,
  Linux service install). The lab ran the agent in the
  foreground and in the background to observe it.
- Agents for Windows, macOS and other architectures; the
  lab ran only the Linux x86-64 agent it downloaded.
- Reaching the server from another machine, a real network,
  or the internet; DNS names; certificates from a real
  authority; reverse proxies. The sandbox's hosts file is
  read-only, which is why the lab's server is named by IP
  address.
- Two-factor sign-in and security keys — prescribed in
  chapter 10, not enabled in the lab.
- Intel AMT groups and the MPS channel, user groups,
  email-based account features, and multi-server setups.
- The neighbour tools of chapter 12 (RustDesk, SSH, VNC/RDP,
  the commercial cloud tools, Cockpit) — characterised, not
  run or benchmarked.

Fixtures are this guide's own and deliberately generic: two
lab accounts (labadmin, labtech), a group called "Lab
Machines", example.org addresses, and invented people and
machines (a helper called Sam; kitchen-pc, Family Laptops) in
the prose. The one real name in the transcripts is the sandbox
host's own hostname, which the agent reported about itself.
