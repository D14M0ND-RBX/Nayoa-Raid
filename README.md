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
| Ready | Raid is starting | Glides to it and clicks 3 times |
| Lv. 13,000 Zen'in Elite | Raid started | Starts the attack rotation |
| Chase took too long... | Phase 2 | Logged, rotation keeps going |
| Raid Summary: Successful | Raid beaten | Loops +1, then looks for Retry |
| Raid Summary: Failure | You died | Loops unchanged, then looks for Retry |
| Retry | Only searched after a win or fail | Glides to it and clicks 5 times |

All images except Retry are scanned non-stop, every 0.05 seconds. All mouse movement is a curved, eased glide.

## The raid counter

- **Loops** goes up by 1 every time *Raid Summary: Successful* is seen. A failure never counts.
- It is shown in the small stats window (always on top, top-right of the screen), in the console window title, and in the console on every win.
- **Time** starts when the macro launches and is shown next to it.
- The counter starts at 0 on every launch. It is not saved between runs.
- With **Loops: Amount** set, the macro stops by itself once it reaches that many wins. **Inf** runs until you stop it.

## Settings

- **Search areas**: one rectangle per image (bottom-left X/Y and top-right X/Y).
- **Attack rotation**: keys from `c f x r t v z y`, pressed in that order, over and over during a raid.
- **Heavenly restriction / Cursed technique / Weapon**: pick one restriction or none. Physical locks cursed techniques, Sorcerer locks weapons. Up to 2 selected per list. These are saved and shown in the console header, but they do not change what the macro presses.
- **Loops**: an amount, or Inf.
- **Stop key** (F1-F12): stops the macro; press it again to restart it. Loops and Time keep counting.
- **Log clearer**: the console is wiped and redrawn every 5 to 30 minutes.
- **Screen**: Half-Screen, Corner Screen or Full Screen. Smaller layouts also try smaller copies of the images, in case Roblox's UI shrinks.
- **Resolution**: display only. It does nothing.

## Tips and fixes

- **Nothing is detected**: check the search area covers where the image appears, and that it is bigger than the image. If the game looks different from the screenshots, replace the matching PNG next to the `.bat` with a fresh crop.
- **Scanning feels slow**: shrink the search areas with GRAB AREA. Large areas cost the most.
- **Keys or clicks do nothing**: run the `.bat` as administrator, and click into Roblox once so it has focus.
- **Close the stats window** (or press Ctrl+C in the console) to stop the macro completely.
