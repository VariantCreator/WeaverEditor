# 1.3.6

A collection of bug fixes and improvements

# 1.3.5

A collection of bug fixes and improvements

# 1.3.4

A collection of bug fixes and improvements

# 1.3.3

* Recover existing graves, including graves owned by offline players.
* Save recovery areas and undo a move while the grave contents are unchanged.
* Search known players and keep staff notes.
* Filter history by admin, player, action and date.
* Spectate online players as an admin. Esc brings you back.
* Choose which F8 pages players see without turning their features off.
* Ghost mode hides your normal form and costumes. Devcommands keeps you off the map.
* Fixed placement menu errors and cleanup when leaving a world.

Keep your configs. Update both DLLs on the server or host and every client.

# 1.3.2

* Kit items now have their own drop chance.
* New warps are public. Use **/warp Destination Name** to travel directly.
* Fixed blocked items getting through travel, including backpack contents.
* Setting a home requires an active ward owned by you.
* Fixed creature attacks and bosses getting stuck while waking up.
* Seagulls can walk and fly. Wings included.
* Costumes protect you from damage and NPC targeting. You can hide your own name and health bar.
* Stopped random creature calls while wearing costumes.
* Clearer zone walls and readable saved menu sections.

Keep your configs. Update both DLLs on the server or host and every client.

# 1.3.1

* Fixed image previews getting stuck after closing or reopening them during loading.
* Stopped old media requests from interfering with a new world session.
* Fixed stale music positions after changing tracks or stopping a preempted music zone. Temporarily interrupted active music still resumes.
* Reimporting a valid file can now repair its damaged stored copy without creating another copy or bypassing the storage limit.
* Released old image textures when a saved image reply arrives more than once.
* Kept the existing menu layout, node toolbar, camera tools and saved content format.

Back up the world and `BepInEx/config/VariantWeaver`. Update both DLLs on the server or host and every client together.

# 1.3.0

* Added a shared image and music library with Windows Browse/Import, path import, thumbnails, previews, search and Replace everywhere.
* Added per-camera timeline travel, holds up to 30 seconds, Cut/Linear/Smooth transitions, drag ordering and music/subtitle cues.
* Added named groups, multi-selection, move/copy, editing locks and hidden editor markers.
* Added direct world selection with a side inspector, camera labels/path lines and Look through controls.
* Added per-placement light overrides and numeric steppers/sliders alongside the existing text fields.
* Added music-zone and boss-introduction setups that create normal editable graphs.
* Added source-specific Stop Audio, zone/track priorities, crossfades, lower-priority music restoration and startup diagnostics.
* Kept the existing node toolbar, continuous camera placement, decimal entry, hex colours and optional image backing.

Update the server or host and every client together. Back up `BepInEx/config/VariantWeaver`, including image/media folders, with the world.

# 1.2.8

* Numeric text boxes use readable input lettering and preserve unfinished numbers while editing.
* Free camera placement uses left-click and stays active for multiple points. Press Esc when finished, then Save shot.
* Added optional camera models with direction arrows for the selected shot. These do not appear during scene playback.
* Zoomed-out nodes show the action and saved asset name instead of internal IDs.
* Added bounded audio caching, background cache writes and automatic nearby-zone preloading.
* Added Preload this audio and Clear local audio cache controls.
* Kept the existing 30-second camera holds, reusable light types, hex colours, audio fades and optional image backing.

Update the server or host and every client together.

# 1.2.7

* Added freely positioned scene cameras with editable aim and holds up to 30 seconds.
* Camera playback hides the HUD and crosshair.
* One saved light type can place multiple lights; added hex colour entry.
* Fixed decimal entry in numeric editor fields.
* Added audio fade-in/out and cancellation of pending zone audio.
* Images can hide their wooden backing; flags can hide their pole.

* Fixed restricted-item travel using the overweight message.
* Added a confirmed Delete graph action. Linked graphs must be unlinked first.

Update the server or host and every client together.

# 1.2.6

* Added an image file chooser, upload previews and clearer messages.
* Fixed picture materials and image proportions.
* Cleaner Community tabs and better layouts on smaller windows.
* Fixed clipped coordinates, button alignment and placement labels.
* Players can use the centre of warp portals with E.
* Image uploads, display scale and scene audio limits can be set up to 16 in the server config.
* Server admins can edit the messages shown when an action is refused; changes reach connected players without a restart.
* Restricted-item travel now uses its own message instead of the overweight message.
* Added a confirmed Delete graph action. Graphs with saved links must be unlinked first.

Update the server or host and every client together.

# 1.2.5

* Admins can remove player vendors. Owners can still collect their stock and earnings.
* Added Give item and Remove item to the admin inventory view.
* NPC outfits and hair load sooner, including items that register late.
* Added placeable warp portals linked to travel destinations. Press E to travel.
* Added lights, image displays, flags, notes, camera shots and optional audio.
* Added clans, homes, checkpoints, earned ranks, player trading and optional wallets.
* Added optional Guilds membership and Groups party display.
* Cleaner navigation with grouped pages and optional button borders.

Update the server or host and every client together.

# 1.2.4

* Fixed vendor placement getting stuck in long mod-manager profile paths.
* Fixed local draft recovery in those profiles. Existing receipts and drafts are kept.

Update the server or host and every client together.

# 1.2.3

* Added player-owned vendors. Give players a Vendor Deed through a kit.
* Sell stocked items for Coins, Stone or another item. Owners collect payments in My Vendors.
* Owners can change their vendor's appearance or pack it away. Stock and earnings stay saved.

Update the server or host and every client together.

# 1.2.2

* Renamed the mod to WeaverEditor. Existing saves and settings carry over.
* Graph exports now use the WeaverEditor folder. Existing files move automatically.
* Fixed graph wires drawing over the menus.
* Large graphs now fit on screen. Use Focus or double-click a node to edit it.

Update the server or host and every client together.

# 1.2.1

* Added optional travel limits for heavy inventories and non-teleportable items.

# 1.2.0

* Renumbered the latest teleport-approval build to 1.2.0.
* Keeps the themed menus and movable quest tracker, updated portal/chest/scroll icons, traders, /warp, /kit, /tp, /return and player teleport approval.
* No gameplay changes in this version update.

Update the server or host and every client together.

# 1.1.1: Teleport approval, menu themes and quest tracker

* Player teleports now ask the destination player to accept or deny.
* Bring player here asks the player who would be moved.
* Theme-matched popup with portal icon, countdown and Esc to deny.
* Requests expire after 30 seconds, cannot be stacked, and cancel when a player leaves.
* Existing permissions, travel restrictions and Weaver-only return tracking are preserved.

* Replaced the simple warp, kit and quest symbols with a portal, supply chest and sealed scroll.
* Added the matching scroll to the quest tracker while keeping objective item icons.
* Changed the player travel command to `/warp`.

* Valheim-inspired frames, lettering and shared styling throughout Weaver.
* Five themes with local accent, text-size and lettering options.
* Redesigned player travel, kit and quest pages with clearer cards and item icons.
* Theme-matched quest tracker and quest update notices.
* Move the tracker by pressing Esc and dragging it. Position saves on release.
* Tracker width, scale, opacity, compact rows, quest count and position reset.
* Appearance options are available to regular players as well as admins.

This build keeps the trader, /return and player-teleport features from 1.1.10.
The requested 1.1.1 label sorts below 1.1.10; use manual installation.
Update the server and every client together.

# 1.1.10

* Larger dark-and-gold conversations with scrollable text and responses.
* Item-icon trader menus with quantities, prices, search, filters and exchange details.
* Supported existing trader graphs work without rebuilding their offers. Conditions and prices are preserved.
* Added /return for the last successful Weaver departure point only. Regular portals do not replace it.
* Added /tp <player name> and live player destinations for Teleport to player and Bring player here.
* Player teleporting requires the existing teleport permission and respects combat travel rules.

Update the server and every client together. Keep both DLLs and preserve your existing config folder.

# 1.1.9

* Cleaner menus with rounded frames, clearer selection and collapsible settings.
* Searchable world objects and compact kit editing with icons and quantities.
* Equal-sized nodes, graph navigation, group selection, minimap and clickable errors.
* Visible save status and local draft recovery. Optional server draft autosave.
* NPC appearance previews, smoother patrols and clearer player kits, travel and cooldowns.
* Configurable server rules, kit limits and storage cleanup with backups.

Update the server and every client together.


