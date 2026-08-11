# RPGSkills — Player Guide

How to actually play. Everything lives under `/rpg`, and every command tab-completes.

---

## Your first ten minutes

```
/rpg class            pick a class
/rpg stats            see where you stand
/rpg quest            take your first quest
```

Kill things. You gain experience, levels, attribute points and skill points.

Your first quest, **First Steps**, asks for 10 kills of anything. It chains into a five-part story
line that ends at the Void Sovereign.

---

## Character

### Stats

Six primary attributes you spend points on:

| Attribute | Drives |
|---|---|
| **Strength** | Physical damage |
| **Dexterity** | Attack speed, crit chance, movement |
| **Vitality** | Health and health regeneration |
| **Intelligence** | Magic damage, mana, mana regeneration |
| **Luck** | Rare drops, crit chance, loot quality |
| **Defense** | Armour and damage reduction |

Those feed 32 derived stats — crit damage, life steal, armour penetration, cooldown reduction,
thorns, and a resistance for each of the six damage elements.

```
/rpg stats            full breakdown
/rpg attributes       spend your points
/rpg profile          summary
```

Points are permanent, so plan around your class. A Mage putting points into Strength is wasting them.

### Classes

Pick one with `/rpg class`. Some unlock at higher levels.

| Class | Level | Plays like |
|---|---|---|
| **Warrior** | 1 | Melee damage, area attacks, self-buffs |
| **Mage** | 1 | Ranged elemental damage and control |
| **Knight** | 5 | Tank — holds boss attention, absorbs damage |
| **Ranger** | 8 | Mobile bow damage with traps |
| **Assassin** | 10 | Burst damage, mobility, evasion |
| **Priest** | 10 | Healing and party support |
| **Archer** | 12 | Pure ranged damage |
| **Necromancer** | 15 | Summons, drains, damage over time |
| **Berserker** | 18 | Damage that scales as your health drops |
| **Paladin** | 20 | Melee and support hybrid |
| **Summoner** | 25 | Fights through summoned creatures |

Your class decides your stat growth, what gear you can equip, and which skill tree you get.

```
/rpg class list           everything available
/rpg class info <id>      details before committing
```

Changing class later costs money, and the first few changes may be free depending on server config.

---

## Skills

47 skills across seven trees. Your class determines which you can learn.

```
/rpg skills               open your tree
/rpg bind <skill> <1-9>   bind to a hotbar slot
/rpg cast <skill>         cast directly
```

**To use a skill**: bind it to a hotbar slot, hold that slot, and swap hands (default **F**) to cast.

Skills cost mana, stamina or energy and have cooldowns. Both shrink as you rank the skill up.
Cooldown reduction from gear applies on top.

### Trees

- **warrior** — battle-cry, bloodthirst, challenging-roar, cleave, earth-slam, iron-skin, whirlwind
- **mage** — arcane-mastery, blink, chain-lightning, fireball, frost-nova, magic-beam, mana-flow, meteor
- **assassin** — blood-slash, dash, deadly-precision, evasion, poison-nova, shadow-step
- **archer** — arrow-storm, eagle-eye, hunters-mark, piercing-shot
- **necromancer** — dark-pact, life-drain, summon-golem, summon-skeleton, summon-wolf
- **priest** — blessing, divine-shield, faith, healing-wave, phoenix-rebirth
- **general** — available to everyone: alchemy, arcane-well, blacksmithing, cooking, enchanting,
  fortune, mining-expertise, scholar, second-wind, swiftness, toughness, vigor

**Tanks, read this**: `challenging-roar` forces every nearby boss to attack you. Bosses track threat
from damage *and healing*, so without a taunt the healer gets killed.

---

## Items

Ten rarity tiers, from Common to Unique. Higher rarity means stronger rolled stats, more sockets and
a higher upgrade ceiling.

```
/rpg item inspect         examine what you are holding
/rpg item accessories     18 accessory slots
```

### The upgrade forge

```
/rpg item upgrade
```

Upgrades the item in your main hand. Each level costs money and can fail. Depending on the item and
your server's settings, failure may do nothing, drop a level, or destroy the item — the menu tells
you which before you commit. A **Scroll of Blessing** improves your odds.

### Sockets and runes

```
/rpg item socket insert     main hand = item, off hand = rune
/rpg item socket remove <n>
```

Runes add permanent stats. Buy them from the `runes` merchant or take them from bosses.

---

## Combat

Nine damage types: physical, magic, true, fire, ice, lightning, poison, holy and shadow. Each has a
matching resistance, so gear choice matters against specific content — bring fire resistance to the
Ember Foundry.

Chaining hits builds a **combo** that increases your damage. Taking a hit resets it.

Damage numbers float above whatever you hit.

---

## Quests

```
/rpg quest              open the journal
/rpg quest track <id>   see objectives in chat
```

Objectives within a quest progress in parallel — do them in any order. When all are complete, the
quest is ready to **claim**; rewards are paid on claim, so a full inventory at the wrong moment never
costs you anything.

- **Main** — a five-part chain: First Steps → Find Your Calling → The Proving Ground → The Tyrant's
  Forge → What Waits Beyond
- **Side** — A Smith's Request, Trial by Fire (magic classes only)
- **Daily** — reset 00:00 UTC, accepted automatically
- **Weekly** — reset Monday 00:00 UTC
- **Repeatable** — the bounty board, as often as you like

---

## Dungeons

```
/rpg dungeon            browse
/rpg dungeon queue <id> join matchmaking
/rpg dungeon top <id>   fastest clears
```

| Dungeon | Level | Party | Difficulties |
|---|---|---|---|
| **The Sunken Crypt** | 15 | 1–5 | Normal, Hard, Heroic |
| **The Ember Foundry** | 35 | 2–5 | + Mythic |
| **The Void Cathedral** | 60 | 3–5 | Heroic, Mythic only |

Difficulty scales enemy health, damage, **and** rewards — but also cuts your lives and your time
limit. Mythic is not just spongier enemies.

**Lives are shared across the party.** One person feeding deaths costs everyone. Run out and the run
fails. Reaching a boss room sets a checkpoint you respawn at.

You keep your inventory on death inside a dungeon.

---

## Bosses

| Boss | Level | Phases |
|---|---|---|
| **Necro Lord** | 25 | 3 |
| **Ember Tyrant** | 40 | 2 |
| **The Void Sovereign** | 70 | 4 |

Bosses change behaviour as their health drops — new abilities, more damage, summoned adds. Take too
long and they **enrage**. They cannot be dragged out of their arena.

Loot is per-player on the first two, so there is nothing to argue about. The Void Sovereign rewards
whoever contributed most damage.

---

## Economy

```
/rpg shop               list vendors
/rpg shop open general
/rpg bank               savings
```

In a shop: **left click** buys one, **shift-left** buys eight, **right click** sells one,
**shift-right** sells everything matching.

Three vendors: `general` (consumables and basics), `blacksmith` (gear and materials, level 10),
`runes` (socket runes, level 20).

The **bank** is separate from your wallet and earns interest over time. Capacity grows with your
level.

```
/rpg bank deposit 1000
/rpg bank withdraw all
/rpg bank top
```

---

## Playing with others

### Parties

```
/rpg party invite <player>
/rpg party accept
/rpg party chat <message>
/rpg party tp              leader only — summons everyone
```

Party members near you **share experience** — your share is reduced and the rest is split among
them — and share boss loot. Parties enter dungeons together automatically.

### Trading

```
/rpg trade <player>
/rpg trade money <amount>
```

Click items in your own inventory to offer them. **Your items never leave your inventory until both
sides confirm**, so closing the window or disconnecting costs you nothing.

Any change to either offer **clears both confirmations** — nobody can swap the good item out after
you have confirmed. Soulbound items cannot be traded.

### Guilds

```
/rpg guild create <name> <tag>
/rpg guild invite <player>
/rpg guild                     the guild hub
/rpg guild chat <message>
```

Guilds are permanent. They have ranks (Officer, Veteran, Member, Recruit), a shared bank, a shared
storage chest, and a level that rises as members play.

Guild levels unlock **upgrades that buff every member**, bought from the guild bank:

| Upgrade | Effect |
|---|---|
| Hall of Heroes | Strength and Vitality |
| Arcane Library | Intelligence and mana |
| War Room | Damage and crit |
| Bulwark | Defence and damage reduction |
| Treasury | Luck |
| Great Hall | +4 member slots per level |

Ranks control who can invite, kick, promote, use the bank, take from storage and buy upgrades. A
Recruit can put items *into* storage but not take them out.

---

## Pets

```
/rpg pet                open the collection
/rpg pet summon <pet>
/rpg pet dismiss
/rpg pet rename <pet> <name>
```

A pet follows you and grants stats **whether or not it is currently visible**. Pets level as you
fight and some **evolve** — a Wolf Pup becomes a Dire Wolf at 25, keeping its level and name.

Some pets cast spells on their own: the Arcane Wisp, Ember Sprite and Void Drake all attack.

Pets never take damage and never hurt you.

---

## Quick reference

```
/rpg help          every command you can use
/rpg stats         character sheet
/rpg attributes    spend points
/rpg skills        skill tree
/rpg bind <s> <n>  bind a skill
/rpg quest         journal
/rpg dungeon       dungeons
/rpg shop          vendors
/rpg bank          savings
/rpg party         group up
/rpg trade <p>     trade
/rpg guild         guild
/rpg pet           pets
/rpg item inspect  examine an item
```
