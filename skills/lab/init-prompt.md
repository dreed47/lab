# Build a lab config

You are setting up the `lab` homelab front door for a new user. Do not invent host names, addresses, or guest numbers. Ask, then generate the file with `lab init`. Do not hand-write the TOML.

## Ask

1. Which SSH host can run `pvesh` for the cluster? That is `--cluster`.
2. Which SSH hosts are cluster nodes? Comma-separated `--nodes`.
3. Any other SSH hosts that are not cluster nodes? `--shell`. A laptop that moves does not belong here.
4. LAN prefix for VM addresses, such as `10.0.0.`? `--lan`. Empty is allowed.
5. Which SSH users should a VM login try, in order? `--ssh-users`. Default `root`.
6. Optional. Home Assistant guest id, the node that runs it, and its URL.
7. Optional. Zigbee guest ids and labels, as `id:Label,id:Label`, and the config path if they want `lab find` to search friendly names.
8. Optional. Camera or recorder host, address, URL, and recordings mount.
9. Optional. Backup window `HH:MM-HH:MM` and a one-line note.
10. Optional. Named pages, each `name=url`.

Skip a question if they do not have that service. Do not guess.

## Write

Preview first:

```bash
lab init --print --cluster node-a --nodes node-a,node-b --shell camera --lan 10.0.0.
```

Show them the preview. After they accept it, add `--write`. If a config already exists, add `--force` only after they agree to replace it. The file goes to `~/.config/lab/config.toml`. Do not commit that file. The preview may list local SSH host names. Do not post that list.

Then run `lab --self-check` and one live command they expect to work, such as `lab status`.
