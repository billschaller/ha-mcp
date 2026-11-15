# teamscha fork notes

Private-use fork of homeassistant-ai/ha-mcp, branched from the reviewed release tag
(`teamscha/v9.2.0` = upstream `v9.2.0`, commit 51e3aac). It is built locally as a Home
Assistant local add-on; no upstream container image is pulled.

Changes from upstream, all in `homeassistant-addon/config.yaml`:

- no `image:` — the Supervisor builds the image from this source;
- `host_network: false` and port 9583 unmapped — reachable only from other add-ons on the
  box's internal network, not from the LAN;
- no `discovery: mcp` — Home Assistant is not offered this server for its own assistants;
- `hassio_role: default` instead of `manager` — no add-on, store or backup management;
- defaults: `redact_secrets: true`, `disabled_tools: "ha_manage_app"`.

Its only intended client is the in-house Claude agent add-on, which classifies every tool
call into risk tiers itself and does not rely on this server's read-only annotations.

To take a newer upstream release: review the diff from the current base tag, create
`teamscha/<tag>` from it, and re-apply the config changes above.
