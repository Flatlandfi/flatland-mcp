# flatland MCP

Connect your agent to a model in flatland desk.

[Explore flatland](https://flatlandfi.com) or
[download flatland desk](https://flatlandfi.com/download).

## Connect through flatland desk (0.2)

These steps are for a 0.2 build with the **Your own agent** panel. If your
installed build does not show that panel, check the download page for the
current release.

1. Open flatland desk and open the model you want to work on.
2. Open the Agent drawer and choose **Your own agent**.
3. Turn on **Let my own agent propose to this model**.
4. Copy the setup for your agent and environment. Run the copied command in
   your terminal, or paste the copied configuration into your agent's MCP
   settings, as the panel directs.
5. Start a new agent session if your agent loads MCP settings only at startup.
   Ask it to connect to flatland.
6. In Desk, check the model and program shown in the access prompt, then
   choose **Allow**.

The panel provides setup for Claude Code, Codex, Cursor and Claude Desktop.
Use the setup Desk provides for your installation, including the WSL line
when connecting from WSL. Desk does not edit your agent's configuration.

No flatland account or API key is needed for this local connection. Your agent
can inspect the open model, run calculations with Desk's local engine, and
propose changes. You accept or reject those proposals in Desk.

The local connection does not control how your agent handles model data.
Check your agent's own data settings before giving it access to a model.

## Troubleshooting

- **The agent cannot connect:** keep Desk open, check that access is turned on
  for the model, and use the setup copied from that installation. Another
  Desk window may already hold the connection.
- **The agent's tools do not appear:** check its MCP configuration and start a
  new agent session.
- **The agent is waiting:** look in Desk for an access prompt or a proposal
  waiting for your decision.
- **You opened a different model or used Save As:** reconnect to the model you
  want the agent to work on and approve the new session.
- **You want to stop access:** choose **Disconnect** for that agent in the
  panel, or turn off **Let my own agent propose to this model**. Remove the
  flatland MCP entry from your agent's configuration if you no longer want
  it configured.

## Existing API-key holders

The legacy hosted connection uses a different client:

```sh
npx -y flatland-client mcp
```

This command is for existing flatland API-key holders. Supply the key through
the `FLATLAND_API_KEY` environment variable or the client's local
configuration. It keeps model files on your machine and sends model data to
the hosted engine for computation. It does not connect to the model open in
Desk.

Use Desk's **Your own agent** setup for the local connection described above.

## About this repository

This repository holds public connection guidance and legacy registry
manifests. The `smithery.yaml` and `.well-known/mcp` files describe the
API-key client, not Desk's local connection. Editing them does not update an
existing third-party listing.

The modeling engine's source is not in this repository.

[Contact](mailto:info@flatlandfi.com).

## License

Files in this repository are MIT licensed — see [LICENSE](LICENSE).
