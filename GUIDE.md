# WeaverEditor guide

Build conversations, quests and events in Valheim with WeaverEditor.

[Getting started](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#getting-started) · [Menus](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#menu-and-editor) · [Shared settings](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#shared-settings) · [First NPC](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#your-first-npc-conversation) · [Nodes](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#nodes-and-connections) · [Quests](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#quests-and-timers) · [Events](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#spawners-zones-and-chests) · [World tools](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#world-tools) · [Imports](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#sharing-graphs) · [Server settings](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#server-settings-and-backups) · [Troubleshooting](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#troubleshooting)

## Getting started

1. Install BepInExPack Valheim, then import the WeaverEditor ZIP into your mod manager.
2. Install the **same WeaverEditor build on the server or host and every client**. Keep `VariantWeaver.dll` and `VariantWeaver.Core.dll` together.
3. Join a world and press **F8**. Server admins and players with assigned permissions can edit content. Other players get Travel, Kits, Quests, Appearance, My Vendors, Community and Costumes, as allowed by the server.

For manual installation, copy the ZIP's `plugins/VariantWeaver` folder into `BepInEx/plugins`. Everyone also needs the content mods used by your graphs. WeaverEditor reads the items and creatures registered by installed mods; use **Mods → Rescan** if an entry is missing.

| Control | What it does |
| --- | --- |
| **F8** | Open WeaverEditor or the player menu |
| **/warp** | Open public warp destinations; no assigned role required |
| **/warp <destination name>** | Travel directly to a public saved destination |
| **/kit** | Open public kits |
| **/return** | Return to the departure point of your last successful WeaverEditor teleport |
| **/tp <player name>** | Ask another player to allow your teleport; requires teleport permission |
| **Fullscreen / Restore** | Expand the editor or return to its window |
| **Esc** | Close WeaverEditor; during ordinary gameplay, open the pause menu and unlock quest-HUD dragging |

Create travel points under **Travel** and kits under **Community**. Mark them public if players should see them in their menu. They can still be used as graph actions without appearing there.

## Player-owned vendors

### Add a vendor to a kit

1. Create and save an NPC with the appearance you want players to receive.
2. Open **Community → Kits**, choose a kit, and add **Vendor Deed** (`VW_VendorDeed`).
3. Select that kit entry and choose its **NPC appearance**, then save the kit. Leave the appearance empty for a basic vendor.

The deed copies the NPC's appearance when placed. Its conversation, graph and admin actions do not carry over. Give the kit a claim limit or cooldown if you want to limit who receives deeds.

### Open your shop

Use the deed from your inventory, choose a nearby spot, and left-click to place it. **Q/E** turns it; **Esc** cancels. The deed is consumed only after placement succeeds. Press **E** at the vendor to open its shop.

Under **Stock**, choose an unequipped inventory item, enter the lot size, and choose the payment item and price. For example, deposit one chest piece and ask for **250 Stone**. Confirming removes those items from your inventory and lists that one lot. Buyers review the goods and payment before purchasing. Quality, condition and saved item details stay with the item.

Payments use the buyer's carried inventory. Equipped, protected and quest items are excluded. Vendor deeds and personal Weaver keys cannot be sold or used as payment. Everyone needs the content mods for the items being traded. Removing an item's mod leaves its vendor stock saved until the item is available again.

### Manage or move your vendor

Open **F8 → My Vendors** to manage your shops. **Earnings** holds payments from completed sales; collect one entry or all of them when you have room. **Listed stock** lets you withdraw an unsold lot.

**Appearance** changes the vendor's name, title, body, hair, beard, colours, outfit and pose. Choose clothing and held items under **Outfit & pose**. These are visual choices; they do not create inventory items or shop stock. Players can only list items they deposit and collect items already held by their own vendor.

**Pack vendor** removes it from the world and keeps its stock and earnings in My Vendors. Use **Place again** to move it without another deed. Only the owner or a server admin can change its appearance or pack it; stock and earnings can only be collected by the owner. Packed vendors still count towards the owner's limit.

### Remove a vendor as an admin

Open **F8 → My Vendors**, find the vendor and choose **Remove vendor**. The shop menu has the same control. Review its name and owner, then confirm.

Removal takes the NPC out of the world and retires the shop. It cannot sell, receive stock or be placed again. Its owner can still collect the saved stock and earnings through **My Vendors**. Admins cannot collect another player's items.

Use **Show removed** to review retired vendors. A trade already in progress must finish before removal. Removed vendors no longer count towards the active vendor limits; recovery records remain saved.

### Vendor limits and backups

The host's `BepInEx/config/com.variantmods.weaver.cfg` has a **Player vendors** section. Defaults are enabled, **3 vendors per player**, **100 per world**, **32 listings per vendor**, and a **100,000-item maximum price**. These limits are enforced by the server. Disabling vendors stops new placements and sales while letting owners recover their items.

Vendors, listings, earnings and pending trades are saved in `BepInEx/config/VariantWeaver/vendors-world-<world ID>.json`. Back up that folder with your world. Keep client `BepInEx/config/WeaverEditor/vendor-receipts` files with character backups; they help recover interrupted trades. Install the same build on the server/host and every client.

## Player records and grave recovery

Open **Players → Known players** to search saved names, account IDs and character IDs. Online players show their current status. Offline records show the last time WeaverEditor saw them. Staff can save private notes and open that player's graves or history. Older names remain searchable.

Open **Players → Graves** and choose **Refresh graves** to scan existing native graves, including ones outside loaded areas. Select a grave and check its owner, death time and position. Unknown owners still appear; a matching name does not prove which account owns an old grave.

**World day** shows the in-game day the grave was created. **Contents not loaded** means its inventory is outside the loaded area; it may still contain items.

Choose your current position, enter coordinates or select a saved recovery area. Review the confirmation before moving. WeaverEditor moves the original grave and keeps its items and owner. It waits for the grave's network owner before moving a loaded grave, and refuses graves marked as in use or with an unfinished inventory transfer. Close its inventory, refresh and retry if it is busy.

**Undo move** returns the same grave to its previous location if it still exists and its contents have not changed. An empty or looted grave cannot be recreated. A recovery message and new map pin reach the owner when they are online, or when that character next joins. Existing death pins are kept.

Server admins have grave recovery access. To delegate it, grant **players.graves** under **Roles**. The default Moderator role does not include it. Player records require **players.view**; staff notes require **players.moderate**. Regular players cannot view these records or move graves.

Open **History** to filter by admin, target player, action, text or date. Results show newest first. Older entries may have only a name in their details; those are marked separately from entries that record the target's account.

Back up the Valheim world and `BepInEx/config/VariantWeaver` together. Graves live in the world save; recovery points, notices and move history live in WeaverEditor's world file.

Grave scans run when requested and show up to 2,000 graves. The menu pages the results so a long list stays manageable. Recent recovery history shows the latest 100 moves.

Close the grave before moving it. You can retry if the list still says it is in use; the server checks its current state. Graves in expanded worlds use the installed world radius. For old graves missing their original spawn anchor, remote players must disconnect before Move or Undo. The menu explains when this is required.

### Spectate an online player

Open **Players → Online**, select a player and choose **Spectate**. Your camera follows their view area while your own player stays where you left them. Move the mouse to look around and use the wheel to change camera distance. Press **Esc** to return, or hold **Alt** and click **Stop**.

Server admins have access. You can delegate it with **players.spectate** under **Roles**. Spectating ends when the player disconnects, changes character or your permission is removed. Return to normal play before using another free camera or a creature costume with movement controls.

### Choose what players see

Open **Settings → Player menu visibility** as a server admin. Toggle Travel, Kits, Quests, Appearance, My Vendors, Community or individual Community tabs. The change is saved on the server and reaches connected clients. Admins still see all pages.

These settings hide F8 pages only. Existing data, feature settings and chat commands remain available. You can also edit **Player menu visibility** in the server's `com.variantmods.weaver.cfg`; saved config changes reload while it is running.

### Admin debug shortcuts

Enable **Admin debug bypass** under **F1 → Server rules** or **F8 → Settings → Server rules**. It starts on. When a server admin has **Debug mode** on, action cooldowns are skipped and **Bring** or **Teleport to player** works without asking that player to approve.

Turn the setting or Debug mode off to use the normal cooldowns and approval prompts again. One-time rewards, inventory travel restrictions, server limits and unfinished transfers still apply. Regular players cannot use the bypass.

### Ghost mode and map privacy

Ghost mode hides your normal appearance, creature costumes, attached effects and name or health bars from other players. Your own view stays usable. Enabling Devcommands also hides your map position, even if your public position was previously enabled. Turning it off keeps your original map preference.

Groups and Guilds position sharing follow the same privacy rules. Server Devcommands remains optional. Use matching WeaverEditor builds on the server and clients for shared visibility.

## Themes, player journal and movable quest tracker

### Choosing a theme

Regular players open **F8 → Appearance**. Admins open **F8 → Settings → Appearance**. The themes are **Valheim**, **Black Forest**, **Frost**, **Ashlands** and **High Contrast**. Accent choices are Theme, Gold, Teal, Blue, Copper, Silver and Ember. Choose **Theme** to use each preset's own accent. Previously saved accent settings are retained.

Choose Valheim lettering or readable lettering, adjust text size, and enable or disable the subtle carved texture. High Contrast does not add grain. Fonts and item icons come from your game or system; no font installation is needed.

These settings affect WeaverEditor's player journal, all admin tabs, WeaverEditor, inventory and selection windows, dialogue, trader menus and quest tracker. Node-category and warning colours remain distinguishable. They do not recolour another mod's menus or the game's own pause/settings screens.

Theme and layout settings are local to each installation. Your choices do not change other players' interfaces.

### Item warning text

Enable **Hide summoned-item warning** under **Appearance** to hide Valheim's warning line in item tooltips. This only changes the text. Item flags, achievements and anti-cheat checks stay unchanged.

To hide the line for everyone, set this in the server's `BepInEx/config/com.variantmods.weaver.cfg`, then restart the server:

```ini
[Server presentation]
Hide summoned-item warning = true
```

Set it back to `false` to let players choose their own display setting. Everyone needs the updated WeaverEditor build.

### Travel, kits and quests

The player menu has **Travel**, **Kits**, **Quests**, **Appearance** and **My Vendors** pages. Travel cards show readiness, cooldown and optional distance/coordinates. The **Return to departure** button uses the same WeaverEditor-only return as **/return**.

Kit cards show availability and item previews. Expand a card to see quantities, chances and the complete contents. Search kits and travel points by name. Claiming kits and using travel follow the server permissions, restrictions and cooldowns.

The quest journal has Active, Finished and All filters. Quest cards show instructions, item counts, destination distance and timers when those values are supplied by the quest. Use the tracked toggle to hide or restore a quest in the HUD. Full instructions remain available in the journal when a tracker row is too short. Abandoning or dismissing a quest still requires confirmation.

### Moving the tracker with Esc

1. Close WeaverEditor and any NPC dialogue, then press **Esc** during gameplay.
2. The tracker shows **MOVE MODE**. Hold the left mouse button on the tracker and drag it to your chosen position.
3. Release the mouse to save. Press **Esc** again to close the pause menu and lock the tracker.

A sample tracker appears in move mode when there are no active tracked quests, so you can arrange it before accepting a quest. When you finish a quest, a short themed completion/update notice may remain visible even when the active list is empty.

While playing normally, the tracker does not intercept mouse clicks or unlock your cursor. Dragging is disabled while WeaverEditor, dialogue, placement, inventory inspection or a native settings/player submenu is open. Closing the pause menu, losing focus or leaving the world ends the drag.

### Tracker settings and reset

Regular players use **F8 → Appearance → Quest tracker**. Admins use **F8 → Settings → Quest tracker**. Available controls:

- Show/hide the tracker, enable Esc dragging and enable quest destination map pins.
- Scale from **0.65× to 1.60×** and width from **280 to 520 pixels** before scaling.
- Background opacity from **35% to 100%** and compact quest rows.
- Maximum **1–6** tracked quests. Extra tracked quests remain in the journal.
- **Move tracker** opens the Esc menu for placement. **Reset position** restores the default placement.

The position is saved as a proportion of available screen space. Resolution, scale and width changes keep the complete panel on screen. Large trackers are automatically reduced to fit smaller screens. The default maximum is three quests.

Preferences are stored in the local `BepInEx/config/com.variantmods.weaver.cfg`, in **Menu appearance** and **Quest tracker**. Use the in-game controls rather than editing the file while the game is open. Reset position does not delete quests or server data.

### Updating from Variant Weaver

WeaverEditor is the new name for Variant Weaver. Update the existing mod to keep your saved content. The DLL names, package identifier and config folders keep their old names so existing installs update correctly. Replace both DLLs together.

Back up your config and world content. Stop the server/game before replacing the existing `VariantWeaver.dll` and `VariantWeaver.Core.dll` with the matching pair from this ZIP. Remove duplicate copies elsewhere in the profile. Update server/host and all clients together. Do not delete `BepInEx/config/VariantWeaver`.

## Optional travel restrictions

Edit the server or host's `BepInEx/config/com.variantmods.weaver.cfg`, under the existing `[Server rules]` section:

```ini
[Server rules]
Block travel while encumbered = true
Block travel with non-teleportable items = true
Extra blocked travel items =
Allowed travel items =
```

Restricted items are blocked by default. The weight rule starts off. Server admins can change either setting through **F1**, or edit the server config. Saved changes reload and sync to players.

The rules cover **warps, /return, teleport to player, Bring player here and graph/NPC teleports**, including admins. The player actually being moved is checked, not a stationary request sender or destination player. Local client config cannot turn off the host's rules.

Weight is checked against the current carry limit. The item rule checks carried items and supported backpack contents. Vanilla metals, Black Metal Scrap and dragon eggs stay blocked by default even if another mod changes their teleport flags. Modded items use their own no-teleport flags. The WeaverEditor rule still applies when the world allows ore through normal portals.

### Ban or allow an item while the server is running

Open **F1 → Server rules**, or **F8 → Settings → Server rules → Travel item overrides**. Keep **Block travel with non-teleportable items** enabled.

* **Extra blocked travel items:** add an item's prefab ID to ban it from WeaverEditor travel. For example, `Wood` blocks wood even though normal portals allow it.
* **Allowed travel items:** add a prefab ID to allow a normally restricted item. For example, `BlackMetalScrap` allows Black Metal Scrap. Remove it to restore the normal restriction.

Separate IDs with commas, semicolons or new lines. Names are case insensitive and must match the whole prefab ID. A blocked entry wins if the same item is in both lists. To unban an ordinary item, remove it from the blocked list. To unban a normally restricted item, also add it to the allowed list.

Wait for **Server settings saved**. The lists sync to connected players without a restart. Editing those entries in the server config also reloads them while it runs. Changes are saved for the next restart. Other travel checks and other mods' own restrictions still apply; these lists do not change ordinary portals or item data.

The travelling player's inventory is checked again immediately before travel, including after another player accepts a pending request. Blocked travel explains why and keeps the previous return point. A rejected warp refunds its warp cooldown; the short anti-spam/retry timers still apply. Store restricted items or reduce weight, then try again. Normal portals and other mods' teleport commands are unchanged.

Install the **same current build on the server/host and every client**. Custom storage supplied by another mod must expose its contents through the player's inventory to be inspected.

The admin **Settings → Server rules** panel shows whether each restriction is enabled and lets server admins edit the item lists. These are server rules, not personal Appearance options.

## Trader menus and player travel

### Trade with a nearby player

Open **Community → Trade**, choose a nearby player and send an invitation. Once they accept, add inventory items or wallet funds. The two panels show **You give** and **You receive**, including quantities, quality and condition.

Choose **Review and confirm trade** and check both offers. Both players must confirm before the exchange finishes. Changing an offer clears the confirmations so nobody agrees to an old price. Use **Cancel trade** to stop; returned items remain available in the trade menu if your inventory is full.

### Item-icon traders

When a dialogue offers a direct Trade action or a straightforward exchange confirmation, WeaverEditor shows an item-icon trader menu. It displays the goods, bundle quantities, price, payment availability and the full exchange. Choose **Buy**, **Sell**, **Barter** or **All**, and use the search field to narrow the list.

Click an offer to select it. **Review exchange** opens an existing confirmation; **Confirm exchange** performs the selected direct exchange through the original graph. One click exchanges one authored bundle. The server still controls the graph and prices; the new menu does not create a separate shop inventory.

Existing straightforward trader graphs need no new import. Conditional offers, multiple-output options, hidden rewards and branching exchanges remain in their authored dialogue paths. An unavailable item uses a placeholder icon and cannot be confirmed through the icon panel. Item names and sprites are read from the installed game/mod items.

### Return from WeaverEditor travel

Use **/return** to go back to where your last successful WeaverEditor teleport started. This covers WeaverEditor travel points, WeaverEditor graph teleports and WeaverEditor player teleports. It does not use general teleport history.

Example: WeaverEditor takes you from your base to a town, then you use a normal portal. **/return** goes back to the base; the normal portal does not replace the WeaverEditor departure point.

A newer successful WeaverEditor teleport replaces the saved point. Failed travel keeps the old point. A successful return consumes it instead of creating a back-and-forth toggle. Return points are session-only and clear when you leave the world or disconnect. A short retry cooldown applies, along with existing WeaverEditor combat and travel restrictions.

## Public /warp access

**New players and players without an assigned role can use public saved warps.** Type **/warp** to open the destination list, or travel directly with an exact, case-insensitive destination name:

```text
/warp Town Square
/warp "Town Square"
```

These are saved destinations, not `/tp` requests to other players. No player acceptance or role assignment is needed for a public warp. Duplicate names ask you to choose from the menu instead of picking an arbitrary destination.

Create a destination under **F8 → Travel → New warp here**. **Available to everyone with /warp (no role needed)** is enabled for new destinations. Existing public warps remain public. Existing private warps are not silently opened: select one, enable that option, and **Save warp** once to open it to every current and future player. You do not have to register or assign each player.

The host/server controls this with its existing setting in `BepInEx/config/com.variantmods.weaver.cfg`:

```ini
[Server rules]
Public travel = true
```

It defaults to `true`; a previously saved `false` setting is respected. Enable it on the host/server and restart if you intentionally disabled public travel earlier. Client config cannot override it. Private warps still require **players.teleport**; creating/editing/deleting warps still requires **world.edit**. Public warps do not grant `/tp`, Bring, coordinate teleports, editing or Costume access.

Menu travel, `/warp <name>` and placed warp portals use the same server-checked destination and per-player cooldown. Enabled combat, encumbrance and restricted-item rules still apply. The existing successful-trip `/return` and failure/refund handling stay in place. No warp can supply its own client-chosen coordinates or move another player.

**Block travel with non-teleportable items** checks carried items, equipment, extra slots and supported backpacks. It reads modded item restrictions too. Vanilla metals and Dragon Eggs stay blocked even if a portal mod changes their item flag. The message names the blocked item; overweight travel has its own message. If a carried inventory cannot be read, travel waits until it can be checked.

These rules apply to WeaverEditor travel, including homes, checkpoints and graph teleports. Normal Valheim portals keep their own rules. Existing server settings are kept when updating. **Personal travel → Require owned ward for homes** controls the owned-ward rule and starts enabled.

### Bring tame companions

Tamed creatures following you can travel with you through WeaverEditor warps. Your ridden mount can come too. Standing livestock, wild creatures and animals following someone else stay where they are.

Under **Server rules**, **Travel with tame companions** starts enabled. **Companion travel range** starts at 10 metres and **Companion travel limit** starts at eight. Admins can change these while the server is running; the server shares the changes with players.

Companions move only after you arrive. They need a safe landing nearby. A companion carrying restricted items, or cargo the mod cannot check, stays behind. Its items stay with it. Normal portals keep their own rules, including any portal mods you use.

Custom cargo mods may need an integration before their storage can be checked.

### Teleport to an online player

Open **F8 → Players**, select an online player, and choose **Teleport to player**. The other player gets a themed **Accept / Deny** popup with your name. **Bring player here** instead asks the selected player to let WeaverEditor move them to you. Neither action moves anyone until they accept.

From chat, use:

```text
/tp PlayerName
/tp "Player Name"
```

Names are case-insensitive. A unique partial name works, but ambiguous matches are rejected. When names are duplicated, choose the player through the menu. The server resolves live positions when it receives the action, rather than trusting coordinates from the player's menu.

Player teleporting and bringing still require admin access or the **players.teleport** permission. This does not grant unrestricted player teleports to everyone. Admins must also get the recipient's approval.

**Accept** permits that one request. **Deny** or **Esc** dismisses it without moving anyone. Unanswered requests expire after **30 seconds**. Denial restores control immediately; accepting waits for the server to validate the request. The popup follows the recipient's selected theme and uses the portal icon. An initial click guard prevents an existing click from accepting a newly opened request.

Only one request can involve a player at a time. A sender must wait at least **10 seconds** between requests, and the recipient gets a brief **5-second** quiet period after one closes. Requests are cancelled when either player disconnects or changes character. They are not saved across worlds or server restarts.

On approval, the server checks the original player sessions, the sender's current permission and the travelling player's combat restriction again. The server includes its current travel rules with the approved effect; the travelling client checks its live inventory and weight before moving. It uses the destination player's **current position**, not where they stood when the request was sent. A stale, expired or replayed approval cannot cause another teleport.

Only a successful approved trip creates or replaces the travelling player's WeaverEditor return point. Denied and expired requests do not alter `/return`. This consent prompt applies to `/tp`, **Teleport to player** and **Bring player here**. Normal portals, named WeaverEditor warp destinations and quest-graph travel do not show this consent prompt. Enabled travel restrictions still apply to all WeaverEditor teleports.

Install the same build on the **server or host and every client**. Older clients cannot use the current travel and costume features.

## Admin Costume

Open **F8 → Costume** in the admin menu. This category uses **admin.powers**, not public /warp access. Native admins and explicitly delegated admin-powers roles can use it; disabling **Allow admin powers** also disables costumes and removes active ones.

Search by model name or prefab ID, or filter **NPCs & creatures**, **Objects**, **Buildings** or **Items**. The list is built from registered content on your installation in small batches. Choose a model, then press **Wear / update costume**. Every viewer needs this build and the relevant content mod to see that model.

**Size ×** accepts 0.1–5. Size 1 keeps the original size. **Edit current fit** loads your current settings, and **Reset fit** resets the size. **Remove costume** restores your player.

Choose **Control creature movement and attacks** to use a creature's real movement, animation and attacks. **WASD** moves, **Shift** runs, and the mouse buttons attack. **R** switches between its available weapons. Flying creatures use **B** to take off or land, **Space** to rise and **Crouch** to descend. Ground creatures use Crouch to switch walking on or off. The camera follows the creature's eye height.

Attacks use the creature's normal cooldown. The controls hint shows when it is ready again.

Seagulls have bird controls. **WASD** walks or flies, **Shift** moves faster, **B** takes off or lands, **Space** rises and **Crouch** descends. Their native wing animation plays in flight. They have no native attack.

Admin costumes protect you from damage and NPC targeting. Controlled bodies are temporary and drop no loot. Your inventory stays intact, and removing the costume restores normal controls and your previous admin settings. Random creature calls are muted. The Costume page lets you show an NPC name and health bar or hide both for everyone. Your player name does not appear while dressed. Ghost mode still hides the entire costume.

WeaverEditor travel keeps your creature costume and resumes its controls when you arrive. Special attacks that depend on a mod's AI scripts may need a separate integration.

Objects and appearance mode keep your normal movement and combat. **Facing degrees**, **Offset from your feet** and the optional idle/movement animation apply to appearance mode. Wearing a chest does not create storage.

Death, logout, switching worlds/characters or losing admin powers clears the costume. It is not saved into your character or the world. The normal model is restored locally if rendering fails or server renewals stop. A failed model does not keep retrying every frame. Automatic changes are server-validated; a client cannot dress another player.

Only standalone visible meshes are supported. Effect-only, script-generated player/NPC equipment (`Player` and `VW_Npc`), models over 2,048 transforms / 256 mesh renderers / 2 million mesh vertices, and missing content are not selectable. Some custom rigs or equipment-driven NPCs can look static or simplified. This is not a guarantee that every prefab from every mod renders correctly. Removing the costume is always the fallback. No desktop files or custom model uploads are used by this feature.

### Updating

Install 1.3.6 on the server or host and every client. Keep **VariantWeaver.dll** and **VariantWeaver.Core.dll** together; remove old duplicate copies rather than leaving two versions installed. Back up and keep `BepInEx/config/VariantWeaver` and your existing WeaverEditor config. This package does not replace saved quests, NPCs or world configuration.

## Player costume rewards

1. As an admin, open **F8 → Costume**, choose a look, then save it as a **Costume reward**. Set its name, size, fit and bar visibility.
2. Open **Community → Kits**, add **Costume Claim**, choose the saved reward and save the kit. Each claim entry gives one claim item; its chance works like other kit entries.
3. Give the kit normally or through a **Give Kit** graph action. The player uses the issued claim from their inventory to unlock the look.
4. Players open **F8 → Costumes** to wear or remove their earned looks whenever they want.

**Grant Costume** unlocks a saved reward directly in a graph. **Has Costume** checks whether that player has it. Both use the selected reward and True/False connections.

Creature rewards can use the same movement and available attacks as admin costumes, including flight for flying creatures. Players keep their normal health and take damage. They do not gain god mode, invisibility or admin permissions. Choose appearance mode in the reward settings to keep normal player movement and weapons instead. Objects use appearance mode; a chest costume is still a player, not free storage. Claims are personal and server-issued; copying an item or changing its saved fields cannot grant another reward.

Reward definitions, unlocks and issued claims are saved on the server. The worn appearance ends on logout; players can wear it again after joining. Missing content stays saved and can be used again once its mod returns. All viewers need the same build and the content used by the reward.

Admins can select someone under **Players → Online** or **Known players**, then open **Player costumes**. Remove their current form, revoke a selected reward or revoke all costume rewards. Revoking also cancels their old claim items. Known players can have access revoked while offline. Give a fresh kit claim or graph reward if you want to grant it again.

## Prop hunt

1. Open **World → Prop hunt** and choose **Place ready arena**. Aim at the ground, rotate with **Q / E**, then click to save its zone and scoreboard together.
2. The starter arena is 40 metres across with chest, chair, workbench and bench props. Choose its name, props, seeker count and player limit. You can also use **New prop hunt** with a zone you already made.
3. The default is 30 seconds to hide and three minutes to hunt. Change the timers and whistle interval, then save the event. **Move whole arena** moves its zone and scoreboard together; **Place scoreboard** moves only the board. Resize its zone under **Zones**.
4. Players enter the zone and press **E** at the scoreboard to join. An admin starts the round once at least one seeker and one hider have joined.

The server assigns roles. Seekers wait behind a dark screen with a countdown and explanation during hide time. Hiders get a random approved prop and can choose another from the scoreboard or **Costumes**. These are ordinary player costumes, with normal damage and controls.

Seekers receive a **Pro Hunt Sword**. Make room for one item before joining. Swing it and hit the prop directly; walls block tags. It does no damage and disappears after the round. Other weapons and **E** cannot tag props.

Hidden props whistle every 30 seconds. Set **Whistle interval** to another value, **0** for silence or **-1** to use the server default. Under **F1 → Server rules**, admins can change that default and the maximum round time, up to 20 minutes including hide time. Game sound effects volume controls the whistle.

Found players wait for the next round. The seekers win by finding everyone; unfound hiders win when time runs out. Death forfeits your place. Leaving the zone or disconnecting has a five-second grace period. Winners must be alive, connected and inside the zone when the round ends.

The wooden scoreboard shows the event name, round state, timer and joined players without opening its menu. Its leaderboard has separate columns for wins and finds. Choose an optional published **Winner reward graph** to run it for each winner once per round. Use **Give Kit** or **Grant Costume** in that graph for rewards. **Join Prop Hunt**, **Leave Prop Hunt**, **Start Prop Hunt** and **Stop Prop Hunt** actions can control the event from a graph.

**Stop / new lobby** ends a round and clears its entrants. Saved rules, board placement and scores survive restarts. A running round ends on restart and does not restart itself. Only admins can create, place, edit or delete these events and scoreboards.

## Menu and editor

The sidebar has icons beside each page. Toggles use a small checkbox next to their description. Button borders start on; change them under **Appearance**. Number fields update as you type.

NPCs, zones, chests and spawners have a searchable browser with enabled and linked status. Select an object to open its settings; expand **Browse** to choose another. Your unsaved object edits stay available while switching within the session.

**Community → Kits** has a compact item list. Search, change quantities directly, or select an item to change it. Set **Chance (%)** separately for each entry, then **Save kit**. 100% always gives the full quantity; 0% never gives it. Fractional chances are allowed. Existing kits start at 100%.

Each entry rolls once per claim. Chests and Give Kit actions use the same rules; spawners roll once per creature. A claim with no successful rolls still uses its cooldown. A full inventory rolls back the reward and releases the claim. **Merge duplicate items** combines guaranteed entries and keeps random entries separate so their odds stay the same.

Save stays at the bottom of the panel. Kits allow 60 rows and 1,000 items per row by default; the server owner can change those limits.

WeaverEditor keeps the current graph name and save state visible. Use the arrows to go back and forward, or **Graphs** to search All, Recent, Linked or Draft graphs. Names such as `Tavern / Greeter` group related graphs.

- All nodes use the same size by default. Longer settings scroll inside the node.
- Shift-click or drag empty space to select nodes. Drag a title to move the selection.
- **Select branch** selects the connected path. Copy/paste keeps connections between copied nodes; reconnect any outside links.
- Align a selection into a row or column. Use the minimap to move around large graphs.
- **Fit graph** shows the whole graph. At a distance, nodes become coloured blocks. Select one and click **Focus**, or double-click it, to return to editing size.
- Click a validation result to find its node. Missing connections appear red.
- Collapse the inspector for more space. Edit node settings directly inside the cards.
- **Connections / Used by** opens related graphs and world objects.

Local draft recovery saves while you edit and does not publish anything. **Recovered drafts** also finds new graphs that were never saved to the server. Compare with the server copy before saving recovered work. Publishing and linking stay manual.

**Settings** controls text size, accent colour, visible rows, node dimensions, minimap, previews and recovery. Server draft autosave is optional and off by default. The server can disable it.

Players can expand a kit to see its items and icons. Travel and kit buttons show their own remaining cooldowns. NPC appearance previews let admins rotate the model before placing it.

## Shared settings

The config is created at `BepInEx/config/com.variantmods.weaver.cfg` after WeaverEditor starts.

| Section | Settings |
| --- | --- |
| Menu appearance | Text size, accent, collapsed sections, browser rows, previews and details |
| Editor preferences | Equal node sizes, dimensions, selection tools, minimap, inspector, local recovery and optional server autosave |
| Server rules | Travel restrictions, public travel/kits, conversations, previews, inspection, admin powers, debug shortcuts, draft autosave and history cleanup |
| Storage | World content limit, saved revision limit and revisions retained per graph after cleanup |
| Server performance | Active creatures and spawns per second |
| Community | Clans, member limits and automatic ranks |
| Personal travel | Homes, home limits and checkpoints |
| Player trading | Nearby trading, distance and timeout |
| Economy | Optional wallets, item deposits, currency precision, PayDay and TaxMan |
| Server scenes | Allow camera and audio actions |
| World images | Approved URL hosts, upload size up to 16 MiB, image dimensions and display scale up to 16 |
| Server media | Admin imports and the shared media disk budget |
| Media | Your local shared-file cache budget |
| Action messages | Server text for combat, cooldown, permission and other refused actions |
| Scenes | Your camera choice, shared server audio, separate Internet audio opt-in and audio volume |

Server admins can change shared settings through **F1** while connected, or edit the server's config. Wait for the saved confirmation. Changes reach connected players; a restart is not required. Other players cannot override server rules. Personal appearance and audio choices stay local. WeaverEditor's debug/devcommands setting controls its own buttons; other mods keep their own controls. Normal portals are unchanged.

### Image, audio and refusal-message limits

Under **World images**, set **Maximum image file size (MB)** from 1 to 16, **Maximum image dimensions** from 1024 to 4096, and **Maximum image scale** from 1 to 16. The server sends these limits to players. Existing uploaded images are kept when a limit is lowered; new uploads and URL downloads use the new values.

Under **Server scenes**, set **Maximum audio file MiB** from 1 to 16. It applies to audio imports/downloads and is sent to connected players. Players can turn shared server audio and Internet audio off independently.

Under **Action messages**, edit the text shown when travel or another server action is refused. Keep the placeholders shown in the setting, such as `{seconds}`, `{reason}` and `{action}`. For an exact old message, add one line to **Other message overrides** in this form:

```text
Original server message => Your replacement message
```

These settings change the wording only. The server still enforces the same rules.

**History → World storage** shows the space used by published graphs, drafts, revisions and player state. Only the server owner can clean earlier revisions. Cleanup first saves the full world file under `BepInEx/config/VariantWeaver/backups`; current graphs, drafts and links are kept.

## Your first NPC conversation

1. Open **NPCs → New NPC**. Give it a name, choose its appearance, then place and save it.
2. Open **WeaverEditor** and create a graph. Add an **Origin**, **Dialogue**, **Option** and **Action** node.
3. Type the NPC's speech inside Dialogue and the player's reply inside Option. Set the Action's type to **Close Dialogue**.
4. Connect the nodes in this order:

   ```text
   Origin → Dialogue → Option → Action: Close Dialogue
   ```

5. Set **Starts from** to **Linked NPC**. Under **Link to**, choose **NPC conversation** and select your saved NPC.
6. Click **Validate**, then **Publish & link**. Close WeaverEditor, face the NPC and press **E** to talk.

**Save draft** keeps your work without replacing the live conversation. **Publish** updates the live graph; **Publish & link** also assigns it to the chosen NPC or zone. The NPC's **On interaction** field shows its saved graph.

To add choices, connect one Dialogue output to several Option nodes. Each Option continues along its own connection after the player selects it.

## Nodes and connections

Choose a colored node shortcut, then edit its settings inside the card. **Action** and **Condition** have a type dropdown for their different jobs.

| Node | Use it for |
| --- | --- |
| **Origin** | The graph's starting point |
| **Dialogue** | What the NPC says |
| **Option** | A reply the player can select |
| **Condition** | Check items, funds, quests, flags, roles, timers or values |
| **Action** | Give rewards, trade, warp, change quest progress or trigger world objects |
| **Wait** | Pause for seconds, including decimals such as `1.5` |
| **Randomiser** | Choose one connected path at random |
| **Bounce** | Jump to a matching Land elsewhere in the graph |
| **Comment** | Leave a note; it does not run |
| **Repeat / Call Graph** | Run a bounded loop or call another published graph |

Click an **output pin**, then an **input pin** to connect them. Conditions use **True** when the check passes and **False** when it fails. Actions with True/False outputs use them for success and failure. Add a failure message where players need to know why something could not happen.

Open **Setup and links** and choose **Delete graph**, then confirm. WeaverEditor keeps the graph if it is still linked to an NPC, zone, chest, schedule, waiting quest or reusable graph call; remove those links first.

Dialogue continues through its output automatically; an Option waits for a player response. A Wait after Dialogue delays the next step. Several connections on a normal output can run several branches; use Options for player choices and Randomiser for a random choice.

| Editing | Control |
| --- | --- |
| Move a node | Drag its title |
| Pan / zoom | Middle-drag / mouse wheel |
| Remove a connection | Right-click its wire |
| Finish typing | Enter or Tab; Shift+Enter adds a line |
| Tidy the graph | Arrange, then Fit graph |
| Reverse an edit | Undo / Redo |

Node positions save automatically for saved graphs. Save a new graph as a draft first.

### Try a graph before publishing

- **Debug draft** lets you step through the graph and inspect branch results.
- **Preview as player** runs without admin roles. Preview controls can simulate inventory, travel and encounter outcomes.
- **Live test on me** runs the **published revision** with real effects on your character and world.

Draft previews use copied state and simulated actions. Finish by publishing and trying the actual NPC or zone interaction.

## Quests and timers

Use **Action → Give Quest** to set a quest key, display name and instructions. The **quest key** identifies the quest; use that same key in **Has Quest**, **Complete Quest**, **Has Completed Quest** and timer checks. A True/False flag is separate from quest progress.

For a timed quest, enter a duration and choose its unit:

- **Expire:** the quest expires when time runs out.
- **Reset:** clears the quest when the timer ends so it can be offered again.
- **Zero duration:** no time limit.

Timers continue while the player is offline. **Has Quest Timer** checks for a running timer; **Quest Time Remaining** compares its remaining seconds. Numeric conditions offer equals, not equals, less than, greater than and inclusive comparisons.

Use **Handoff Quest** to send a player to another saved NPC. Its continuation runs when that player talks to the destination NPC. Keep quest keys consistent across both conversations.

An optional item target and map destination help players follow a quest. Players can track up to three active quests. The displayed item count comes from their inventory; your graph still needs to check the requirement and complete the quest.

## Spawners, zones and chests

### Trigger a named spawner

Create and save a spawner under **Spawners**. Choose its creature, count, maximum alive, cooldown, size, health and loot settings. Health `0` uses the creature's normal health. Settings apply to future spawns; save changes before trying them.

In WeaverEditor, choose **Action → Trigger NPC Spawner**, then select the saved spawner by name. It spawns at its placed position. **False** means the spawner could not activate, for example because it is disabled, cooling down or at its living-creature limit.

Spawners require a graph, zone or manual **Spawn now** trigger. WeaverEditor clears their surviving enemies after a server restart without loot or victory rewards.

### Start an event from a zone

Create a sphere or box under **Zones**, place it and save it. In the graph's **Link to** controls, select the zone and the event you want: Enter, Exit, Stay, First or Last. Use **Publish & link** to save that connection.

**View zone** shows the area with WeaverEditor out of the way; press **Esc** to return. **World markers** shows nearby zones and spawner eggs while moving around.

Zone previews have translucent walls and clear outlines, including the full sphere surface. Adjust **Settings → Appearance → Zone wall opacity** to make them stronger or lighter. Set it to 0 for outlines only. These previews are visible only to admins with zone editing permission.

For a starting example, use **World → Encounters** to create a linked spawner, zone, reward chest and graph. The chest unlocks after the encounter is cleared and locks again on restart.

### Set up a reward chest

Choose its reward kit, name, access rules and protection. **Lock access** and **Protect chest** are separate settings: opening a chest and destroying it are controlled independently.

Choose a one-time reward or a refill cooldown. Claims can be per player or shared across the server. Saving a new refill duration updates active cooldowns.

Keys can be ordinary items or one of eight WeaverEditor key types. Issue a personal key with **Give Key**. It appears in the recipient's inventory and is bound to that player and the selected chest or quest. Personal keys are single-use; regular item keys have a separate consume setting.

## World tools

| Tool | How to use it |
| --- | --- |
| **Placement** | Move while aiming. Q/E rotates; Shift uses 15-degree steps. G toggles a 1 m grid. Page Up/Down changes height. Front arrows show facing. |
| **Placement handles** | Hold Left Alt to drag move/rotate handles. T returns to aiming. Click saves; Shift-click keeps placing a copy. Esc returns to WeaverEditor. |
| **Inspect** | Toggle it to inspect with WeaverEditor closed. Shows player identities and known building creators. Older creators become known when they join; other platforms show their platform ID. Esc returns to WeaverEditor. |
| **History** | Undo recent NPC, chest, zone and spawner edits, including deletions. Undo preserves player progress and refuses to overwrite newer edits. |
| **NPC routines** | Add poses, nearby greetings and patrol points. Set Pause to 0 for continuous walking or use seconds for a stop at each point. Patrols follow straight paths; keep them clear of walls. NPCs pause while talking and when nobody is nearby. |

WeaverEditor travel is blocked during combat and for **20 seconds afterward**, including NPC, graph and admin teleports. Blocked trips do not spend the warp cooldown; teleport actions follow False. Normal Valheim portals work as usual.

## Portals, lights, pictures and notes

Under **Travel**, create a destination, then add a **World portal** and choose that destination. Place and save it. Players press **E** to travel; access, cooldown and combat rules still apply. Removing its destination leaves the portal inactive until you link another one.

Open **World → Props** and choose Lights, Images & flags or Notes. Create the prop, set its appearance, place it and save. For images, turn off **Show wooden backboard** to display just the image. Flags have a **Show wooden flag pole** toggle. Existing images keep their backing until you change it.

Only server admins can place, edit or remove these portals and props. Players can use portals and read notes.

- **Lights:** save a light type with RGB or hex colour, brightness and range, then use **Place copies of saved type**. Each click adds a separate light; Esc finishes. Editing a type updates all copies. Select a copy to move or remove it. Shadows are limited to eight placed lights.
- **Images:** click **Browse / Import image…** or **Choose from media library**, select a PNG/JPG and save the placement. Windows Browse opens your PC’s normal file explorer. Other platforms can paste a full path into **Media library → Local file path** and choose **Import file from path**. The host/server stores shared files once. Limits are up to 16 MiB and 4096 × 4096, with display scale up to 16. Library thumbnails show the saved files; pictures keep their proportions.
- **Image URLs:** choose **Switch this draft to an approved URL** when necessary, enter a direct image link and save the placement. Approve its host in **World images → Allowed image hosts** on the server. Uploaded files work without an external website.
- **Flags:** turn on **Tall flag shape** for a portrait display.
- **Picture facing:** the gold **FRONT** arrow points out from the picture side while placing images or flags. Use **Q/E** to turn them.
- **Notes:** write plain text, up to 4,000 characters. Players press **E** nearby to read it.

## Community hub

Players and admins can open the Community hub from **F8**.

- **Clans:** create a clan, invite players, accept invitations and manage membership. Leaders can transfer leadership or disband. Admins can manage all WeaverEditor clans.
* **Homes:** use **/sethome Name**, **/home Name** and **/delhome Name**. Saving or moving a home requires your active ward. With Guilds and ProtectiveWards, members can also use an active ward bound to their guild with guild access enabled. Being ordinarily permitted in someone else's ward does not qualify. Homes are private and obey WeaverEditor travel restrictions.
- **Checkpoints:** a **Set Checkpoint** action saves the NPC/zone location or a chosen travel destination. **Has Checkpoint** checks it and **Clear Checkpoint** removes it. Players choose whether to use it after death.
- **Ranks:** admins create permission-free ranks and set promotion rules for playtime or completed quests. **Grant Rank** and **Remove Rank** actions can change them in a graph. These actions cannot grant admin access.

The server controls these features and their limits. Turning a feature off keeps its saved data.

### Guilds and Groups

Guilds and Groups are optional. Under **Community → Clans**, admins choose **Auto**, **Weaver** or **Guilds** as the clan provider. Auto uses Guilds when its server membership is ready; otherwise it uses WeaverEditor clans. Your saved WeaverEditor clans are kept when you switch.

Use the original Guilds menu to create and manage external guilds. **Has Guild**, **In Guild**, **Is Guild Leader** and **Same Guild** conditions read membership from the server. If Guilds is missing or unavailable, those checks follow False.

Groups can show your party in the Community hub. Its current API provides personal client data, so **Has Group** cannot unlock server rewards and follows False. Admins can turn both integrations off in the same page or the **Integrations** config section.

## Player trading and wallets

Open **/trade**, choose a nearby player and send an invitation. The other player opens **/trade** to accept. Deposit the items you want to offer, then review both sides and confirm. Changing an offer clears both confirmations.

The server holds deposited items until both players confirm. Moving too far away, disconnecting, cancelling or a timeout ends the trade. Items return through saved recovery parcels. If your inventory is full or an item mod is missing, make room or restore the mod and click **Collect**.

**/wallet** opens the optional server wallet. It starts disabled. Admins can enable it, name the currency and choose an ordinary item for deposits and withdrawals. Wallet payments can be included in player trades. Existing physical Coin actions keep their original behaviour.

Admins can adjust accounts under **Wallet → Admin accounts**. **Economy settings** controls PayDay payments and TaxMan percentage taxes; both start off. Currency precision is chosen for a new world and stays fixed once balances exist.

Use **Has Wallet Funds**, **Give Wallet Funds** and **Remove Wallet Funds** for wallet amounts in graphs. Enter a decimal amount in the node's Amount field.

## Numeric entry and zoomed-out nodes

Type directly into number boxes, including with the numeric keypad. Decimal fields accept `0.25` or `0,25`; partially typed values such as `-` and `0.` remain visible while editing. Press Enter or leave the field to finish. Counts and other integer-only settings still require whole numbers, and each setting keeps its normal limits. Input lettering stays readable even when Valheim-style lettering is chosen for headings.

Zoomed-out graph cards show their action and saved asset name, such as **Play Audio / Music**, rather than an internal ID. Missing assets show a readable missing-reference label. Zoom in or use Focus to edit the card’s fields.

## Camera shots, audio and skills

Open **F8 → World → Scenes** for Camera shots, Audio tracks, Media library, Setups and Groups. The existing graph node toolbar stays in place.

### Place and aim cameras

Create a shot and choose **Add free camera**. Mouse movement aims; **WASD** flies, **Q/E** moves down/up, **Shift** is faster, **Ctrl** is slower and the wheel changes FOV. **Left-click** places a camera and keeps the rig active for the next one. **Enter** also places. **Esc** finishes and retains the draft; **Save shot** persists it to the host/server. Repositioning replaces the selected point on the first click; later clicks append new points.

Each shot supports 16 points. Select a point to change its label, world position, pitch, yaw, roll and field of view. Text boxes support decimals, with steppers/sliders for small changes. **Look through** holds that draft camera view until Esc. **Preview from here** starts the current draft at the selected camera; **Preview this draft** starts from the beginning. Previewing does not require overwriting the saved shot.

**Show camera models, labels and direction arrows** shows the selected shot’s local editor markers and connecting path. Labels include the shot and point names. Markers are not persistent world props and are hidden during scene playback. All shot points must stay within 500 metres of the player who receives the scene, so the camera remains in their loaded area. Playback hides the HUD/crosshair. **Stop Camera**, Esc, death or leaving the world restores the camera.

### Per-camera timeline

Existing shots retain legacy travel/final-hold timing. Enable **Use per-camera timeline** to give every point its own settings. The first point starts immediately; each later point controls travel *into* that camera. Choose **Cut** for an instant change, **Linear** for constant-speed interpolation or **Smooth** for an eased start/stop. Moving segments allow 0–20 seconds and every camera holds for 0–30 seconds, including decimals. A whole timeline is limited to 600 seconds.

Click a timeline card to edit it. Drag it onto another card to reorder, or use **Earlier / Later**. Music/subtitle cue timestamps stay at their absolute time when cards move; check them after reordering or shortening the shot. Invalid cues beyond the new end must be moved or removed before saving.

Add a **Music cue**, **Dialogue cue** or **Stop audio cue** at a chosen number of seconds. Dialogue cues are cinematic captions, each visible for 1–30 seconds with up to 500 characters. They use a Valheim frame and lettering. Choose a base text color, or select words and use **Color selected words**. You can also write `<color=#E2B960>gold words</color>` directly. **Text speed %** works like a Dialogue Node: 60 is the usual speed and 0 shows the whole message. Give longer messages enough visible time to finish typing.

A shot supports 64 cues. Timeline Stop audio affects that scene’s cue track. **Stop this scene’s timeline audio when it finishes** defaults on. Turning it off lets that track continue under its own duration/loop rules, but leaving its parent zone still clears it. Esc cancels the scene and its cue music.

### Shared image and music library

Open **Media library** to search and page through imported files, see image thumbnails or preview 30 seconds of an audio file. **Browse / Import image…** and **Browse / Import audio…** open the Windows file dialog on the editing PC—not on the remote dedicated server. **Local file path → Import file from path** is the non-Windows alternative. Desktop drag-and-drop is not a control in this version.

The chosen file uploads to the host/dedicated server with progress and a Cancel control. Authenticated server admins may import, rename, replace or remove entries. Uploads are limited by type, size, checksum and storage budget. PNG/JPG/JPEG images use the server’s image bounds; MP3, Vorbis OGG and WAV audio use its 1–16 MiB limit and a maximum decoded duration of 10 minutes. Web pages, live streams and other OGG codecs are not supported media files.

Import once, then choose that entry from any number of image placements or audio-track settings. Audio volume, fades, priority and loop settings belong to each saved track, not to another copy of the file. **Save audio** or save the image placement after selecting a file. Importing by itself creates the reusable library entry, not a world prop or playback graph.

Select an entry and confirm **Replace everywhere** to upload a replacement into the same library identity. All saved images/tracks referencing it move to the new content hash. Already playing audio retains the old stream until it ends; subsequent plays use the replacement. Active editor drafts that used it are updated on the importing client. Other admins should refresh their drafts before saving. Renaming changes the library label, not the names of individual tracks/props. Referenced entries cannot be deleted until their saved track/image references are removed.

Files live on the host/server in `BepInEx/config/VariantWeaver/media-<world ID>`. Existing pre-library image uploads stay in `images-<world ID>` and continue to work. **Back up both folders with `world-<world ID>.json` and its `.bak`.** Media bytes are not placed in graph/world JSON or the public mod ZIP. Graph exports do not carry the shared files with them.

Under **Server media**, **Allow admin imports** can disable new imports, and **Storage budget MiB** defaults to 256 (32–2048 supported). There are up to 200 library entries. Replaced/deleted blobs remain on disk for saved-world backups and still count towards this quota; removal of a library entry is not a disk-cleanup action. Do not manually remove files still referenced by the world or backups. On each client, the reusable shared-file cache is under `BepInEx/cache/WeaverEditor/media`, bounded by **Media → Local cache budget MiB** (default 256; 32–1024). In-use streaming files stay pinned until released. This cache is not the authoritative server library.

### Music zones, fades and priorities

Under **Audio tracks**, create a track and choose a library file, Browse/Import one, or switch to a direct Internet URL. Imported music uses the player’s **Shared server audio** setting, on by default. Direct HTTP(S) audio still requires their separate **Internet audio** opt-in, off by default. Both respect the player’s scene volume. Server script permissions and audio size limits still apply.

Set **Fade in seconds** and **Fade out seconds** (0–30, default 2), playback duration, loop and priority. A track priority and its zone’s **Music priority** are added; higher values take over. Equal-priority renewals remain stable instead of constantly switching. At most one main track and one outgoing fade are audible. Leaving the winning zone allows the lower-priority active zone to resume with a fade; renewing the same loop does not restart it. Scene cue music has precedence over regular zone tracks. These controls affect WeaverEditor music, not vanilla background music or other mods’ audio.

**Stop Audio → Stop scope** defaults to **This zone / graph source**. An outer zone’s exit must not stop a newer inner-zone track. Choose **All scripted music for this player** only for a deliberate global stop. Stop begins a fade without holding the graph until silence. The server also clears departed/disabled/deleted zone owners, including after teleports, and cancels their pending playback. Source-scoped stops from zones should run through that zone’s enter/exit/stay graph bindings so they carry the same source identity.

Nearby zone and timeline music can preload automatically when that audio source is enabled. Up to three candidates are sent ahead of entry, with four streaming clips in the client’s session cache. Use **Preload this audio** to prepare a selected draft without playing. **Clear local audio cache** stops scripted music and clears streaming/temporary URL entries; it does not erase the persistent shared-file library cache. Replacing a file at the same Internet URL needs this clear action or a new URL. Library replacements use content hashes automatically.

Audio status shows Loading, Ready, Playing or Failed, plus recent startup timing for cold, disk-cached and memory-cached playback. The timings include transfer/cache work, file write, clip decode and the largest observed frame-update delta during preparation. They are local diagnostics, not a full Unity audio-profiler trace. The first uncached play can still take time, especially after teleporting directly into a zone. Preloading ahead of entry helps avoid starting a download at the same moment as playback.

### Groups and direct world editing

Open **Groups** or **Select objects in world** from the camera/prop screens. In selection mode, click a light, image, note or camera label/model to inspect it. **Ctrl/Shift-click** builds a multi-selection. Hold the **right mouse button** to look and fly with WASD/QE; Shift is faster, Ctrl slower and the wheel changes FOV. Without right mouse, the pointer stays available for editing. **Esc / Return to groups** ends selection.

The side inspector edits position, facing, size, light appearance, image backing and camera fields. **Save placement / Save camera shot** persists the draft. A camera offers **Look through** and **Open full timeline**. Labels can be selected even when a light has no useful collider. The view limits the displayed labels to nearby visible objects to avoid covering the scene.

Create a named group from the current selection or select its members on the Groups page. An object/point belongs to one group. Save, then use a translation offset to **Move** or **Duplicate** it. Copies get independent placement and camera IDs while reusing light types and media. Moving affects world objects, not only editor labels. The limits remain 200 placed props, 100 saved camera shots, 100 groups and eight shadow-casting lights.

**Locked** prevents accidental saving/moving/removing of group members. Save the group unlocked before changing membership. Locking any camera point protects its whole shot from conflicting edits. **Hide editor markers** affects editor overlays, not actual lights/images/notes. Removing a group keeps its objects. Duplicating every point of a shot copies its timeline cues; duplicating only part of a shot creates a new shot without the original time-based cues, with a warning.

For lights, keep **Override only this placement** off to inherit the saved light type. Updating that type changes all non-overridden copies. Turn it on to give one placement its own colour/hex code, brightness, range, enabled state, size and shadows. Turning it off reapplies the type. The eight-shadow-light limit counts all actual placed copies, not just saved types.

### Ready-made setups

Open **Setups** and choose **Music zone** or **Boss introduction**. Choose the centre/radius, audio track, zone priority and optional fades/loop settings. The boss version also chooses a saved camera shot and a saved or new creature spawner, with a global cooldown. Creature choices come from the installed game’s catalogue.

**Create and enable** publishes the ordinary graphs, creates matching editable drafts and links/enables the zone immediately. Players already inside can trigger it. Check the location before confirming. A music zone creates enter/play, stay/renew and exit/stop graphs. A boss introduction links cooldown, music, camera and spawner; audio/camera opt-outs or an early end do not strand the graph before the encounter. Different loop/fade settings create a separate track-settings record but still reuse the imported file.

These are normal graphs and zone/spawner records. Edit them with the existing toolbar and normal publish/link workflow. The wizard does not create a hidden template runtime that prevents later changes.

**Set Skill Level** sets a native Valheim skill from 0 to 100. **Skill Level Range** checks its base saved level against inclusive bounds before temporary bonuses.

## Sharing graphs

Put graph JSON files in `BepInEx/config/WeaverEditor/exports`, then choose **Import** in WeaverEditor. **Export** writes files to the same folder. On first launch after updating, existing exports move here automatically. Files with matching names and different contents are kept under separate filenames.

New exports include link names. Imports match unique names and ask you to resolve missing or ambiguous references. Positions and wires are preserved; **Arrange** tidies the layout. Choose the destination NPC or zone on your own server, review item and spawner references, then **Publish & link**.

## Server settings and backups

When updating, replace the mod files on the server and every client, then restart them. **Keep and back up `BepInEx/config/VariantWeaver` alongside the Valheim world.** It holds graphs, NPC and zone links, kits, travel points and player progress.

Uploaded pictures and music are stored on the host/server in the matching `media-<world ID>` and `images-<world ID>` folders under `VariantWeaver`. Keep those folders with the world JSON when backing up or moving the server. Clients receive shared files from the server. Direct Internet links still depend on their original host.

The server allows **8 MB of saved WeaverEditor content per world** by default. This includes published graphs, drafts, earlier revisions and other saved state, rather than a separate allowance for each graph. Larger network transfers are compressed automatically.

To increase the limit, stop the server and edit `BepInEx/config/com.variantmods.weaver.cfg`:

```ini
[Storage]
World content limit (MB) = 16
```

The supported range is **1–16 MB**. Clients do not need matching config values, but they do need the same mod build.

Server performance defaults are **200 active WeaverEditor creatures** and **40 new creatures per second**. A blocked spawner follows False. Graphs share a work budget and continue on later ticks when busy.

## Troubleshooting

| Problem | Check |
| --- | --- |
| NPC has no conversation | Save and enable the NPC, publish the graph, then use Publish & link. Close WeaverEditor before interacting. |
| Preview works but Talk does nothing | Preview can run a draft. Check the published graph, its entry node and the NPC's saved On interaction field. |
| A spawner is missing from a dropdown | Save the spawner, refresh WeaverEditor, then select it by name. |
| An event will not start | Check the saved zone binding, cooldowns, enabled state and spawner's live status. |
| An imported graph has missing targets | Resolve its links and install the content mods its items or creatures need. |
| Travel or kits are missing for players | Mark them public and save. |
| Version mismatch or repeated old media-limit warning | Update both server and clients to the same current build. Image and audio limits come from the server config and are sent to connected players. |
| Imported media stops working after moving the server | Copy the matching media/image folders with the world JSON; shared files are not bundled in graph exports. |
| Browse does not open on Linux/macOS | Use a full local file path in Media library; the native picker is Windows-only. |
| A group member cannot be saved | Save the group unlocked first; a locked camera point locks its shot. |
| Music is silent | Check the matching Shared server audio / Internet audio setting, server script policy and the audio status/error. |
| A server restart loses content | Check that the server retains its WeaverEditor config folder and world identity. Restore your backup if needed. |

If an older build already cleared a link, select its NPC or zone and use **Publish & link** after updating. For unresolved problems, include the mod version, what you clicked and the relevant client/server `BepInEx/LogOutput.log`.

## Inspiration and credit

WeaverEditor is inspired by [Pippi — User & Server Management](https://steamcommunity.com/sharedfiles/filedetails/?id=3725018456) for Conan Exiles, created by **Joshtech (CoOkIeMoNsTeR)**. Credit to Joshtech for the NPC tools and visual quest editing that inspired this project. WeaverEditor is an independent Valheim mod, with its visual editor named **WeaverEditor**.

### Journal icons

Warps show a glowing portal, kits a supply chest, and quest headings a sealed scroll. The tracker uses the same scroll. Item objectives keep their native item icons. These icons are included in the mod and do not require an extra download.
