# Upsello Bot content updates

The desktop app fetches `team.json` every six hours and after start, and applies it to the
state its Agents read on their next turn. Nothing here is code: only prompts, capability
lists and skill texts.

- `version` must increase by one for a change to be picked up. Only a higher number is applied.
- `agents` is keyed by the shipped Agent's stable key: `sales`, `recovery`, `pdp`, `ads`, `social`, `expert`.
- `agents.<key>.instructions` replaces that Agent's prompt (20,000 characters at most).
- `agents.<key>.capabilities` replaces that Agent's capability list. Every name must already exist on the machine; unknown names are dropped.
- `skills[]` holds `{ name, description, content }`; a skill is written into the capability library and picked up by the Agents that name it.
- `rollbackTo` points the app at a kept older version, e.g. `{ "version": 8, "rollbackTo": 6 }`; versions up to 8 are then ignored.

A malformed file is refused whole, and the app keeps the last good version.
