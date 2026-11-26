# ZombieUI

A complete interface for playing [ZombieMUD](http://www.zombiemud.org) in
[Mudlet](https://www.mudlet.org) 5.1 or newer:

- **A map that draws itself** as you walk, with ZombieCity, Ravenkall and the outworld's area
  entrances already on it.
- **Walking anywhere** with `goto`, across cities, the outworld, rides and castles.
- **Runs:** rounds of monsters to kill, walked a key press at a time.
- **Cards** for your party, buffs, stats and session, gauges for hp and sp, and chat in its own
  windows.
- **Loadouts** on the number pad: attack, rebuff and heal with one key.
- Selling trips, castle chests, loot, training, spell shortcuts and much more.

ZombieUI never plays for you: everything it sends is something you asked for, while you are at
the keyboard (see `help botting` in the game).

## Install

1. Install [Mudlet](https://www.mudlet.org) 5.1 or newer, and make a profile for ZombieMUD.
2. Download **[ZombieUI.mpackage](https://github.com/bogataj/zombieui-releases/releases/latest/download/ZombieUI.mpackage)**
   and drag it onto Mudlet (or Toolbox > Package Manager > Install).
3. Log in and type **`zui setup yes`**. This sets the game settings ZombieUI reads from. Among
   them, your prompt is replaced by a data line that ZombieUI reads and hides (`prompt old` in
   the game gives yours back). It also removes Mudlet's own generic mapper and base UI, since
   ZombieUI replaces them.

**Updating:** ZombieUI checks once a day for a new version and tells you when you log in.
`zui update` installs it, and you stay logged in. Your settings, map and notes are always kept.
If an update ever fails, it puts the previous version back.
All versions and what changed in each are on the
[releases page](https://github.com/bogataj/zombieui-releases/releases).

## First steps

| Type | To |
|---|---|
| `zui` | see every command by topic; click one for more |
| `zmap on` | start mapping the rooms you walk into |
| `goto cs` | walk to Central Square from anywhere |
| `zmap next` | explore: walk to the nearest unexplored exit and try it |
| `zload build` | set up what your number pad fights and buffs with |
| `zrun` | list your runs, or `zrun record <name>` to make one |

The number pad walks (**8** north, **2** south and so on, **5** looks, **-** up and **+** down).
A key you have set yourself in Mudlet stays yours.

## Map and exploring

ZombieMUD sends no map data, so ZombieUI reads every room from the game's text. With
`zmap on`, each room you step into from a known room is added to the map. Right-click the map
for walking there or telling the mapper where you are. The **3D** button above it switches to
Mudlet's 3D map.

- **Exploring:** `zmap next` walks to the nearest exit you haven't tried and tries it. It
  opens closed doors on the way. If a guard or lock stops you, the next press tries elsewhere.
  `zmap next blocked` shows what stopped you, and `zmap next retry` tries those again.
- **New areas** are named after their outworld entrance. `zmap entrance` lists the entrances
  you haven't mapped yet, and `zmap entrance next` walks to the nearest.
- **Cities** (ZombieCity, Ravenkall, Acir's Spire, and any other once you type `map` there) are
  laid out on the game's own city map, which the map panel shows while you are on a street.
- **Terrain grids:** areas that show a terrain window around you (the bazaar, the Castle Area,
  Corn Fields, Savannah, Darkwater, Dwarf Valley, Eldoria and more) are drawn as a grid, and
  `goto savannah 5 3` walks to a square.
- **Rooms that change:** some areas, like ZombieCity's graveyard, describe a room differently
  on every visit. They are mapped by position. `zmap vary on` marks another such area.

More: `zui help map`.

## Walking and places

- `goto <place>` walks there from anywhere: by the map, across the outworld, through gates,
  doors and rides. `goto` lists your places, `goto add <name>` saves where you stand.
- Long walks run in brief mode and finish with a `look`. `zstop` stops a walk.
- `goto home` and `goto castle` lead to your castle. `goto <player>` leads to a player's
  castle, and `goto <guild>` to a guild once you have saved it with `goto add <guild>`.
- `goto rides` lists the transport shops you have used. Routes take a ride when walking is far
  longer or impossible.
- `sgoto <npc>` follows your spyglass's directions to an NPC.
- `zwalk 3n2e` walks a path of your own while mapping.

More: `zui help walking`.

## Runs

A run is a round of stops, each with the monsters to kill there. ZombieUI plans the way to each
stop from wherever you are, but walking on and fighting stay with you.

- **numpad /** walks to the next stop (**shift**: back, **ctrl** or **alt**: skip without
  walking). On arrival the stop's monsters become your kill target (`kt` attacks it), and the
  RUN card counts kills and says when the stop is clear.
- `zrun record <name>`, then walk the round: press **numpad /** at each stop, or just kill
  something there. `zrun save` keeps it.
- `zrun info` lists every stop with what you know of its monsters. `zrun go 3` or
  `zrun go orc` walks to a stop.
- `zrun optional captain` marks a monster you may leave standing, such as one that is too hard
  to fight solo.
- If a guard that stopped you before stands in the way to the next stop, the first press warns
  you. Guards that let only some races or guilds through are learned per character.
- `zrun end castle` (or any place) chooses where the round ends.

More: `zrun help`.

## Fighting

- **Loadouts** decide what the number pad casts: **\*** attacks, **shift+\*** opens a fight,
  **.** rebuffs, **ctrl+.** heals. Build one with `zload build`. Each reinc can have several.
- **Buffs on your party:** `zload buff iron will at tank` (or `at party`) keeps a buff up on
  others. The PARTY card tags each one and counts down its time, and `zbuffs` shows them all.
- **Spell shortcuts:** `iw` casts iron will, `psc goblin` psychic crush at the goblin, and about
  340 more. `zshort` lists those your reinc has.
- **Loot:** `zloot on` puts loot away and deals with corpses after your kills
  (`zloot into bag`, `zloot corpse tin`). Your party's arrows go back to them.
- **Warnings:** `zwarn on` warns when the monster you fight starts a spell.
- **Magic words** in casts are shown as the spell's name (`zwords off` keeps the game's).

More: `zui help fighting` and `zui help targets`.

## Selling, chests and training

- `zsell` sells your loot at ZombieCity's shops and walks back. `zsell preview` shows what
  would be sent first. You choose the sources (bag, disc, mule, servant), what to protect, and
  whether to deposit at a bank or booth. `zsell help` explains each.
- `zchest open`, `zchest stash` and `zchest get` handle every chest in a castle room at once.
- At a guild trainer, `list skills` and then `train all skills` (or `study all spells`) trains
  everything to the guild's maximum.

More: `zui help selling` and `zui help chests`.

## Cards and information

- **PARTY** follows joins, leaves and leaders as they happen, with each member's hp and sp.
- **EFFECTS** shows your buffs and when they run out. **STATS** shows your score, and
  **SESSION** this session's exp, kills, deaths, the reboot and the time of day.
- The status bar shows when you are stunned, poisoned or scarred.
- `zui layout` rearranges the cards, map and chat around the main window.

More: `zui help you`.

## Exploring helpers

- `xa <thing>` tries every way of examining something (look, search, push, pull, turn...).
- `sea` searches the room, and `open doors` opens doors in all directions.
- `znotice` lists optional notices (arena, puzzles, gates, timers), and `zhl add <text>`
  highlights lines.

More: `zui help exploring`.

## When you die

ZombieUI holds still while you are a ghost: it sends nothing, and the map keeps your place.
`goto` still walks you, over water too. You're seen as alive again at your first prompt
(`zui alive` if it ever misses it).

## Sharing

`zshare export map` (or `area here`, `run <file>`, `npcs`) writes a file you can give other
players. `zshare import <file>` shows what it would add, `zshare apply` adds it, and
`zshare undo` takes it back. Only game facts are shared: never your notes or exp.

More: `zui help sharing`.

## Your data

Everything that is yours lives in `<profile>/zui_data/`: settings, map, places, runs,
loadouts, NPC knowledge and your own `user.lua`. Updates never touch it. The map that comes
with ZombieUI is added to yours, never replacing it.

## Help

Type `zui` for every command by topic, and `zui help <topic or command>` for more
(`zui help goto`). `zmap help`, `zrun help` and `zsell help` cover their own commands.
ZombieMUD has its own `map` command, so the mapper's commands are `zmap`.
