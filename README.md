
# Uplink Theme Manager

This tool assumes that Uplink has been installed using Steam.

## Installation

To install this tool, simply clone this repository, navigate to the folder, and run the below command.

    ln -s $(pwd)/upth /usr/local/bin/upth

This will symlink the `upth` file into your `PATH`, making it available on the commandline.
Then proceed as below.

If the file for some reason is not executable, try running `chmod +x upth`.

## Commands/Usage

### Install

    upth install <path>

Installs the theme at `path`.
If a theme is already installed, this command does nothing.

### Restore

    upth restore

Restores the default theme for Uplink, deleting any theme that might be installed.

### Replace

    upth replace <path>

Replaces the current theme with the theme at `path`.
If no theme is installed (the default doesn't count), this command does nothing.

## What is going on behind the scenes?

### About themes

The way theming works in Uplink (at least, the Steam version) is that when loading the theme,
Uplink first looks for a `graphics` folder in its install directory.
If one is not found, Uplink defaults to the graphics in file `graphics.dat` in the same directory.

To install a theme, one has to copy the theme files into the `graphics` folder, creating it if it doesn't exist.
In doing so, Uplink will use these files instead of the ones from `graphics.dat`.

To make modding (and theming) easier, the game has created a folder where mods can be installed into.
Unfortunately, it doesn't seem like the game even acknowledges these folders.
So they must be symlinked into a location the game *will* acknowledge.

The locations are as follows:

1. `~/Library/Application Support/Uplink/mods`
2. `~/Library/Application Support/Steam/steamapps/common/Uplink/Uplink.app/Content/Resources`

where location #1 is the mods folder and location #2 is the location it must be symlinked to.

### What this tool does

First, the tool will check that symlinks exist, creating them if they don't.
Then, depending on the command invoked, one of two actions take place.

Invoking `install`, will copy the files at `path` into location #1.
Along with copying `theme.txt` this will make Uplink use the new theme instead of the default one.

Invoking `restore`, the tool will delete theme files at location #1, making Uplink fall back to the default theme files.
The files deleted are according to a list of filenames, that make up the default theme.
For the curious ones, the list is located in `paths.txt`.

Invoking `replace` consists of first calling `restore` and then `install`.
