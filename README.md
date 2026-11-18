<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="docs/logo-dark.svg">
    <img src="docs/logo-light.svg" alt="HydroNode" width="96">
  </picture>
</p>

<h1 align="center">HydroNode skills</h1>

<p align="center">
  HydroNode for Claude: the hosted MCP server plus skills for condensed history, safe writes
  and scripting with the <code>hydronode</code> CLI.
</p>

<p align="center">
  <img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-blue">
  <img alt="Claude Code plugin" src="https://img.shields.io/badge/Claude%20Code-plugin-8A63D2">
</p>

## Install

**Claude Code**

```bash
claude plugin marketplace add TexhFexLabs/hydronode-skills
claude plugin install hydronode@hydronode
```

**Claude Desktop:** add the marketplace `TexhFexLabs/hydronode-skills` in the plugin settings and install
`hydronode`.

The plugin brings the HydroNode connector (`https://hydronode.tech/mcp`) and the two skills. On first use
your browser opens HydroNode: sign in and choose which projects Claude sees and whether it may switch
things. Change or revoke that anytime under <https://hydronode.tech/account/security#connected-apps>.

## What is inside

| Skill | Loads when | Teaches |
|---|---|---|
| `hydronode-mcp` | the HydroNode MCP tools are connected | top-down lookup (`overview` → `find` → `get_sensor` → `summarize_history`), diagnosing offline devices, asking before every write, dry-run automations, what "not found" and "not granted" mean |
| `hydronode-cli` | you work with the `hydronode` / `hn` command | `--json` output, exit codes, profiles, login choices, typical scripts (export, watch, simulate, push) |

The plugin contains no credentials and runs nothing on your machine. The connector talks to
`https://hydronode.tech/mcp` only after you signed in and allowed it; the skills only guide how Claude uses it
and the CLI you installed yourself.

## Without the plugin

- **MCP only:** add a custom connector with the URL `https://hydronode.tech/mcp` in Claude (Settings ›
  Connectors). Guide: <https://hydronode.tech/docs/guide/mcp>.
- **CLI:** install `hydronode` and run `hn login`. Guide: <https://hydronode.tech/docs/guide/cli>.

## License

MIT, see [LICENSE](LICENSE).
