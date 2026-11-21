# Install lab

You are installing the `lab` homelab front door for the person you are talking to. Do the steps below. Do not invent host names, addresses, or guest numbers. Do not copy anyone else's config. Do not start, stop, or migrate guests.

## Install

```bash
git clone https://github.com/dreed47/lab.git ~/code/lab
ln -sfn ~/code/lab/lab ~/.local/bin/lab
```

`~/.local/bin` must be on `PATH`. If `lab` is not found after the symlink, tell the user. Do not rewrite their shell config unless they ask.

If `~/.hermes/skills/lab` already exists and is not a symlink to this checkout, leave it. That is their private skill. Otherwise:

```bash
mkdir -p ~/.hermes/skills
ln -sfn ~/code/lab/skills/lab ~/.hermes/skills/lab
```

## Config

Read `~/code/lab/skills/lab/init-prompt.md` and follow it.

Ask the questions in that file. Skip a service they do not have. Preview with `lab init --print`. Write with `--write` only after they accept the preview. If a config already exists, `--force` only after they agree to replace it.

Do not commit `~/.config/lab/config.toml`. The preview may list local SSH host names. Do not post that list.

## SSH

`lab` does not create keys and does not copy keys from anywhere else. SSH to their cluster must already work with no password prompt. If it does not, stop and say so.

## Finish

Run `lab --self-check`, then one live command they expect to work, such as `lab status`. Report what those commands printed. A password prompt means the key is broken, not that a host is down.
