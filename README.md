# Muse

Personal clothing storefront skills for taste, saves, dismissals, and closet notes. Purchases stay on retailer sites.

This directory is the whole plugin. Published, these files sit at the repository root of [myachhadia/muse-plugin](https://github.com/myachhadia/muse-plugin), not inside a `plugin/` folder. The private Muse repo keeps the rack, catalog, photos, and server.

## MCP server

Muse is hosted at `https://muse-mcp.mya-chhadia.workers.dev/mcp`. Connect by signing in with your own Muse account over OAuth. There is nothing to self-host.

`.mcp.json` and `mcp.json` both use that URL. Do not commit a token or key.

The two MCP files are the same JSON. `.mcp.json` is the filename this package publishes for Open Plugins clients. `mcp.json` is the Agent Plugins 1.0.0 and Cursor template location. Both use the closed Agent Plugins shape: `$schema`, `mcpServers`, and a `streamable-http` URL.

## Layout

```text
plugin.json                 Agent Plugins manifest
.cursor-plugin/plugin.json  Cursor plugin manifest
.mcp.json                   hosted MCP URL
mcp.json                    same hosted MCP URL
skills/*/SKILL.md           curate, log a decision, plan an outfit
agents/muse.md              storefront agent
PRIVACY.md                  what is stored, and what is not
```

## Skills

| Skill | Use when |
| --- | --- |
| `curate-storefront` | Read feedback, then write this person's recommendations. Also edit taste, brands, or styles. |
| `log-decision` | Read reactions before the next recommendations, and record why they saved or dismissed something. |
| `plan-outfit` | Plan from closet items they added, or record a purchase approval note. |

The storefront is only what this person's bot writes with `add_recommendations`. Call `list_feedback` before writing a new batch. A missing price stays unknown. An image URL is stored only when the bot already has one. Nothing here fetches a retailer photo.

## Tools

`get_taste_summary`, `update_taste_summary`, `list_brands`, `add_brand`, `remove_brand`, `list_styles`, `add_style`, `remove_style`, `get_storefront`, `add_recommendations`, `clear_recommendations`, `list_feedback`, `save_item`, `dismiss_item`, `list_saved`, `record_purchase`, `add_closet_item`, `list_closet_items`.

`record_purchase` records approval only. It never places an order or takes payment. See [PRIVACY.md](PRIVACY.md).

## Install

Point an Agent Plugins client at this directory. It reads `plugin.json`, `skills/`, and `mcp.json`.

In Cursor, this directory is a single plugin: `.cursor-plugin/plugin.json`, `skills/`, `agents/muse.md`, and `mcp.json`. There is no marketplace manifest because the published repo contains one plugin at the root.
