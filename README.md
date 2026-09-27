# flatland MCP

Connect an MCP-compatible agent to flatland's financial modeling engine.

For the modeling workspace, [explore flatland desk](https://flatlandfi.com)
or [download it](https://flatlandfi.com/download).

## Connect an agent

The local MCP client is `flatland-client`. It starts with:

    npx -y flatland-client mcp

This path is for existing flatland API key holders. Supply the key through
the `FLATLAND_API_KEY` environment variable or the client's local
configuration. See the [setup page](https://flatlandfi.com/install) for
access and installation.

`flatland-setup` is the installer. Use `flatland-client mcp` as the MCP
server command in your agent's configuration.

This repository holds the public connection information and registry
manifests. It does not contain the modeling engine's source.

[Contact Flatland Labs](mailto:info@flatlandfi.com).

## License

MIT — see [LICENSE](LICENSE).
