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
for walking there or telling the mapper where you are. The **⋯** button above it switches to
Mudlet's 3D map (and its style and angle) and opens the layout editor. In a city, the **city**
button shows the city's own plan with you on it.

- **Exploring:** `zmap next` walks to the nearest exit you haven't tried and tries it. It
  opens closed doors on the way. If a guard or lock stops you, the next press tries elsewhere.
  `zmap next blocked` shows what stopped you, and `zmap next retry` tries those again.
- **New areas** are named after their outworld entrance. `zmap entrance` lists the entrances
  you haven't mapped yet, and `zmap entrance next` walks to the nearest.
- **Cities** (ZombieCity, Ravenkall, Acir's Spire, and any other once you type `map` there) are
  laid out on the game's own city map, which the map panel shows while you are on a street.
- **Terrain grids:** areas that show a terrain window around you (ZombieCity's booths as `booth X Y`, the Castle Area,
  Corn Fields, Savannah, Darkwater, Dwarf Valley, Eldoria and more) are drawn as a grid, and
  `goto savannah 5 3` walks to a square.
- **Rooms that change:** some areas, like ZombieCity's graveyard, describe a room differently
  on every visit. They are mapped by position. `zmap vary on` marks another such area.

More: `zui help map`.

## Walking and places

- `goto <place>` walks there from anywhere: by the map, across the outworld, through gates,
  doors and rides. `goto` lists your places, `goto add <name>` saves where you stand.
- **Inside an area**, left-click a room or exit name to walk there. Right-click it for route
  details. For example, click **ZombieCity** above your room to leave the Arena. The **inside**
  button switches to Mudlet's map, where a double-click on an exit arrow also walks through it.
- **Click the outworld map** (or a booth, Castle Area or field grid) in the panel: a left click
  walks to that square, a right click tells what is known of it, with a link to walk. A click
  on a city walks into it: ZombieCity to Central Square, other cities through their nearest gate.
  On a city's plan, a click on a place's name (Bank, Tinker, Adv.Guild...) walks into it, and a
  click elsewhere walks to the nearest street. When two buildings are as near a name, you pick
  which one it is once.
- Long walks run in brief mode and switch back to verbose when they are over (`goto brief off` walks verbose). `zstop` stops a walk.
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
- `zrun info <run>` sums a run up before you take it: its areas, how many moves a round takes,
  guards on the way, every monster with exp, fight time, weakest resist and dangers, a difficulty
  once you have considered enough of them, and your own finished rounds (time, exp, deaths).
- `zrun danger captain stun` notes what a monster does (stun, aggro, hunts, summons, poison,
  blind, party) at every stop it is a target. The tags go along when you share the run.
- `zrun optional captain` marks a monster you may leave standing, such as one that is too hard
  to fight solo.
- If a guard that stopped you before stands in the way to the next stop, the first press warns
  you. Guards that let only some races or guilds through are learned per character.
- `zrun end castle` (or any place) chooses where the round ends.
- To grow a run, load it and type `zrun extend`. Then play on as when recording: **numpad /**
  makes the room you're in a stop, and what you kill is added to it. `zrun extend off` ends it.
- Change a stop from anywhere by its number: `zrun 14 note rest here`, `zrun 14 kill orc 2`.
  `zrun add bank after 3` adds a stop at a place, room number or outworld square.
- `zrun name`, `zrun notes`, `zrun copy <new>` (a variant to change) and `zrun rename <new>`.
  `zrun undo` takes back the last change (this session).
- `zrun optimize` prefers stop orders that encounter fewer known blocking guards, then fewer
  moves. Put a guard on the required kill list at its room to clear the way later in the round.
  `zrun optimize apply` takes the suggested order.
- Arriving at a stop says what its monsters do (stuns, summons...). On the way to a stop you
  cleared not long ago, you're told when, and how long its monsters took to come back before.
- After a few rounds, `zrun info` names the stops that give the least exp for their time.

More: `zrun help`.

## Fighting

- **Loadouts** decide what the number pad casts: **\*** attacks, **shift+\*** opens a fight,
  **.** rebuffs, **ctrl+.** heals. Build one with `zload build`. Each reinc can have several.
  The builder suggests repeatable attacks, direct heals and compatible buffs for yourself.
  It also lists situational abilities for manual selection.
- **Worth the cast:** `zload vuln golden spear 1M party 300k` casts a vulnerability first on
  monsters worth 1M exp or more (300k in a party), and `zload open battlecry 2M` opens only on
  the big ones. **\*** takes one step a press: vulnerability, opener, then attacks. Smaller
  monsters skip the steps they aren't worth, and one never killed counts as big. The target
  chip shows the next step. `zrun vuln never` or `zrun open 500k` changes it for one run.
- **Chains:** the game's own `chain` command is followed. When it starts the next spell or skill
  by itself, the status bar names that one, and **\*** doesn't send an opener your chain
  already started. `zui setup` turns on `set nomore on` so your chain list can be read whole.
- **Spells and skills that go on:** cryokinesis and molecular agitation show in the status bar
  while they run, kiru and hurl axes until their last hit, and the chain after each is named.
  In a fight **\*** asks for a second press before casting over a running cryokinesis or
  molecular agitation, which any cast or skill would end.
- **Necromancers:** your undead, dark servant and spirit show in the PARTY card with their
  health, whether they fight or are chained, and a red "surgery" when they need it. `@m` in any
  command is your minion (`cast cure undead at @m`), `zload buff unholy courage at minions`
  keeps a buff on them, and **ctrl+\*** (`zcorpse`) uses a corpse best: bone armour, surgery,
  the spirit, else your corpse action. `zload minions on` sends them in with your opening.
- **Ogre mages with parallel process:** a spell and a skill going on at once each get a chip and
  end on their own. With `zload dual on`, **\*** sends whichever of the two isn't going.
- **Buffs on your party:** `zload buff iron will at tank` (or `at party`) keeps a buff up on
  others. The PARTY card tags each one and counts down its time, and `zbuffs` shows them all.
- **Spell shortcuts:** `iw` casts iron will, `psc goblin` psychic crush at the goblin, and about
  340 more. `zshort` lists those your reinc has.
- **Loot:** `zloot on` puts loot away and deals with corpses after your kills
  (`zloot into bag`, `zloot corpse tin`, or `zloot corpse tineat` to eat the can too). Your party's arrows go back to them.
- **Warnings:** `zwarn on` warns when the monster you fight starts a spell.
- **Magic words** in casts are shown as the spell's name (`zwords off` keeps the game's).

More: `zui help fighting` and `zui help targets`.

## Selling, chests and training

- `zsell` sells your loot at ZombieCity's shops and leaves you where it finishes; `zrun sell`
  does the same and walks you back to your run, stopping if anything blocks the way. `zsell preview` shows what
  would be sent first. You choose the sources (bag, disc, mule, servant), what to protect, and
  whether to deposit at a bank or booth. `zsell help` explains each.
- `zchest open`, `zchest stash` and `zchest get` handle every chest in a castle room at once.
- At a guild trainer, `list skills` and then `train all skills` (or `study all spells`) trains
  everything to the guild's maximum.

More: `zui help selling` and `zui help chests`.

## Cards and information

- **PARTY** follows joins, leaves and leaders as they happen, with each member's hp and sp.
- **BUFFS** groups your buffs and timers by type, a row each with its state on the right.
  Missing buffs from your loadout are listed first in red as down, and a line says when you
  have no greater or stun protection at all.
  **STATS** shows your score, and
  **SESSION** this session's exp, kills, deaths, the reboot and the time of day.
- The status bar shows when you are stunned, poisoned or scarred.
- `zui layout` rearranges the cards, map and chat around the main window. A card is only as
  tall as what it shows, and the map or chat takes the rest (`zui layout fit off` to turn it off).

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
