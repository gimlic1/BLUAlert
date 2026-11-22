# FFXI Addon — BLUAlert

> [!NOTE]
> **Quick Reference**
> - **Path:** `C:\Windower\addons\BLUAlert\`
> - **Author / Version:** Kainsin / v1.0.0.0
> - **Commands:** None
> - **Load Status:** On-Demand (unloaded)
> - **Origin:** Official Windower

Alerts the player with a chat message and sound effect whenever a nearby monster readies a learnable Blue Magic spell that the player has not yet learned.

## What the Code Does
- At load time, builds a `spell_id_map` dictionary mapping `res.monster_abilities` and `res.weapon_skills` IDs to `res.spells:type('BlueMagic')` IDs by matching English names (handling 7 abbreviated/divergent names in `blu_different_names`, e.g., `"Everyone's Grudge"` -> `"Evryone. Grudge"`, `"Quadratic Continuum"` -> `"Quad. Continuum"`).
- Listens to `action` events for `category == 7` (monster/entity readies an ability), extracts `v2['param']` from `action['targets']`, looks up `spell_id_map[action_id]`, and checks `not windower.ffxi.get_spells()[spell_id]`.
- If unlearned, prints `"Unknown Blue Magic Used!"` to chat (color `123`) and plays `sounds/UnknownBlueMagicUsed.wav`.

## Commands & Usage
- No commands; runs passively once loaded (`//lua load blualert`).

## Events, Packets & Technical Hooks
- **Windower Events:** `action` (`category == 7`)
- **Packets:** None — uses Windower `action` event and `windower.ffxi.get_spells()`.
- **Dependencies / Libraries:** `sets`, `resources`, `chat`

## Local Settings & Customizations
- No `data/settings.xml`. Ships with `sounds\UnknownBlueMagicUsed.wav`.

## Related Notes
- `FFXI Addon — bluguide`
- `FFXI Windower Overview`
- `FFXI Windower Addons Catalog`
