# Glossary

Domain terms of rs-sdk, read from `sdk/types.ts`, `sdk/index.ts`, `server/gateway/gateway.ts` and `sdk/MARKET.md`.

**Bot**: A game account driven by code rather than a person. Identified by a username (max 12 characters, alphanumeric) with a `bot.env` and a `script.ts` under `bots/<username>/`.

**BotSDK**: The TypeScript client class (`sdk/index.ts`) that connects to the Gateway and exposes a Bot's state and low-level actions.

**BotActions**: The higher-level action layer (`sdk/actions.ts`, e.g. `chopTree`, `burnLogs`) built on BotSDK; each returns an `ActionResult`.

**BotWorldState**: The snapshot of everything a Bot can see (player, inventory, nearby NPCs/locs/players, dialog, shop, bank, trade, GE). Published by the game client once per update; carries `tick` and a monotonic `revision`.

**Tick**: One game-engine update. `BotWorldState.tick` is the tick a state was captured on.

**Gateway**: The WebSocket router (`server/gateway/gateway.ts`) between the game client's Bot connection and SDK clients.

**Controller**: An SDK client connected in `control` mode. It may send any action and pre-empts any controller the Bot already has.

**Observer**: An SDK client connected in `observe` mode (`SDKConnectionMode`). It may send chat and nothing else, and never pre-empts a Controller.

**Session status**: `active`, `stale` or `dead` (`SessionStatus`); how recently the Gateway received a state from a Bot.

**Runner**: The sandbox (`sdk/runner.ts`) that executes agent-supplied code against a Bot; raises `BotDisconnectedError` when the Bot drops.

**NPC / Loc / Ground item**: A non-player character (`NearbyNpc`), a static world object such as a tree or booth (`NearbyLoc`), and an item lying on the ground (`GroundItem`). Located by world coordinates `worldX`, `worldZ`.

**Dialog / Interface / Modal**: The three kinds of blocking UI a Bot must dismiss or answer (`DialogState`, `InterfaceState`, `modalOpen`).

**Prayer**: A toggleable combat buff (`PrayerName`, `PrayerState`).

**Grand Exchange (GE)**: The player market. Offers are placed in-game at a Grand Exchange table or teller in Varrock west bank; can be disabled with `GE_ENABLED=false`. When disabled, actions fail with reason `ge_unavailable`.

**Market**: The public, read-only view of the GE (`MarketClient`, `/market`, `/api/market/*`): items, quotes, history. Needs no Bot connection.

**Engine**: The vendored LostCity game server in `server/engine`.

**Webclient**: The vendored LostCity browser client in `server/webclient`, extended with the in-client Bot state collector.

**Vendored tree**: `server/{engine,content,webclient}`, local copies of upstream LostCity; local changes ("monkeypatches") are tracked in `server/PATCHES.md`.

**MCP server**: The Model Context Protocol server in `mcp/` exposing `execute_code`, `list_bots`, `disconnect_bot` and `get_market` to AI tools.
