---
name: fleet-netbird-onboarding
description: >
  Onboard a machine to the owner's NetBird fleet with independently authenticated
  SSH trust, least-privilege access policy, verified mesh SSH, deliberate service
  persistence and cleanup. Use for adding a fleet host, NetBird enrollment,
  connected-but-missing peers, new-machine SSH bootstrap, or simplifying repeated
  onboarding. Establish machine access first; Pi/router/worker setup is separate.
---

# Fleet NetBird onboarding

## Outcome and operating principle

Deliver working, trustworthy **management-machine -> target mesh SSH**, not just
an installed client or a dashboard entry. Aim for one owner-local bootstrap,
one private enrollment/login and one independent host-trust confirmation.
Do not promise those steps can always be eliminated.

Follow the current user and repository instructions, including
`~/.pi/agent/AGENTS.md` when present, especially the private-network, privilege,
delegation and functionality-first policies. This skill grants no new authority. Historical host facts, releases and scripts are
examples/evidence, **not reusable approvals or executors**.

Keep this small: use supported tools and existing installers; no bespoke approval
system, certification framework, exhaustive matrix or repeated status polling.
A short progress note and a focused real connection test are sufficient.

## 1. Agree the bounded scope once

Before mutations, establish:

- Physical target identity, owner-confirmed hostname/user and intended machine.
- Management/source machine and permitted transport. NetBird is the default;
  LAN needs an explicit endpoint-specific temporary exception, never fallback.
- Whether approval includes install, client start, **boot autostart**, required
  SSH/key/firewall setup and cleanup. These are different permissions. No reboot,
  linger, root worker daemon or unrelated service change by inference.
- Exact proposed access-policy/group changes, if any. General onboarding or
  dashboard inspection authority is not permission to invent or broaden ACLs.
- Owner-private enrollment/authentication and independent SSH host-trust method.

Bundle known, specifically described steps into one scope where possible rather
than asking again at every harmless step. Ask again only at a real authentication,
new authority or material-risk boundary. Do not ask users to repeat facts or send
new photographs when existing evidence is sufficient.

## 2. Check effective access policy EARLY

**Enrolled/Connected does not mean authorized to reach another peer.** Before
assuming transport trouble, inspect the intended group's effective policy and,
when available, the dashboard's **Accessible Peers** view.

- Determine actual assigned custom groups, source/destination identities, enabled
  rule, direction, protocol/port and any applicable posture/approval restrictions.
- Do not assume approval/posture features exist on the account's plan.
- Compare intended access with current client peer maps. Dashboard accessible-peer
  lists can distinguish management exclusion from client update propagation.
- Treat user-reported group membership respectfully; if observed facts differ,
  describe the exact difference without endlessly repeating the same question.

Prefer the fleet's existing least-privilege convention. For a new management SSH
path, an appropriate **proposed**, separately approved delta is:

1. A dedicated singleton `peer:<target>` group containing only the verified host.
2. One enabled, one-way TCP rule from the existing management-host singleton group
   to that target group, restricted to the **verified actual SSH port**.

Do not place a new host in another host's singleton group. Do not enable broad
Default All-to-All, grant reverse initiation, or add unrelated ports merely to
make discovery work. Source and destination can both appear in peer maps even
when initiation is one-way; visibility is not reverse-access permission.

Dashboard inspection must use an authorized machine/session. Follow GUI model
and harness preferences, including any explicit task-specific user override;
read the relevant computer-use skill first. Default GUI delegation uses Astra,
not the coding model. Every child uses Pi in its own separate unfocused Herdr tab,
natural `HERDR_ENV=1`, discovered CLI syntax and inherited safeguards. Preserve
human apps/drafts/focus. Never borrow another desktop when the authorized target
is unavailable. Stop for private owner authentication; do not collect cookies,
admin tokens, browser credential stores, password fields or login links.

## 3. Minimal owner-local bootstrap

Inspect the target before installing: OS/architecture, existing NetBird binary and
service, real SSH listener/port, login user and any active-use conflicts. Avoid
credential-bearing config/environment dumps or unrelated-session investigation.

- Use a supported distribution package or official upstream release with checked
  provenance/checksum. If absent from repositories, do not invent an AUR package or
  execute an unreviewed curl-pipe installer. Inspect help and service behavior.
- Preserve existing software/config/identity. Refuse an unexpected existing install
  rather than silently overwrite, migrate, reset or re-enroll it.
- Add only the management machine's **public** client SSH key when approved. Keep
  the source's own private mesh identity on the source; never copy it to targets.
- Confirm native OpenSSH availability and the actual listening port. NetBird's
  built-in SSH and native OpenSSH are distinct; do not substitute one implicitly.
- Make only a specifically required and approved narrow firewall allowance.
  Record its exact source, destination, port/protocol/interface and whether newly
  added. Never disable the firewall or allow Anywhere/a subnet as a shortcut.
- Configure service persistence according to scope. `service install` may enable
  boot startup: inspect first. A transient service is **not durable onboarding**.
  Avoid duplicate daemons/sockets. Reattest owned unit/process identity before a
  transition; leave existing enrollment intact. No client lifetime cap.
- Use standard local sudo authentication when needed; never request passwords in
  chat or weaken sudo. Prefer one short, inspected local command over several
  long commands typed by the owner.

A helper, if needed, should be target-bound, no-clobber and safe against replay:
verify artifact/identity, record the consequential invoking step, then stop on
partial/ambiguous failure. Inspect actual state before any retry. Do not turn
these safeguards into a generalized installer framework.

## 4. Enroll privately; establish host trust efficiently

The owner performs the intended fleet SSO login locally. A supported restricted,
short-lived enrollment mechanism with suitable automatic groups may reduce work,
but requires explicit authority and private handling. Never put setup keys,
tokens, passwords or authentication URLs in chat, argv, reports or screenshots.

Have the bootstrap expose selected **nonsecret** facts only: hostname/user,
NetBird FQDN/IP, client state, SSH port and public Ed25519 key/full SHA256 fingerprint.
Prefer a public-key file plus a readable fingerprint, or a suitable QR/public-only
transfer, over transcribing a long Base64 key from photos.

- Authenticate the host fingerprint through physical owner inspection or another
  independently authenticated channel. A fetched public key is not its own trust.
- Compare the **complete** fingerprint. Plausible glyphs or a matching prefix are
  insufficient. Public key-scan requires its own specific exception where standing
  policy forbids it; never blind TOFU, `accept-new` or disable host checking.
- Pin the matching public key for the exact endpoint/port in a private per-task
  known-hosts file, preserving global known-hosts. Client-key and host-key
  fingerprints serve different purposes; never confuse them.
- For LAN -> mesh transition, authenticate/reconcile target identity and current
  mesh peer state before creating the mesh-endpoint pin from the trusted key.

## 5. Verify the real mesh path

Before each inter-machine connection, verify source hostname/user/UID and inspect
current read-only `netbird status --detail`. Reconcile the destination against
trusted inventory and authenticated enrollment facts. Stop on identity mismatch,
missing/unavailable peer or trust ambiguity; do not guess hostnames/IPs/ports.
Lazy-connection `Idle` is not automatically offline; distinguish it from a missing
peer or failed route. No unrelated-host probes, scans, proxy pivots or LAN fallback.

Use the source's own `~/.ssh/id_ed25519_netbird_mesh`, the exact verified mesh
IP/user/port, private pinned trust and strict noninteractive options:

```text
BatchMode=yes  StrictHostKeyChecking=yes  IdentitiesOnly=yes
ConnectTimeout=10  ConnectionAttempts=1
ServerAliveInterval=5  ServerAliveCountMax=2  ForwardAgent=no
```

Isolate task transport from unintended SSH config, multiplexing and forwarding
where appropriate (`-F /dev/null`, no agent/other forwarding, no connection sharing,
explicit private `UserKnownHostsFile`, no global trust updates). Do not weaken
verification to resolve a failure. First remote command should verify hostname,
username and UID; stop on unexpected identity. Bounded individual calls are useful;
there is no cumulative task/agent/client lifetime cutoff.

**Troubleshoot the exact failing layer:**

| Evidence | Next useful decision |
|---|---|
| Client needs login | Owner-private authentication, not policy or firewall changes. |
| Connected but counterpart absent; dashboard also excludes it | Inspect effective management rules/groups/approval/posture. |
| Dashboard allows counterpart but current client map omits it | Investigate update propagation; one scoped safe refresh may help. |
| Peer known, bounded TCP connection times out | Route/peer/port/firewall reachability; not yet host trust or public-key auth. |
| Host-key mismatch | Stop; reconcile independent trust. No bypass. |
| Public-key authentication denied | Check intended user/client-key installation without password fallback. |

Do not repeatedly poll/reconnect when it changes no decision. Client firewall
changes do not repair a management-delivered peer exclusion. A reconnect can disrupt
active peers, routes and DNS: inspect impact and obtain appropriate authority first.

Verified LAN bootstrap may support other explicitly approved setup while mesh policy
is unresolved. Do not make endless dashboard investigation a prerequisite for all
useful work, or claim LAN success proves mesh access.

## 6. Close bootstrap; report honestly

After mesh SSH succeeds, remove only newly added temporary LAN allowances and stop
only owned temporary transfer servers. Verify other firewall rules remain unchanged
and the firewall stays active. Then perform a final strict **mesh-only** SSH check.
Do not remove the last working bootstrap path before the replacement works.

Completion checklist:

- [ ] Target identity/enrollment and current source-peer discovery reconciled.
- [ ] Intended service is running; autostart enabled if requested; no duplicate daemon.
- [ ] Exact approved least-privilege policy applied; existing rules preserved.
- [ ] Independent host trust pinned; actual strict mesh SSH verifies hostname/user/UID.
- [ ] Temporary bootstrap exceptions/processes removed; mesh SSH works afterward.
- [ ] Owned GUI/agent work settled/cleaned up; human apps and unrelated work preserved.

State what was configured versus demonstrated. Autostart enabled is not a reboot
survival test; do not reboot merely to certify it. Preserve login/session-expiration
settings unless explicitly authorized to change them; mention possible future
private reauthentication. Record the verified endpoint/port/key/pin and concise
operating/recovery instructions. Useful reference commands are `netbird status
--detail` and `systemctl status netbird.service` when that is the actual installed
unit. Discover names rather than assume them.

NetBird completion does **not** authorize Pi/router/account setup, a worker install,
queue/pilot/model proof, persistent worker activation, Plane state changes or Done.
Hand off working machine access to those separate tasks.

## Lesson from a completed Linux onboarding

NetBird 0.79.0 enrollment worked, but the fleet's Default All-to-All was disabled.
The new host had no singleton SSH group/rule and saw only an application server
through an existing application-port policy. A narrow
`peer:management -> peer:target` TCP/22 policy
fixed visibility; strict mesh SSH worked without a new broad UFW allowance. A
permanent service replaced the deliberately transient bootstrap service, and the
exact temporary LAN rule was removed. Check effective policy early; do not replay
that machine's consumed scripts, IPs, PID bindings or approval history.
