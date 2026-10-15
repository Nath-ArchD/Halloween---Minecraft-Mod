# Halloween Minecraft Mod: Project Plan and Handoff

Status: **planning only. No code has been written yet.** The repo contains just `README.md` and this file.

> All mod names and availability below were listed from memory, not verified. Check every mod on Modrinth for a **Fabric 1.20.1** build before adding it to the pack. Items marked *(check)* are the ones most likely to be missing or Forge-only.

---

## 1. Decisions made

| Topic | Decision |
|---|---|
| Mod loader | **Fabric** |
| Minecraft version | **1.20.1** (recommended, not yet confirmed by the user). Chosen because the Create Fabric port and most decoration mods are most mature there. |
| Java | 17 (1.20.1 requires it). The dev container has Java 21 installed, so a Java 17 toolchain may be needed. |
| Audience | The user and their friends, on a shared server or world |
| Playstyles | Both **builders** (pretty blocks, Create contraptions) and **adventurers** (bosses, dungeons, magic). Builders and adventurers are linked by a trade loop (see section 4). |
| Pack size | Roughly 50 to 70 mods to start, 100 at most. Add in layers and test after each layer. |
| Distribution | Modrinth or Prism launcher, exported as a `.mrpack` that friends import in one click |

## 2. Modpack list (to verify)

**Core and performance:** Fabric API, Sodium, Lithium, FerriteCore, Entity Culling, ImmediatelyFast, Iris Shaders, Mod Menu, Cloth Config, Continuity

**Create:** Create Fabric, Create Deco, Create: Steam 'n' Rails, Create Interiors *(check)*, Create: Garnished *(check)*

**Building and decoration:** Chipped, Handcrafted, Supplementaries, Macaw's (partial on Fabric), Every Compat, Another Furniture, Twigs, Rechiseled *(check)*, Dramatic Doors *(check)*, Immersive Paintings, Dynamic Lights, Farmer's Delight (Refabricated)

**World and exploration:** Terralith, YUNG's Better Dungeons / Strongholds / Nether Fortresses, Incendium and Nullscape, Ambient Sounds or Sound Physics Remastered

**Mobs:** Naturalist, Friends & Foes, Ender's Delight. (Mowzie's Mobs is Forge-only as far as we know, so skip it.)

**Magic (keep to about 3 systems):**
- Botania (nature and automation, pairs with Create)
- Spell Engine with Wizards / Paladins & Priests / Rogues & Warriors (class-based, easy for adventurers)
- Hex Casting (programmable magic, optional "expert" content; needs Patchouli, Paucal and other libs)
- Not on Fabric, so do not plan around them: Ars Nouveau, Iron's Spells 'n Spellbooks, Occultism, Hexerei. Witchery-style mods vary, so search Modrinth for "witch" or "ritual".

**Quality of life and multiplayer:** JEI or REI, AppleSkin, Xaero's Minimap and World Map, Jade, Simple Voice Chat, Patchouli, FTB Quests or FTB Chunks *(check Fabric support)*

## 3. The custom Halloween mod (this repo)

First milestone, in order:

1. **Candy and relic items.** These are the shared currency. Candy gives effects (speed, jump boost, fire resistance), and eating too much causes a "sugar crash".
2. **Pumpkin King boss.** A multi-phase boss (fire, then flying pumpkin minions, then a pumpkin-bomb finale) meant for 3 to 4 players.
3. **Boss-drop decoration blocks.** A few exclusive blocks (coffin, skull candle, cursed glowing block) that builders can only make from adventurer loot.
4. **Blood moon event.** Mobs are stronger, drops are better, and magic is stronger.
5. **Halloween Handbook.** A Patchouli guidebook that every player spawns with. It covers quick start, goals, boss ladder, what each mod is for, and the builder/adventurer trade loop.
6. **Starter advancement tree.** Uses vanilla advancements (no extra mod needed), for example: build a shelter and a Create water wheel, get first candy, survive the first blood moon, defeat the Pumpkin King.

Later ideas, not in scope yet: trick-or-treat villages, Headless Horseman, mimic chests, a haunted house generator, a ghost mode on death, a witch's broom, Skeleton DJ, hide and seek, graveyard wave survival, costume contest, a bounty board.

## 4. Design intent: one world, two playstyles

- **Builders** get the full decoration mods, Create, Dynamic Lights, and a safe, mob-free "Spooky Village" build area.
- **Adventurers** get a dangerous world (Terralith, YUNG's), the Halloween bosses, and a difficulty ramp where mobs get stronger the further from spawn.
- **Trade loop:** adventurers bring back candy, relics, and rare materials. Builders turn those into exclusive decorations. Builders also craft gear, potions, safe bases, and Create-powered traps for adventurers.
- **Onboarding:** friends pick a role (Builder, Adventurer, Mage/tinkerer, Farmer/cook) and only need to learn that part. Run a first-hour test with one new friend and fix the places they get stuck.

## 5. Open questions for the user

- Confirm **Fabric 1.20.1**, or check whether the Create Fabric port now supports a newer version.
- Survival-focused or creative-focused? (Asked earlier; the answer so far is "both", with a trade loop.)
- Which magic systems to include: class-based (Spell Engine), programmable (Hex Casting), nature and automation (Botania)?
- Who hosts the server, and is it modded Fabric server or single player/LAN?

## 6. Handoff: what the next session should do

**Do not** create a pull request unless the user asks.

1. **Verify versions first.** The last attempted step (a `curl` against the Fabric maven and meta endpoints) was **interrupted by the user before it ran**, so none of these are confirmed. Look up the current Fabric Loom, Fabric Loader and Fabric API versions that match 1.20.1 (Fabric API versions look like `0.9x.x+1.20.1`). Ask the user before running network commands.
2. **Scaffold the Fabric project** in this repo: `build.gradle`, `gradle.properties`, `settings.gradle`, Gradle wrapper, `src/main/resources/fabric.mod.json`, a `ModInitializer` main class, a `.gitignore`, and an updated `README.md`. Set the Java toolchain to 17.
3. **First content:** one pumpkin-themed item (candy) and one block, to prove the build works with `./gradlew build`. Then build the milestone items in section 3 one at a time.
4. **Add the Handbook and advancements** once the core items exist.
5. **Pack manifest:** keep a `modlist` file (or a Modrinth `.mrpack` index) in the repo so friends can install the pack. Verify each mod there against Modrinth.
6. Keep commits small and push to the designated branch with `git push -u origin <branch>`.

Environment notes: working directory is `/home/user/Halloween---Minecraft-Mod`. The repo has one commit ("Initial commit"). Outbound HTTPS goes through a proxy, so see `/root/.ccr/README.md` if network tools fail.
