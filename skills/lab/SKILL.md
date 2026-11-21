---
name: lab
description: "Use when the homelab comes up. Run lab first."
version: 1.0.0
license: MIT
platforms: [linux]
metadata:
  hermes:
    tags: [homelab, lab, ssh]
---

# lab

## When to Use

Use when the user asks about their homelab, a node, a guest, or a service `lab` is configured for. Run `lab` before probing by hand.

Reports stay short: bullets, no walls of text.

`lab` is a homelab front door. One Python 3 file plus OpenSSH. It does not start, stop, or migrate guests. House-specific names live in config, not in this file.

## Where it lives

- Command: `lab` on `PATH`, usually a symlink to the repo file
- Config: `~/.config/lab/config.toml` (copy from `lab.example.toml`)
- A missing section means that command is not configured. Do not guess guest numbers or addresses.

## Rules

- Homelab questions go through `lab` first. Do not invent a second cluster script.
- New commands go in the single `lab` file, then `lab --self-check`. Self-check does not SSH.
- `lab` uses `BatchMode`. A password prompt means the key or `~/.ssh` ownership is broken, not that the host is down.
- `lab shell` takes the remote program and each argument as separate argv. One quoted string is quoted again and run as a single command name.
- Do not ship a remote probe as an encoded payload. Run the read command directly.
- Cluster reads (`pvesh`) run on the configured `cluster` host. `pct exec` and `docker ps` run on the node that hosts the guest.
- A name in `shell_hosts` but not `cluster_nodes` is a shell target only. `lab on` will refuse it.
- Zigbee search reads `friendly_name` lines only. Do not read `network_key` or print tokens from a process command line.
- Do not start, stop, or migrate guests.

## Commands

```bash
lab status              # quorum, nodes, configured camera host, every guest
lab status --json
lab on <node>           # guests on one cluster node
lab where <name>        # name or guest id
lab find <word>         # guest names and Zigbee friendly names, if zigbee is configured
lab shell <host>        # SSH to a shell host. Add a command to run one and return
lab guest <name>        # login to a container or VM
lab ha                  # Home Assistant guest from config, if set
lab frigate             # camera host from config, if set
lab zigbee              # Zigbee guests from config, if set
lab tasks               # cluster jobs since yesterday that need a look
lab mem                 # RAM and swap
lab storage
lab recordings          # recording disk from config, if set
lab open <name>         # URL from guest notes, or a name under [pages]
lab --self-check        # local checks, no network
```

Stopped guests are refused. Two guests with the same name are refused. Use `lab where` and the number.

A new guest shows up in status, on, where, guest, and open with no edit. `lab open` needs an `open:` line in the guest notes, or a name under `[pages]`.

## First setup

Do not hand-write the config. Follow `init-prompt.md` in this directory, then run `lab init`. Preview with `--print`. Save with `--write` only after the user accepts the preview.

