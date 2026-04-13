# TrajCakeWars — Quick Setup Guide
## by TrajStudio

---

## Step 1: Installation

1. Place `TrajCakeWars.jar` in your server's `plugins/` folder.
2. Start the server once to generate config files.
3. Stop the server.

---

## Step 2: Prepare Your CakeWars Map

You need a CakeWars map built with:
- 2 islands (one per player) with a cake block on each
- Bridges or gaps between the islands
- A center area (optional, for diamond generators)
- Spots for shop NPCs on each island

### Option A: Your map is in a separate world
```
cp -r your_cakewars_world cw_templates/desert
```

### Option B: Your map is in the main world
```
cp -r world cw_templates/desert
```

### Option C: In-game
Stand in the world containing your map and run:
```
/cw savetemplate desert
```

The `cw_templates/` folder must be at the server root,
same level as `world/`, `plugins/`, etc.

---

## Step 3: Place Shop NPCs

In your CakeWars map (before saving the template), place
NPCs on each island using any NPC plugin:

### With Citizens:
```
/npc create §e§lItems Shop
/npc type VILLAGER
```
```
/npc create §a§lBlocks Shop
/npc type VILLAGER
```

### With a vanilla villager:
Rename it with a name tag containing "Items" or "Blocks".

### Recognized keywords:
- Items Shop → name contains: Items, Item, Combat, Weapons
- Blocks Shop → name contains: Blocks, Build, Construction
- (Configurable in config.yml)

Place 2 NPCs per island (Items + Blocks) = 4 NPCs total.
If you saved the template AFTER placing the NPCs,
they will be cloned automatically for every game.

---

## Step 4: Configure the Arena

Start the server and connect in-game.

### Create the arena:
```
/cw create desert
```

### Teleport into the template to configure:
```
/cw tp desert
```

### Set the 7 required points:
Go to each location and run the corresponding command.

```
/cw set desert spawn1       → Player 1 spawn
/cw set desert spawn2       → Player 2 spawn
/cw set desert cake1        → Player 1 cake block
/cw set desert cake2        → Player 2 cake block
/cw set desert gen1         → Iron generator, island 1
/cw set desert gen2         → Iron generator, island 2
/cw set desert lobby        → Spectator/waiting point
```

### Add diamond generators (optional):
```
/cw set desert diamond      → Repeat at each location
```

### Customize:
```
/cw setname desert §6§lBurning Desert
/cw seticon desert SAND
/cw settemplate desert desert
```

### Verify everything is configured:
```
/cw info desert             → Everything should be green ✓
```

### Return to lobby:
```
/cw back
```

---

## Step 5: Set the Lobby Return Point

Stand exactly where players should be teleported
after each game (in your main lobby) and run:

```
/cw setlobby
```

---

## Step 6: Enable and Save

```
/cw enable desert
/cw save
```

---

## Step 7: Lobby NPC (optional)

To let players access CakeWars from the lobby
by clicking an NPC:

### With Citizens:
```
/npc create §d§lCakeWars 1v1
/npc type VILLAGER
/npc command add -p cw
```

Players click → the /cw menu opens.

---

## Step 8: Test

Connect with 2 accounts (or a friend).

1. Both players click the lobby NPC or type `/cw`
2. Click "Play" in the menu
3. Matchmaking finds both players
4. A temporary world is cloned
5. Players are teleported, frozen 5s, then GO!
6. Game plays out
7. Winner receives rewards
8. Both players teleported to lobby
9. Temporary world deleted

---

## Adding a Second Map

1. Build a new map in a dedicated world
2. Place shop NPCs inside it
3. Save: `/cw savetemplate jungle`
4. Create arena: `/cw create jungle`
5. Configure: `/cw tp jungle` then `/cw set jungle spawn1` etc.
6. Enable: `/cw back` → `/cw enable jungle` → `/cw save`

Both maps will be available in matchmaking.

---

## Command Cheat Sheet

### Player:
  /cw                → Main menu
  /cw join           → Quick matchmaking
  /cw join <code>    → Join private session
  /cw private <map>  → Create private session
  /cw leave          → Leave queue/game

### Admin:
  /cw create <id>              → New arena
  /cw delete <id>              → Delete (type twice to confirm)
  /cw tp <arena>               → Teleport into template
  /cw back                     → Return to lobby
  /cw set <arena> <point>      → Set a configuration point
  /cw setname <arena> <name>   → Display name
  /cw seticon <arena> <mat>    → GUI icon material
  /cw settemplate <arena> <t>  → Link to template
  /cw savetemplate <name>      → Save current world as template
  /cw setlobby                 → Set lobby return point
  /cw enable <arena>           → Enable for matchmaking
  /cw save                     → Save to disk
  /cw info <arena>             → View configured points
  /cw list                     → List all arenas
  /cw admin                    → Admin GUI panel

---

## Troubleshooting

### Shop inventory is empty
Delete `plugins/TrajCakeWars/config.yml` and restart.
The old config is missing the shop sections.

### Arenas are DISABLED / ready=false
Missing configuration points. Run `/cw info <arena>`
to see which ones are missing (✗).

### Players fall into the void after the game
Run `/cw setlobby` at the correct position in your lobby.

### Temporary world is not created
Verify `cw_templates/<name>` exists at the server root
and the template is linked: `/cw settemplate <arena> <name>`

### Matchmaking can't find an arena
The arena must be `ready=true` AND `state=WAITING`.
Run `/cw enable <arena>` then `/cw save`.

---

TrajCakeWars v2.1.5 — by TrajStudio
