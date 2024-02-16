# Xenia Canary Game Patches
This repository contains game patches for [Xenia Canary](../../../../xenia-canary).

**Non-patch questions belong on the [Xenia Discord server](https://discord.gg/Q9mxZf9).**

[![Game Patches Discord](https://img.shields.io/discord/930763773109735484?color=5865F2&label=Game%20Patches%20Discord&logo=discord&logoColor=white)](https://discord.gg/fyRWq3xYNz)

### These are NOT actual games or Title Updates!<br>Read Xenia's [Quickstart](https://github.com/xenia-canary/xenia-canary/wiki/Quickstart) to get games.

## Installing/Updating
0. Prerequisites
    * [Latest Xenia Canary experimental](https://github.com/xenia-canary/xenia-canary/releases/download/experimental/xenia_canary.zip).
        * Patches aren't supported on master or outdated versions of Xenia Canary.
1. Download [this zip](../../../releases/latest/download/game-patches.zip).
2. Go to where `xenia_canary.exe` is.
3. Delete `patches` folder if present (backup if needed).
4. Open `game-patches.zip` and extract `patches` in the same directory as `xenia_canary.exe`.
    The folder structure should look like this:
<br>![](./README/patch_location.png)
    ```
    └─── Xenia Canary
        |  ...
        │  xenia_canary.exe
        |  ...
        └─── patches
                ...
                584111F7 - Minecraft (XBLA, TU0).patch.toml
                ...
    ```
5. Continue to the section below.

## How to use
0. Prerequisites
    * [Latest Xenia Canary experimental](https://github.com/xenia-canary/xenia-canary/releases/download/experimental/xenia_canary.zip)
        * Patches aren't supported on master or outdated versions of Xenia Canary.
    * The right version of the game e.g. Title Update (TU).
    <!--
        * Try commenting out the `hash` of the patch like so:
            ```toml
            # Add # before hash
            hash = "################"
            # like this
            #hash = "################"
            ```
            **This isn't guaranteed to work, and may cause crashes.**
            <br>Hashes are used to verify the correct version of a game is being patched, and this bypasses it.
            <br><br>If the game has multiple modules you will need to [get the hash(es)](#How-to-get-the-module-hash-and-filename)
    -->
    * `apply_patches` set to `true` (default) in the [Xenia Canary config](https://github.com/xenia-canary/xenia-canary/wiki/Options#canary).
1. Open the .patch.toml file that corresponds to your game in a text editor (Notepad, [VSCode](https://code.visualstudio.com/), [VSCodium](https://vscodium.com/), [Notepad++](https://notepad-plus-plus.org/), etc.)
2. Change `is_enabled` from `false` to `true`. For example, to enable a 60 FPS patch:
    ```toml
    [[patch]]
        name = "60 FPS"
        desc = "Description"
        author = "Author"
        is_enabled = false

        [[patch.be8]]
            address = 0x########
            value = 0x##
    ```
    becomes
    ```toml
    [[patch]]
        name = "60 FPS"
        desc = "Description"
        author = "Author"
        is_enabled = true

        [[patch.be8]]
            address = 0x########
            value = 0x##
    ```

If you see `[Patches Applied]` in the title bar then the patch(es) applied successfully.

***Don't change the hash of existing patches. If your version of the game is different then the patch(es) need to be ported to that version.***

#### Notes about aspect ratio patches
* [**`present_letterbox` must be changed from `true` to `false`!**](https://github.com/xenia-canary/xenia-canary/wiki/Options#black-bars-letterboxingpillarboxing)
* Aspect ratio patches **do not** increase resolution!
* While most aspect ratio patches are 21:9 (3440/1440), they can be changed to other aspect ratios as well unless not specified or specified otherwise;
    1. Divide your monitor's resolution width by height (i.e. 3440/1440)
    2. [Convert the result to hex](https://gregstoll.com/~gregstoll/floattohex).
    3. Change the value to `0x########` replacing `########` with the hex value.

#### Note about framerate patches
Framerates above 60 FPS require [vsync to be changed from true to false in the Xenia Canary config](https://github.com/xenia-canary/xenia-canary/wiki/Options#user-content-Vsync).

---

## Creating a patch
See [wiki page](https://github.com/xenia-canary/game-patches/wiki/Creating-Patches).
