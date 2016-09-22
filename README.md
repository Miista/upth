
# Uplink Theme Manager

This tool assumes that Uplink has been installed using Steam.

## Commands/Usage

### Install

    upth install <path>

Installs the theme at `path`.

### Restore

    upth restore

Restores the default theme for Uplink.

### Replace

    upth replace <path>

Replaces the current theme with the theme at `path`.

## What is going on behind the scenes?

The way theming works in Uplink (at least, the Steam version) is as follows:
the game looks in one of two locations for the file `theme.txt`.

1. `~/Library/Application Support/Uplink/mods`
2. `~/Library/Application Support/Steam/steamapps/common/Uplink/Uplink.app/Content/Resources/graphics`

If `theme.txt` is found in the location #1, the game uses the graphics in that folder.
If not, the game defaults to the graphics in location #2.
What this tool does when invoking `install` is to copy the theme files at `path` into location #1, making Uplink use these files first.
When calling `restore`, the tool deletes theme files at location #1, so Uplink will fall back to the default theme files.
Invoking `replace` consists of first calling `restore` and then `install`.
