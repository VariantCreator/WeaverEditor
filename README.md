# ✨ WeaverEditor
### Build NPCs. Create quests. Run your world.

Create conversations, shops and events for Valheim. Connect nodes to choose what happens when a player talks to an NPC, picks an answer or enters a zone.

## 🧩 What you can do

* **🧙 NPCs and quests:** Make greeters, traders and quest givers with their own outfits.
* **🔗 Graphs:** Connect dialogue, options, conditions, waits and actions.
* **🛒 Player shops:** Give players a Vendor Deed. They stock their shop and choose a payment item, such as Coins or Stone.
* **🎁 Kits:** Give each item its own chance to appear. Wood for everyone, fancy armour for the lucky ones.
* **🌀 Travel:** Create destinations and physical portals. Players use **/warp** or press **E** at a portal.
* **🏮 World tools:** Place lights, pictures, flags and notes. Build camera scenes with music and subtitles.
* **🤝 Community:** Use clans, trading, homes, checkpoints and optional wallets.
* **🛠️ Admin tools:** Manage players, inspect inventories, run events and wear creature costumes.

## 📦 Install

Install **BepInExPack Valheim**, then import the ZIP into **Gale** or your mod manager.

**Use the same build on the server or host and every client.**

For a manual install, copy `plugins/VariantWeaver` from the ZIP into `BepInEx/plugins`. Keep both DLLs together.

When updating, replace the old DLLs and **keep your configs**. WeaverEditor replaces Variant Weaver. The package, folder and DLL names stay the same so existing installs can update.

## 🚀 Get started

**Open the menu**

Press **F8** in a world. Admins get editing tools. Players get Travel, Kits, Quests, Appearance, My Vendors and Community.

**Make an NPC talk**

Place and save an NPC. Create a graph, select the NPC and click **Publish & link**. Close the menu and press **E** to talk.

**Set up kits and travel**

Add kits under **Community → Kits** and destinations under **Travel**. Players open them with **/kit** and **/warp**. **/warp Destination Name** travels directly.

Select a kit item and set **Chance (%)** from 0 to 100. Each item rolls separately. Old entries stay at 100%. These chances also work for chests, graph rewards and spawner loot.

New warps are public. For an older private destination, enable **Available to everyone with /warp** and save it. The server's **Public travel** setting must be on.

When the server blocks restricted items, store metals, Dragon Eggs and other blocked items before travelling. Backpack contents count too. Normal portals keep their own rules.

**Open a player shop**

Add a **Vendor Deed** to a kit and choose its NPC appearance. Players use it to place a shop, deposit stock and set a price. **My Vendors** holds their stock and earnings. Admins can remove shops; owners can still collect what was left inside.

**Trade and find your way home**

Use **/trade** to invite a nearby player. Both players confirm the trade. **/clan**, **/home** and **/checkpoint** open their menus. Set a home with **/sethome Name** inside an active ward owned by your character.

**Decorate and make scenes**

Open **World → Props** for lights, pictures and notes. **World → Scenes** has camera shots, music and the shared media library. Use **Browse / Import…** to add a picture or song, then save its placement or track. Only admins can place world portals and props.

**Try a costume**

Admins can open **Costume**, choose a model and press **Wear / update costume**. Creature controls use its movement and available attacks. Seagulls can walk and fly. Wings included.

Costumes protect you from damage and NPC targeting. Your inventory stays intact. Use the local checkbox to hide your own name and health bar. **Remove costume** returns you to normal. Some modded creatures need their own scripts for special abilities.

Change colours and text size under **Settings → Appearance**. Players have their own Appearance page too.

## 🧰 Other mods

WeaverEditor works with BepInEx on its own. Everyone needs the content mods used by your NPCs, graphs and props. **Guilds**, **Groups**, **Backpacks** and extra inventory integrations are optional.

Choose **Guilds** as the clan provider if you use it. **Groups** can show your party. Keep other free camera modes off while a scene plays. Custom storage and creature systems may need their own integration.

Back up the world and the whole `BepInEx/config/VariantWeaver` folder.

### 📖 [Full guide](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md) · 📝 [Changelog](https://github.com/VariantCreator/WeaverEditor/blob/main/CHANGELOG.md) · 📥 [Downloads](https://github.com/VariantCreator/WeaverEditor/releases)

Inspired by [Pippi](https://steamcommunity.com/sharedfiles/filedetails/?id=3725018456) for Conan Exiles, created by **Joshtech (CoOkIeMoNsTeR)**.
