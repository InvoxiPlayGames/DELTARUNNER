# DELTARUNNER

A custom version of the GMS LTS runner for running DELTARUNE on Linux natively.

This was made for personal usage, support will **not** be provided. You are *much* better off playing the Windows version of the game under Proton.

**This project is UNOFFICIAL. This software is NOT affiliated with nor endorsed by Toby Fox, Fangamer, 8-4 Ltd, YoYo Games or Opera Norway AS.**

(although I would be very willing to help any of these people out if native Linux is in the cards...)

## Features

* Implemented game_change for chapter switching.
* Reading game files out of the executable directory, rather than `assets/`.
* Saving savegames to the home folder ($HOME/.config/DELTARUNE).

## Usage

You need to own [DELTARUNE](https://store.steampowered.com/app/1671210/DELTARUNE/) on Steam, or its free demo.

1. Download DELTARUNE on Steam.
    * For the free demo, switch to the `chapter1.2.lts.test` branch.
2. Extract the `deltaRunner` binary into your DELTARUNE game files.
3. Run `chmod +x deltaRunner` to make the binary executable.
4. Launch the deltaRunner binary via the Steam Linux Runtime 1.0 (scout).
    * `~/.local/share/Steam/ubuntu12_32/steam-runtime/run.sh ./deltaRunner`
    * or `~/.local/share/Steam/steamapps/common/SteamLinuxRuntime/run-in-scout-on-soldier ./deltaRunner`

*(Launching individual chapters can be done; e.g. `./deltaRunner -gamedir chapter4_windows`)*

### arm64

1. Download DELTARUNE on Steam on another computer and copy the files over.
2. Extract the `deltaRunner_arm64` binary and provided .so files into your DELTARUNE game files.
3. Run `chmod +x deltaRunner_arm64` to make the binary executable
4. Launch the deltaRunner binary.
    * e.g. `./deltaRunner_arm64`

This should work on most modern arm64 GNU/Linux distros, including Debian 12 (untested), Fedora 42, and the Steam Linux Runtime 3.0 (sniper).

## Known Issues

**With DELTARUNNER** - these issues only affect DELTARUNNER or the game when running under it:

* Audio files with capitalised filenames do not play. A temporary fix is to rename all of these to lowercase in "mus" and the chapter folders.
    * Droning sound effect in Chapter 1. (`AUDIO_DRONE.ogg`)
    * "ANOTHER HIM" at the start of Chapter 1. (`AUDIO_ANOTHERHIM.ogg`)
    * "Darkness Falls" when you give up in Chapter 1. (`AUDIO_DARKNESS.ogg`)
    * "Faint Courage" when you run out of HP in the later chapters. (`AUDIO_DEFEAT.ogg`)
    * "DELTARUNE" logo sound effect. (`AUDIO_INTRONOISE.ogg`)
    * "Before The Story" music in SAVE Select. (`AUDIO_STORY.ogg`)
    * GALLERY. (`GALLERY.ogg`)
    * THE HOLY. (`THE_HOLY.ogg`)
    * KEYGEN. (`KEYGEN.ogg`)
    * "Quiz" during the games. (`TV_GAME.ogg`)
* game_change does not properly preserve window position (offset by window border size).

**With GMS LTS** - these issues affect all games using GMS's native Linux runner:

* libavcodec.so.58 is required for video playback- steamrt1 comes with an older version, and many distros are on newer versions. This can cause a softlock/crash on DELTARUNE Chapter 3's introduction cutscene.
* Controller input is slightly broken and doesn't work with many gamepads.
* (x86_64) Requires launching under Steam Linux Runtime 1.0 (scout) or an older distro.

Nitpicks:

* Savegames save to $HOME/.config rather than $XDG_CONFIG_HOME.
* Runs under XWayland when the user is using Wayland.
* Does not scale to HiDPI displays.
