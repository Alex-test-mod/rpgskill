# RPGSkills — Server Setup Guide

Everything a server owner needs, in the order you need it.

---

## 1. Requirements

| | |
|---|---|
| Server | Paper 1.21.x, or a fork such as Purpur |
| Java | 21 or newer |
| RAM | No special requirement beyond your normal server budget |

Storage drivers (HikariCP, SQLite, MySQL) are downloaded automatically by Paper's library loader on
first start. Nothing to install, nothing to shade.

### Optional plugins

| Plugin | What it unlocks | Without it |
|---|---|---|
| **Vault** + an economy plugin (EssentialsX, CMI…) | Shops, the savings bank, guild banks, money in trades | Those features disable themselves; everything else runs |
| **PlaceholderAPI** | Placeholders for scoreboards, chat and holograms | Placeholders unavailable |
| **LuckPerms** | Per-rank experience bonuses | Falls back to permission nodes |

Install Vault first if you want any economy features. RPGSkills never handles currency itself — it
asks Vault, so whichever economy plugin you already use stays in charge of the wallet.

---

## 2. Installation

1. Stop the server.
2. Drop `RPGSkills-1.0.0.jar` into `plugins/`. **Make sure there is only one copy** — a second,
   older jar is the most common cause of "my changes did nothing".
3. Start the server. Sixteen configuration files are generated in `plugins/RPGSkills/`.
4. Check the console for `Loaded N class definitions`, `Loaded N skill definitions` and similar. If
   a file has a mistake in it, the affected entry is named in the log and skipped rather than
   crashing the server.

### Storage

SQLite is the default and needs no setup — a `rpgskills.db` file appears in the plugin folder.

For MySQL, edit `database.yml`:

```yaml
type: mysql
mysql:
  host: 127.0.0.1
  port: 3306
  database: rpgskills
  username: rpg
  password: 'your-password'
  pool-size: 10
```

Schema migrations run automatically on start and are versioned, so upgrading the plugin later never
requires touching the database by hand.

---

## 3. Permissions

Most player commands default to `true`. Administrative ones default to `op`.

| Node | Grants |
|---|---|
| `rpgskills.command.use` | The base `/rpg` command and help |
| `rpgskills.command.stats` · `.attributes` · `.profile` | Character sheet |
| `rpgskills.command.class` · `.skills` · `.bind` · `.cast` | Class and skills |
| `rpgskills.command.item` | Item tools and the upgrade forge |
| `rpgskills.command.dungeon` · `.quest` · `.shop` · `.bank` | Content and economy |
| `rpgskills.command.party` · `.trade` · `.guild` · `.pet` | Social and pets |
| `rpgskills.admin` | Everything below |
| `rpgskills.command.boss` | Spawning and clearing bosses |
| `rpgskills.command.item.admin` | `/rpg item give` |
| `rpgskills.command.class.admin` · `.skills.admin` | Forcing classes and granting skills |
| `rpgskills.command.quest.admin` · `.dungeon.admin` · `.bank.admin` · `.pet.admin` | Admin subcommands |
| `rpgskills.command.reload` · `.save` | Administration |

**Experience bonus by rank** — grant `rpgskills.xp.bonus.<percent>`, for example
`rpgskills.xp.bonus.25` for +25%. The highest node a player holds wins. With LuckPerms installed you
can use a meta key instead (see `config.yml`).

---

## 4. What works immediately, and what needs building

Classes, skills, stats, combat, items, the forge, bosses, quests, shops, the bank, parties, trading,
guilds and pets all work the moment the server starts.

**Dungeons need you to build the maps.** This is the one system that cannot ship ready-made, because
it depends on your world.

### Setting up a dungeon

`dungeons.yml` ships with three dungeons pointing at a world named `dungeons`. Either build there, or
change the coordinates to match what you have.

```yaml
sunken-crypt:
  arenas:
    alpha:
      world: dungeons
      origin:   { x: 0.0,  y: 64.0, z: 0.0 }
      entrance: { x: 0.5,  y: 65.0, z: 0.5, yaw: 0.0, pitch: 0.0 }
      bounds:
        corner-1: { x: -60.0, y: 40.0, z: -60.0 }
        corner-2: { x:  60.0, y: 100.0, z: 60.0 }
```

- **origin** — the reference point. Every stage's spawn is an *offset* from this.
- **entrance** — where players arrive.
- **bounds** — the box players must stay inside. Stepping out teleports them back to the last
  checkpoint.

Stage spawns are offsets, so once you have built the map you can copy it elsewhere and add a second
arena with a different origin — and two parties can then run the same dungeon at the same time. The
number of arenas you build is the number of concurrent runs.

```yaml
  stages:
    approach:
      type: wave
      spawn: { x: 0.0, y: 1.0, z: 20.0 }    # 20 blocks north of origin
      mobs: ["ZOMBIE:8", "SKELETON:4"]
      checkpoint: true
    warden:
      type: boss
      boss: necro-lord
      spawn: { x: 0.0, y: 1.0, z: 70.0 }
```

Three stage types: `wave` (kill everything), `boss` (kill the named boss), `interlude` (a timed
pause). Until an arena exists, `/rpg dungeon` reports that no instance is free.

---

## 5. Tuning your server

Every file is documented inline. The ones you are most likely to touch first:

| File | Change this to… |
|---|---|
| `config.yml` | Level curve, XP rates, starting points, autosave interval |
| `stats.yml` | What each stat does and its caps |
| `classes.yml` | Class stat growth, level requirements, starter kits |
| `skills.yml` | Skill damage, cooldowns, costs, effects |
| `damage.yml` | The armour formula, crit behaviour, combos |
| `items.yml` | Rarity odds, item templates, upgrade chances and penalties |
| `bosses.yml` | Boss health, phases, loot |
| `dungeons.yml` | Arenas, stages, difficulty scaling, rewards |
| `quests.yml` | Quest chains, objectives, rewards |
| `economy.yml` | Shop stock and prices, bank interest |
| `social.yml` | Party size, XP sharing, trade rules |
| `guilds.yml` | Ranks, permissions, upgrades |
| `pets.yml` | Pet stats, abilities, evolution |
| `messages.yml` | **All** player-facing text, in MiniMessage format |

Numbers are formulas, not constants. `"20 - level * 2"` is a valid cooldown. Variables available
include `level`, `player_level` and every stat id.

Run `/rpg reload` after editing. It re-reads every file without a restart.

### Balance levers worth knowing

- **XP rate** — `config.yml` → `experience.multiplier`
- **Money sinks** — a shop's `sell-multiplier` is the single biggest lever on inflation. The
  blacksmith ships at `0.35`, meaning gear sells back for 35% of its price.
- **Dungeon difficulty** — Normal, Hard, Heroic and Mythic scale enemy health, damage, rewards,
  lives *and* the time limit together.
- **Party XP** — `social.yml` → `party.experience.earner-share` (default `0.75`). The remainder is
  **split** among nearby members, not duplicated, so a five-player group is not five times faster
  than soloing.

---

## 6. Content reference

**Classes** (with level requirement): warrior (1), mage (1), knight (5), ranger (8), assassin (10),
priest (10), archer (12), necromancer (15), berserker (18), paladin (20), summoner (25)

**Bosses**: `necro-lord` (lv 25) · `ember-tyrant` (lv 40) · `void-sovereign` (lv 70)

**Dungeons**: `sunken-crypt` (lv 15) · `ember-foundry` (lv 35) · `void-cathedral` (lv 60)

**Shops**: `general` · `blacksmith` · `runes`

**Pets**: `wolf-pup` → `dire-wolf` · `cave-bat` · `arcane-wisp` · `ember-sprite` · `iron-sentinel` ·
`void-drake`

**Guild ranks**: officer · veteran · member · recruit (leader is built in)

---

## 7. Admin commands

```
/rpg boss spawn <boss>        spawn a boss where you stand
/rpg boss active              list live fights with phase and health
/rpg boss threat              show the nearest boss's threat table
/rpg boss clear               despawn every boss

/rpg item give <player> <item> [amount] [rarity]
/rpg class set <player> <class>
/rpg skills give <player> <skill> <level>
/rpg quest give <player> <quest>
/rpg pet give <player> <pet>
/rpg bank set <player> <amount>
/rpg xp give <player> <amount>
/rpg level <player> <level>

/rpg dungeon close            end every running dungeon
/rpg reload                   reload all configuration
/rpg save                     force-save all loaded data
```

---

## 8. Troubleshooting

**"Changes to a config did nothing"** — check `plugins/` for a second RPGSkills jar.

**Economy commands say no economy is available** — Vault is missing, or Vault is installed with no
economy plugin behind it.

**`/rpg dungeon` says no instance is free** — the arena world is not loaded, or the arena has not
been built. See section 4.

**A skill, item or boss is missing after editing a config** — the console names the entry and the
reason at startup. Bad entries are skipped so one typo cannot take the server down.

**Placeholders show as raw text** — PlaceholderAPI is not installed, or the expansion did not
register. RPGSkills logs `PlaceholderAPI not found` on start when it is absent.
