# Space plugin and skills

[Space](https://getspace.sh) gives your AI agents one shared memory and workspace. A decision, a preference, a document or a task saved from one agent can be recalled by every other agent you authorize: Cursor, Claude, ChatGPT, Codex, or an agent on a server.

This repository is the Space plugin for Cursor and Claude, and the source of the Space skills. The plugin bundles three things:

| Part | File | What it does |
|---|---|---|
| Space MCP server | [`mcp.json`](mcp.json) for Cursor, [`.mcp.json`](.mcp.json) for Claude | Connects the agent to `https://api.getspace.sh/mcp/`, with Space's own sign-in |
| Skills | [`skills/`](skills/README.md) | Seventeen workflows: recall what was decided, remember a lesson, brief a project, track tasks, keep a database, review a day or a week, and more |
| Memory rule, in Cursor | [`rules/space-memory.mdc`](rules/space-memory.mdc) | Asks the agent to use Space as shared memory: retrieve context before project work, save confirmed decisions, and never store secrets. In Claude, the Space server's own instructions say the same. |

The plugin runs no code on your computer. It holds instructions and the address of Space's MCP server, and everything the agent reads or saves in Space goes through that server, after you sign in.

## Before you install

You need a Space account at [app.getspace.sh](https://app.getspace.sh) with a plan. A new account picks a plan before it can write; [pricing](https://getspace.sh/#pricing) lists the plans and their free trials.

## Install in Cursor

From the Cursor Marketplace, search for Space and install it.

To try the plugin from this repository, clone it into Cursor's local plugin folder, then run **Developer: Reload Window**:

```sh
git clone https://github.com/Hugo-SEQUIER/space-skills.git ~/.cursor/plugins/local/space
```

The first time the agent calls a Space tool, Cursor opens Space's sign-in in your browser. Choose the Space, and grant read-only access or write access as well. You can revoke the connection at any time from **Agents** in Space.

## Install in Claude

Once the plugin is listed in Claude's directory, add it from there. Until then, add this repository as a plugin marketplace in Claude Code and install the plugin from it:

```text
/plugin marketplace add Hugo-SEQUIER/space-skills
/plugin install getspace@getspace
```

Then run `/mcp`, select `space` and sign in. Space's sign-in opens in your browser: choose the Space, and grant read-only access or write access as well.

## Use the skills in other agents

Each folder under `skills/` is a standard skill (`SKILL.md`) that works on its own in any client that reads skill folders, such as Codex or Hermes. [`skills/README.md`](skills/README.md) describes every skill and where to install it. A skill does not connect anything by itself: connect the client to Space as described in the [connect guide](https://getspace.sh/docs/connect).

## Privacy and support

Space stores only what you or your agents save, never imports your chat history, and encrypts documents, tasks, records and memory text before storing them. See the [privacy policy](https://getspace.sh/privacy). For help, write to support@getspace.sh.

## License

MIT. See [LICENSE](LICENSE).
