# Calamity Cleaver

Auto-raid macro for **Jujutsu Zero** (Nayoa Calamity). It watches the screen for six images, replays the raid for you, and keeps a win counter. If you die it retries straight away.

## Quick start

1. Put `Calamity_Cleaver.bat` in its own folder.
2. Double-click it. If Python or a library is missing it installs it (needs internet). Once everything is installed, later launches skip this and nothing gets upgraded.
3. The settings window opens. Set your search areas (see **Grab**), pick your options, press **SAVE & LAUNCH**.
4. The macro starts. Keep Roblox visible and in focus.

The six PNG images are built into the `.bat` and get written next to it the first time it runs. Your settings are saved in `calamity_settings.json` and are pre-filled next time.

## Grab: setting the search areas

Every image is only searched inside its own rectangle, so smaller rectangles scan faster.

1. Put Roblox on screen.
2. Press **GRAB AREA** next to an image. The settings window minimises.
3. When the banner says **BOTTOM-LEFT**, hover that corner of where the image shows up and wait 3 seconds.
4. When it says **TOP-RIGHT**, hover that corner and wait 3 seconds.
5. The window comes back with all four numbers filled in.

The small **BL** and **TR** buttons grab just one corner. You can also type the numbers by hand.
The box must be bigger than the image itself, so leave a little room around it.

## What the macro does

| Image | Meaning | Action |
| --- | --- | --- |
| Ready | Raid is starting | Glides to it, clicks 3 times, then presses your slot(s): 1, 2, or 1 then 2 if both are picked |
| Lv. 13,000 Zen'in Elite | Raid started | Equips your slot and starts the attack rotation |
| Chase took too long... | Phase 2 | Logged, rotation keeps going |
| Raid Summary: Successful | Raid beaten | Loops +1, then looks for Retry |
| Raid Summary: Failure | You died | Loops unchanged, then looks for Retry |
| Retry | Only searched after a win or fail | Glides to it and clicks 5 times |

All images except Retry are scanned non-stop, every 0.05 seconds. All mouse movement is a curved, eased glide sent as real mouse input, with a short hover before each click so Roblox registers it. Scanning pauses for the second or two the mouse is moving and clicking, so it stays smooth.

## The raid counter

- **Loops** goes up by 1 every time *Raid Summary: Successful* is seen. A failure never counts.
- It is shown in the small stats window (always on top, top-right of the screen), in the console window title, and in the console on every win.
- **Time** starts when the macro launches and is shown next to it.
- The counter starts at 0 on every launch. It is not saved between runs.
- With **Loops: Amount** set, the macro stops by itself once it reaches that many wins. **Inf** runs until you stop it.

## Settings

- **Search areas**: one rectangle per image (bottom-left X/Y and top-right X/Y).
- **Attack rotation**: keys from `c f x r t v z y`, pressed in that order, over and over during a raid.
- **Slots**: slot 1, slot 2 or both. With one slot, the macro presses it when the raid starts. With both, it runs one full pass of the attack rotation on a slot, swaps to the other slot, runs another pass, and keeps alternating.
- **Heavenly restriction / Cursed technique / Weapon**: pick one restriction or none. Physical locks cursed techniques, Sorcerer locks weapons. Up to 2 selected per list. These are saved and shown in the console header, but they do not change what the macro presses.
- **Loops**: an amount, or Inf.
- **Stop key** (F1-F12): stops the macro; press it again to restart it. Loops and Time keep counting.
- **Log clearer**: the console is wiped and redrawn every 5 to 30 minutes.
- **Modifiers**: tick (✔) or cross (✖) for **Weaken** and **Hardcore**. Only used by auto rejoin when it creates the raid (see below). Defaults: Weaken on, Hardcore off.
- **Screen**: Half-Screen, Corner Screen or Full Screen. Smaller layouts also try smaller copies of the images, in case Roblox's UI shrinks.
- **Resolution**: display only. It does nothing.

## Tips and fixes

- **Nothing is detected**: check the search area covers where the image appears, and that it is bigger than the image. If the game looks different from the screenshots, replace the matching PNG next to the `.bat` with a fresh crop.
- **Scanning feels slow**: shrink the search areas with GRAB AREA. Large areas cost the most.
- **Keys or clicks do nothing**: run the `.bat` as administrator, and click into Roblox once so it has focus.
- **Close the stats window** (or press Ctrl+C in the console) to stop the macro completely.

## Auto rejoin (when the game kicks you)

Roblox kicks you out now and then. The **Disconnected** box (Leave / Reconnect) is searched for all the time. The moment it shows up, **every other image search stops** and the rejoin protocol runs:

1. Click **Leave** (the left button of the box). Then, before anything else, look for the big blue **Play** button for up to 15 seconds:
   - **Play found**: click it **5 times**, then skip straight to step 4 (**Gamemodes**).
   - **Not found within 15 seconds**: click **Home** once (light mode or dark mode, both are searched), then carry on with step 2.
2. Look for the **Search** bar (light mode or dark mode, both are searched), click it once, press Ctrl+A, type the game name (default `Jujutsu: Zero`, changeable in settings) and press Enter
3. **Play** (big blue button) x3 -> **Gamemodes** x1 -> **Raids** x3 -> **Create** x3 -> **Projection** x3 -> **Calamity** x3
4. **Modifiers** x1 -> **Weaken** x1 -> **Hardcore** x1 -> **Friends Only** -> **Create** x3 -> **Start** x5
   - Only the modifiers ticked under **MODIFIERS** are selected (Weaken first, then Hardcore, in the same step).
   - If neither is ticked, the Modifiers button is not clicked at all and it goes straight to **Friends Only**.
   - The step count in the stats window adjusts (`REJOINING step N/13`, `/14` with both, `/11` with none).

It runs strictly in order, step 1 to 13 (when Play is found in step 1 it jumps ahead and the Gamemodes step is where the order picks up again). Each step only searches for its own image, glides the mouse to it, clicks, then waits for that button to leave the screen before the next step starts, so the two Create buttons can never be mixed up (Create is only searched at step 6 and step 12, and a hit is ignored if the other Create fits better at the same spot). The stats window shows `REJOINING step N/13`. If the Disconnected box is still there or comes back, it goes back to step 1. When Start has been clicked the normal macro carries on until the next kick.

- Every rejoin button has its own search area with the same X/Y boxes and **GRAB AREA / BL / TR** buttons (inside the **AUTO REJOIN** card). **Fullscreen scan** overrides all of them.
- **Light and dark mode**: Home, Search and Play each come in more than one look (`Rejoin_Home.png` + `Rejoin_HomeDark.png`, `Rejoin_Search.png` + `Rejoin_SearchDark.png`, `Rejoin_Play.png` + `Rejoin_Play2.png`). Both looks are searched at the same time inside the **same** box, and whichever fits better is clicked, so each button still has just one row of numbers. The log says which look was used, e.g. `Rejoin: Home (dark mode)`.
- The Play button is also checked for its blue colour, so a bright icon on a dark page (like the Home icon) can never be mistaken for it.
- The new `Rejoin_*.png` files are written next to the `.bat` the first time it runs if they are missing. To change one, replace that PNG with a fresh crop.
- The Disconnected box is scanned non-stop, so give it a small search area for the best speed.
- The stats window shows `REJOINING` while it runs and counts the rejoins.
- If a step image is not found, the log warns every 60 seconds. Click it yourself and the protocol carries on from there. The stop key aborts it.
- The 15 second Play check in step 1 has no warnings or screenshots of its own, because not finding Play there is normal and just means "go via Home".
- Switch it off with **Auto rejoin: Off**.

## Slots: key or click

Under **SLOTS**, **How to equip a slot** can be **Press key** (presses 1 / 2) or **Click position**. With Click position you set an X/Y for slot 1 and slot 2 (**GRAB POINT**, then hover the slot for 3 seconds) and the mouse glides there and clicks it once. With a middle-mouse Lock On, the mouse glides back to where Ready was before it locks on.

## The log file (if something bugs)

Every run writes `logs\session_<date>_<time>.log` (the last 10 are kept). It has your settings, every action with a time stamp, a heartbeat line every 30 seconds, and full error details if anything crashes. **Send me that file** when something goes wrong.

- **Frozen scanner or stuck mouse action:** a WARN is printed and a thread dump (what every part of the macro is doing) is written to the log.
- **Rejoin step stuck for 20 seconds:** the log gets the best match score for that image (and its rival, and the Disconnected box) next to the score it needs, and `logs\stuck_stepNN_area.png` (what the search box sees) plus `logs\stuck_stepNN_screen.png` (the whole screen) are saved. Send those too.
