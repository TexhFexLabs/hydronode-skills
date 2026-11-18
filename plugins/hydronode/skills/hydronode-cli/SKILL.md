---
name: hydronode-cli
description: Use when running or scripting the HydroNode command-line tool (`hydronode` or its alias `hn`), e.g. to list sensors, summarize values, export readings, watch live data, push or simulate a device, update firmware, or when a hydronode command fails with an auth or exit-code error.
---

# Working with the HydroNode CLI

`hydronode` is the command; `hn` is the same program under a short name where it is installed (Homebrew,
install scripts, winget; not by default on Snap). Use `hydronode` unless the user uses `hn`.
`hydronode help <command>` shows purpose, options and examples.

## Always script with `--json`

Tables are for people. In scripts and when you parse output, pass `--json` (stable shape) and use `jq`.

```bash
hydronode sensors --json | jq -r '.[].name'
hydronode values <point-id> --from 7d --json | jq '.avg'
```

## Exit codes

| Code | Meaning | What to do |
|---|---|---|
| 0 | ok | |
| 1 | error (network, server) | read the message; retry later |
| 2 | wrong usage (bad option, bad time, missing `--yes` without a terminal) | fix the command; see `hydronode help <command>` |
| 3 | not signed in or not allowed | `hydronode login`; read-only token (`hrt_`) cannot write, use a browser/device login or a `hat_` token |
| 4 | not found | check the id with `hydronode sensors` or `hydronode status` |

## Sign in

- `hydronode login` asks how. `hydronode login --web` (browser), `hydronode login --device` (code on another device, for SSH
  sessions), `hydronode login --with-token < token.txt` (API token from stdin; prefer over `--token`).
- Tokens live in the OS keychain, never in the config file. `hydronode whoami` shows who and with what rights.
- Profiles for a second account or server: `hydronode profile add work --server https://hydronode.tech`, then `hydronode -p work login` and `hydronode -p work …`.

## Typical tasks

```bash
hydronode status                                    # devices, anomalies, messages at a glance
hydronode values <sensor-id>/temperature --from 7d  # summary, at most 48 steps
hydronode values <sensor-id>/soil_moisture --below 30 --from 30d   # periods below a threshold
hydronode values compare <point-id> --shift 7d     # this week vs last week
hydronode watch                                     # live values (TUI), --plain for logs
hydronode console <sensor-id> --rejected            # why a device's data was refused
hydronode export --from 30d --format parquet        # CSV, JSON or Parquet
hydronode simulate <sensor-id> --kind weather --every 30s   # fake device with signed values
```

## Be careful

- `set`, `command`, `devices update`, `sensors delete` change real devices or data. Say what will
  change and get a yes before running them. Destructive commands ask; in scripts pass `--yes` only
  when the user asked for it.
- `simulate` and `push` write real readings into the sensor. Use a test sensor.
- `sensors credentials` and `tokens create` print secrets. Do not paste their output into chats,
  logs or files that get committed.
- Prefer summaries over `--raw`; raw readings are large.
