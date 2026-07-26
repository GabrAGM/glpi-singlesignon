---
title: Overview
audience: technical
last_reviewed: 2026-07-26
---

# GLPI Single Sign-On Plugin

This is AGM's fork of [`edgardmessias/glpi-singlesignon`](https://github.com/edgardmessias/glpi-singlesignon),
a [GLPI](https://github.com/AGM-One-Vision/glpi) plugin that adds
`Login with <provider>` buttons to the GLPI login page, backed by OAuth2/OIDC.

## What it does

The plugin registers itself as a GLPI authentication hook. When enabled, it
renders one login button per configured provider (`Configuration > Single
Sign-On`). Clicking a button drives the standard OAuth2 authorization-code
flow against the provider's `authorize` / `access_token` / userinfo
endpoints (defined per-provider in `providers.json`), then maps the returned
identity onto a GLPI user account.

## Provider used at AGM

AGM configures the **Azure AD** provider so staff log into GLPI with their
AGM Microsoft 365 account, against the same Azure AD tenant that
[`glpi-mcp-auth`](https://github.com/AGM-One-Vision/glpi-mcp-auth) uses to
authenticate MCP callers. The two integrations are independent — this plugin
authenticates browser logins to the GLPI web UI; `glpi-mcp-auth` is a
separate service authenticating MCP/Claude Code callers — but both trust the
same Azure tenant.

Other providers ship in the plugin (Google, GitHub, Facebook, LinkedIn,
Instagram, and a Generic OAuth2 provider) but aren't configured at AGM today.

## Installation

Standard GLPI plugin install: drop the plugin into
`<GLPI_ROOT>/plugins/singlesignon`, then enable it from
`Configuration > Plugins`. See the
[upstream provider configuration wiki](https://github.com/edgardmessias/glpi-singlesignon/wiki/Plugin-Provider-Options)
for the exact fields each provider needs (client ID/secret, tenant, scopes).

## Related

- [`glpi`](https://github.com/AGM-One-Vision/glpi) — the host application this plugin runs inside
- [`glpi-mcp-auth`](https://github.com/AGM-One-Vision/glpi-mcp-auth) — separate Azure AD-authenticated MCP server for AI/Claude Code access to GLPI
