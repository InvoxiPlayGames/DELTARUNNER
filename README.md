# DELTARUNNER

A custom version of the GMS LTS runner for running DELTARUNE on Linux natively.

This was made for personal usage, support will **not** be provided. You are *much* better off playing the Windows version of the game under Proton.

**This project is UNOFFICIAL. This software is NOT affiliated with nor endorsed by Toby Fox, Fangamer, 8-4 Ltd, YoYo Games or Opera Norway AS.**

(although I would be very willing to help any of these people out if native Linux is in the cards...)

## "Features"

* Implemented game_change for chapter switching.
* Reading game files out of the executable directory, rather than `assets/`.
* Saving savegames to the home folder ($HOME/.config/DELTARUNE).
* Automatic handling of uppercase audio file paths.

### Bugfixes

* Fixed video support on modern Linux distros (backported from GMS Beta).
* Fixed the game becoming blurry after playing a video on older versions of the game.

## Usage

You need to own [DELTARUNE](https://store.steampowered.com/app/1671210/DELTARUNE/) on Steam, or the [Chapter 1&2 free demo](https://store.steampowered.com/app/1671210/DELTARUNE/).

1. Download DELTARUNE on Steam.
    * For the Chapter 1&2 demo on Steam, switch to the `chapter1.2.lts.test` branch.
    * You can also download the files for the Chapter 1&2 DEMO from [itch.io](https://tobyfox.itch.io/deltarune).
2. Extract the `deltaRunner` binary into your DELTARUNE game files.
3. Run `chmod +x deltaRunner` to make the binary executable.
4. Launch the deltaRunner binary via Steam's "Legacy Runtime 1.0 (scout)".
    * `~/.local/share/Steam/ubuntu12_32/steam-runtime/run.sh ./deltaRunner`

*(Launching individual chapters can be done; e.g. `./deltaRunner -gamedir chapter4_windows launcher`)*

### Video Playback

Video playback (for DELTARUNE Chapter 3) requires ffmpeg/libavcodec installed.

* **Debian 12+, Ubuntu 22.04+:** `sudo apt install ffmpeg`
* **Fedora 41+:** `sudo dnf install ffmpeg`
* **Arch Linux:** `sudo pacman -S ffmpeg`
* **SteamOS:** TODO

### arm64

1. Download DELTARUNE on Steam on another computer and copy the files over.
    * You can also download the files for the Chapter 1&2 DEMO from [itch.io](https://tobyfox.itch.io/deltarune).
2. Extract the `deltaRunner_arm64` binary and provided .so files into your DELTARUNE game files.
3. Run `chmod +x deltaRunner_arm64` to make the binary executable
4. Launch the deltaRunner binary.
    * e.g. `./deltaRunner_arm64`

This should work on most modern arm64 GNU/Linux distros, including Debian 12 (untested), Fedora 42, and the Steam Linux Runtime 3.0 (sniper).

## Known Issues

**With DELTARUNNER** - these issues only affect DELTARUNNER or the game when running under it:

* game_change does not properly preserve window position (offset by window border size).

**With GMS LTS** - these issues affect all games using GMS's native Linux runner:

* (x86_64) Requires launching under Steam Linux Runtime 1.0 (scout) or an older distro.

Nitpicks:

* Controller input is slightly broken.
* Savegames save to $HOME/.config rather than $XDG_CONFIG_HOME.
* Runs under XWayland when the user is using Wayland.
* Does not scale to HiDPI displays.
