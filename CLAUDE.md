# hydronode-skills — notes for coding agents

Claude plugin marketplace `hydronode` with one plugin `hydronode`: the HydroNode connector (`plugins/hydronode/.mcp.json`,
remote `https://hydronode.tech/mcp`) and two skills (`hydronode-mcp`, `hydronode-cli`).

- Skills follow the Agent Skills format (`SKILL.md` with `name` and `description`); keep them short and practical.
- The CLI command in texts is `hydronode` (`hn` only where the user uses it).
- Check with `claude plugin validate .` and `claude plugin validate plugins/hydronode` before pushing.
- Release: bump `version` in `plugins/hydronode/.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json`,
  push to `main`. Users get it with `claude plugin marketplace update hydronode`.
- No credentials, no scripts that run on their own.
