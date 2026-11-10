# ZombieUI

A Mudlet 5.1 UI for ZombieMUD. ZombieMUD sends no GMCP, so the mapper reads rooms from plain
game text and shows them on Mudlet's map: the flat 2D map at first, or Mudlet 5.1's 3D map
with the **3D** button over the map (the **View** button, or `zmap view`, picks its angle, kept
for next time).

## Installing

1. Install [Mudlet](https://www.mudlet.org) 5.1 or newer.
2. Make a profile for ZombieMUD and open it.
3. Download **[ZombieUI.mpackage](https://github.com/bogataj/zombieui-releases/releases/latest/download/ZombieUI.mpackage)**
   (the newest release; earlier ones and what changed are on the
   [releases page](https://github.com/bogataj/zombieui-releases/releases)) and drag it onto
   Mudlet (or Toolbox > Package Manager > Install). To be told of new versions, click
   **Watch > Custom > Releases** on the releases repository.
4. Log in. ZombieUI welcomes you and lists the game settings it reads from; type
   `zui setup yes` to set them. This replaces your game prompt with a data line ZombieUI reads
   and hides; `prompt old` in the game gives you your own prompt back. It also removes Mudlet's
   own generic mapper, if you have it (ZombieUI does the mapping), and Mudlet's base UI steps
   aside for ZombieUI's (`baseui show` brings it back).

You start with a map of ZombieCity and Ravenkall, and the outworld with its area entrances marked
(most of them named): the rest of the map is yours to make as you go in. It is added to any map
you have and never replaces it.

## Updating

Once a day ZombieUI asks the releases page whether there is a newer version, and if there is it
tells you when you log in. `zui update` downloads it and installs it in place: your settings,
map and notes are kept, and you stay logged in. Nothing is installed until you type it.
`zui update check` looks right away, and `zui update off` (or `on`) stops or starts the daily
look. You can also update by hand: install the new `.mpackage` the way you installed the first
one. If a new version ever fails to start, drag an earlier one from the
[releases page](https://github.com/bogataj/zombieui-releases/releases) onto Mudlet.

## Layout

Blocks (map, room, chat, and the party, effects, stats and session cards) sit in regions around
the main console: columns left and right, and bands above and below. By default
chat runs above the main console, and the right column has the map, room and party, then effects
beside session, and stats beside the run you have loaded. The column width and text size follow
the window size. `zui layout` shows the placement and changes it; your choices are kept in `zui_data/`.
`zui layout undo` takes back the last change made with its commands, a reset or a preset too.

Right-click the map and open the **ZombieUI** menu for walk here, I am here, move to the
mapping area, and terrain for the 3D diorama ground.

## How the mapper reads ZombieMUD

| Room kind | How it looks in game | What the mapper does |
|---|---|---|
| indoor | description, then `There are N obvious exits: ...` | mapped |
| city | 15-column street map (you are `X`) beside the description | mapped; the map is shown in the room card |
| wild | terrain map (you are `@`) beside the description | not mapped; the terrain map is shown in the room card |
| grid | a field of squares (the bazaar; you are `*`) | mapped square by square |

Each room is keyed by kind + exits + description. Walking through an exit the map already
knows is trusted first, so rooms with the same description still work if you walk into them.
With mapping on (`zmap on`), a room is only added for a step from a room the map knows, or for a
step in from a known outworld square (a new area). When the map doesn't know where you are,
nothing is added until it finds you again; `zmap start <area>` begins a new area by hand.

The game doesn't name an area at its entrance on the outworld (it is only "the entrance to
something special"), so a new area is named after its first room until you rename it (`zmap
rename <name>`). `zmap entrance <name>`, standing on the entrance square, names it for good: the
area behind it takes the name now, or when it is first mapped, and the name travels with your
outworld marks when you share the map. `zmap entrance 131,70 Uhruul` names one from anywhere (the
numbers the outworld header shows). ZombieUI comes with the outworld's area entrances marked `?`,
most of them named. `zmap entrance` lists the nearest ones whose area isn't on your map yet (click
one to walk there), `zmap entrance all` every one, and `zmap entrance next` walks to the nearest.
The entrances and their names come from the players' own
[outworld map](https://zommap.github.io/) and the r/zombiemud wiki, checked against the routes
the wiki gives.

A hidden way out of a room (`press opal`, `pull lever`) isn't taken for an exit when you just type
it: a typed `recall` or teleport would be mapped as one. Use `zmap via press opal` instead. It
sends the command, links the room it leads to through that command, and routes then use it like
any other exit. A room entered by a command (`hut`, `enter`) is drawn a level up on the same
square.

A city can have more rooms on a curving street than there are squares between its ends
(Ravenkall). When a stretch of new rooms reaches a room the map already has and doesn't fit, it is
laid out again between its two ends, bowing out to the side it was walked on. `zmap fit <from>
<to>` does the same for rooms already mapped. Look-alike streets are told apart by their side
maps, which each city room keeps.

## Runs

A run is a round of stops: map rooms or outworld squares, each with what to kill there and how
many, and notes and warnings. The way to each stop is planned from wherever you are, as `goto`
plans it, so you can start a run anywhere and skip stops. `zrun` lists your runs (click one to
load it), and `zrun help` shows the commands.

- **numpad /** walks to the next stop, **shift+numpad /** walks back, and **ctrl** / **alt+numpad /**
  skip a stop forward or back without walking. On arriving, the stop's NPCs become your kill
  target (`@t`, `kt`), and the RUN card counts the kills.
- `zrun info` lists every stop: where, what to kill, and what your NPC knowledge says about it
  (exp, aggro, least resist, KYA). `zrun here` finds the stop you're at after a death or a
  detour, and `zrun go 3` walks to stop 3.
- `zrun record <name>` writes a run down as you play: walk to each stop and press **numpad /**
  there, or kill something and the room becomes a stop with that NPC. `zrun kill orc 2`,
  `zrun note ...` and `zrun warn ...` change the stop you're at; `zrun add`, `zrun del` and
  `zrun move` change the round. `zrun save` keeps it.

Runs are files in `<profile>/zui_data/runs/`. If a move is refused, or you end up somewhere else
than the way expected, ZombieUI tells you and the run stays where it was. Runs never move or
fight for you (`help botting`).

## Places

`goto <place>` walks there from wherever you are. `goto` alone lists your places (click one to go).

- A place is a map room or an outworld square, with any commands to do on arriving
  (`goto then feda (enter)(portal)9w7n`). `goto add <name>` makes the room or square you're on a
  place, and `goto del <name>` removes one. A new player starts with `cs`, the central square.
- The way is worked out each time. It goes by the map to a city gate, across the outworld by the
  shortest walk that avoids mountains, walls and water deeper than wading, and in through a gate
  when the place is a mapped room. `goto <place> w` may cross deep water. Gates learn their
  outworld squares as you walk through them.
- `(goto castle)` in a place's commands or a run's path is routed from wherever the path has
  got to.
- `sgoto <npc>` asks your spyglass (`find <npc>`) and walks the directions it gives. Numpad `/`
  with no run loaded does that for your kill target.

They are kept in `<profile>/zui_data/places.json`.

### Rides and guilds

- **Rides** are the transport shops ("buy transport to ravenkall"), the walking player's way
  between landmasses: they aren't joined without deep water. A ride is learned the first time
  you buy it; `goto rides` lists them.
  - **A ride that lands in a room** (an area like Ravenkall) always lands there, and becomes an
    exit on the map.
  - **A ride that lands on the outworld** lands on a random square. `goto` walks to the shop,
    rides, and plans the rest from where you land.
  - Routes take a ride only when walking can't get there or is much longer; a ride counts like
    40 moves.
- **Guilds:** `goto <guild>` walks to a guild (`goto psionicist`, `goto psionicists`). Most
  guild halls aren't known to ZombieUI in advance, so each is a place you add once at its hall
  with `goto add psionicist`. `goto guilds` shows which are known. Short names (psi, sorc,
  navi, necro) work too.

### Castles

- `goto castle` walks to the outworld castle of the character you're playing. `goto home` walks
  to their castle in the castle area. `goto <player>` walks to that player's outworld castle,
  or to their home if that's all that is known. `goto castles` lists the castle owners known.
- Owners come from `finger <player>` ("The Lord of the outworld Castle 'Astral forest'.").
  Castle squares come from passing them on the outworld ("The Castle of Astral forest").
  Both are kept up to date as you play.
- Home is learned by walking into your castle's first room. The game shows its owner (and
  co-rulers) "[ The Castle room: 0 ]" there, so ZombieUI knows the castle is yours. `goto add
  home` sets it by hand. Every character has its own home.
- Famous castles get a name of their own with `goto add`.

## Loadouts

A loadout is how your reinc fights: what opens a fight, what you fight with, which buffs you keep
up and what you heal with. The number pad sends it (below). ZombieUI never makes one for you:
when a reinc has none, it says so once its spells and skills are read, with what it would
suggest from what you know.

- `zload build` walks you through it a step at a time: opener, follow-up, buffs, heal. Each step
  lists the spells and skills you know for it, best trained first, with ZombieUI's suggestions
  starred. Click to pick or drop one. Nothing is saved until the last step.
- `zload suggested` takes the suggestions as they are. `zload` shows the loadout and how to
  change one thing at a time (`zload buff iron will`, `zload heal cure serious wounds`...).
- A reinc can have several: `zload build party` makes another, `zload use main` switches which
  one the keys use, and `zload copy`/`zload delete` copy or throw one away.
- Presets of your own in `user.lua` (`zui.user.preset`) are starting points for `zload from`.

## When you die

A ghost has no prompt and no colours, and its `look` is brief, so ZombieUI holds still until
you are back: it sends nothing for you, the map keeps your place and makes no rooms, the
loadout keys do nothing, and the gauges and cards say you are dead instead of showing what was
true before. `goto` walks a ghost on foot, over water too (ghosts walk on it), so every place
is a walk away: to Hubertus in Uhruul or Emlar in Ravenkall,
or ask whether a player who knows the spell can resurrect you (praying at the church altar can
cost a level). ZombieUI sees you alive again at your first prompt (if it ever misses it, `zui
alive` tells it). The SESSION card counts your deaths, who killed you and the exp it cost.

## Keys

The number pad walks: **7 8 9 / 4 6 / 1 2 3** are nw, n, ne, w, e, sw, s and se, **5** is
`look`, **-** goes up and **+** down, and **0** is `score`. **\*** attacks with your loadout,
**shift+\*** stops your cast and opens with your loadout's opener, **.** rebuffs, **ctrl+.**
heals (`hl <player>` heals them), and **/** walks runs (above). A key you have set yourself in
Mudlet's Keys stays yours: ZombieUI leaves it alone.

## Words ZombieUI takes over, and what it hides

- **Shortcut words** for spells and skills (`iw` casts iron will, `psc goblin` psychic crush at
  the goblin): about 340 come with ZombieUI, and each is on only while your reinc has its spell
  or skill. Alone, a word aims an attack at your kill target and a protection or heal at you.
  `zshort` lists the ones on for you, `zshort all <text>` every one, and `zshort del <word>`
  switches one off (`zshort add <word> <spell>` makes your own).
- **Its own short commands:** `kk`, `ki`, `rb` (and `b`), `hl` (the keys above), `kt` (kill your
  target), and `@t` anywhere in a command, which becomes your target's word. `kill <word>` goes
  to the game as you typed it, and teaches ZombieUI the word for that NPC.
- **Hidden lines:** the data prompt shows as a plain `>`, the game's `hp: sp:` lines are left out
  (the gauges show them; `zui gag off` brings them back), the game's `*** KEEPALIVE MESSAGE ***`
  (`set keepalive`) is hidden (`zui gag keepalive off` shows it again), and what ZombieUI reads on
  its own at a login or a cast's end (score, spells, skills, buffs, party) doesn't show.
- **Elf tales:** a tale's lines ("Gam says 'In the beginning there was nothing.'") show in the main
  window as the game sends them but stay out of the Says and All feeds. ZombieUI knows each tale by
  its words: when one ends it says which it was and whether you have now heard all of it. The
  SESSION card's Tales row counts this season's five heard in full since the reboot (your own
  recitals too); click it, or type `zui tales` (`zui tales all` for every season). Tales you heard
  before ZombieUI counted them: `zui tales heard factions`, or `zui tales heard all` for the season's
  five (`zui tales unheard` takes it back).
- **Your bless and profane sacrament:** a cleric's or paladin's bless, and a death knight's profane
  sacrament for the undead, each last until the reboot (or until you quit), and you get one of each
  every reboot. ZombieUI notes who gave it and what it gave ("You feel wiser."): the EFFECTS card
  shows `Bless WIS` or `Sacrament CON`, and the SESSION card's Bless and Sacrament rows say whether
  you have this reboot's (red when you quit or died and it's gone). `zui bless` tells more. One from
  before ZombieUI saw it: `zui bless wis` (any gift: `str`, `AC`, `fire`...) or `zui bless sacrament
  con`; `zui bless none` (or `zui bless sacrament none`) takes it back.
- **The time of day** sits on the right of the vitals bar. Until the game has confirmed the clock
  it reads `sync`: a click walks you to ZombieCity's clocktower to look at it.

## Your data

Your settings, loadouts, map, NPC records, places, runs, chat history and `user.lua` live in
`<profile>/zui_data/`, outside the package, so installing a new version never touches them. The
starter map in the package is added to the map you have: rooms you have already stay as they
are, and a new version's new rooms come in on its first start (`zshare undo` takes them out).

## Sharing

`zshare` passes what you have gathered to other players, as a file you send them however you
like (ZombieUI never sends it through the game).

- `zshare export area here` writes the area you're in (a city with its buildings) to
  `<profile>/zui_data/share/`. `zshare export map` writes all your rooms, with your places,
  rides, castles and outworld marks. `zshare export run <file>` writes a run with the rooms on
  its way, and `zshare export npcs` what you know of NPCs (`npcs orc`, `npcs area <name>`, or
  `zshare export area here npcs` with the area). Add `as <name>` to name the file.
- Shared NPC knowledge is what the game told you: KYA, consider, aggro, the word it answers to,
  where it was seen, which exits it guards. Your notes and your own least-resisted type are
  never in a file, and neither are exp and fight times: they depend on your character.
- `zshare import <file>` (a file in your share folder) shows what it would do and changes
  nothing yet. Room numbers differ from player to player, so rooms are recognised by their text,
  exits and side map, by their outworld square, and by the exits between them. A room that
  could be one of several of yours, or whose exits disagree with your map, is left out with
  everything only reached through it; `zshare same <file room> <your room>` says which it is.
  `zshare show` marks the rooms on the map.
- Places, runs and rides are moved onto your rooms. A place of yours with the same name stays
  yours (`zshare take place <name> as <new>` takes theirs). The preview lists every command a
  place sends on arriving, and every command an exit or a ride of the file sends on the way
  through (`press opal`, `buy transport to ravenkall`): read them before you take someone's
  file. Those of exits and rides go to the game as they are, never through your aliases.
- `zshare apply` does it, `zshare undo` takes the last import back, and `zshare list` shows
  your imports. A file from someone you imported from before is recognised at once; rooms they
  see differently now are listed, and `zshare theirs` takes their text.

## Commands

Type `zui` in Mudlet: the commands by topic (map, walking and places, targets, fighting, runs,
sharing, you, built-in lists, ZombieUI), a line each; click one, or `zui help <topic or command>` (`zui help
goto`), for its commands. `zmap` shows what the map knows of where you are and the map commands
you use most; `zmap help` lists them all. ZombieMUD has its own `map` command, so the mapper uses
`zmap`.

What ZombieUI comes with can be looked up: `zui lookup <spell or skill>` (`zui lookup force
shield`, `zui lookup fs`) shows its type, the tag its effect shows with on the cards, its shortcut
words, the guilds that teach it and from what level, and whether you have it. `zfx tags <text>`
and `zshort all <text>` search the tags and every shortcut word; `zui help lists` has the rest.
