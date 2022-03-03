# VATSIM EuroScope and AfV on wine

This is a script that's meant to facilitate installing an ATC-environment for Linux users.

If everything goes well, it does not require any additional interaction.

As both the essential VATSIM ATC programs [EuroScope](https://www.euroscope.hu/) and
[Audio for VATSIM](https://audio.vatsim.net/) are Windows-only (why?!), this uses `wine` as emulation layer.

## Current recommendation

2022-02: Audio for VATSIM does currently not run in neither wine 6 nor 7. Installing EuroScope in wine works though and runs fine.

Recommendation: 

Use this script only to install EuroScope and its newest beta (see "Usage" below).

For audio use the Mac/Linux AfV client project [pierr3/VectorAudio](https://github.com/pierr3/VectorAudio).
This is in beta state but mostly usable. It needs people testing it. Please report problems with it on [pierr3/VectorAudio issues](https://github.com/pierr3/VectorAudio/issues).


## Remarks

It installs the newest EuroScope beta version. We could make that an option if users need a choice there.

`wine` integrates into your host's audio system and registers all application audio channels there. Thus, just select
the "default" audio device in the Windows applications and do the routing in your host.
See [Wine Sound](https://wiki.winehq.org/Sound) for more information.

## Requirements:

* `bash`, `unzip`, `grep`, `wget`
* `wine` and `winetricks`. Suggested (unsure if needed): Packaged `wine-gecko` and `wine-mono`
* There will be a warning if it misses something it needs.

## Usage:

```bash
# create a new directory for your wine environment and change into it
wineDir=$USER/VATSIM-ATC/wine
mkdir -p "$wineDir"
cd "$wineDir"

# download the installer script
wget https://raw.githubusercontent.com/jonaseberle/euroscope-afv-wine/main/euroscope-afv-wine_install.sh

# make executable
chmod +x euroscope-afv-wine_install.sh

# check its options
./euroscope-afv-wine_install.sh --help

# .. and execute it
# current recommendation: only install EuroScope, use VECTOR audio (https://github.com/pierr3/VectorAudio)
# for audio:
./euroscope-afv-wine_install.sh --euroscope

# it does some checks and asks you for confirmation before starting the installation
```

... expect around 15min until the installation is finished. If everything worked ok, you will be able to start EuroScope
and Audio for VATSIM via your usual applications menu.

You'll find your configured "Documents" directory (`xdg-user-dir DOCUMENTS`) labelled "Documents" in the Windows file
browsers, too. This can be adjusted with `winecfg`. EuroScope expects its settings files at `"Documents"/EuroScope`.

## Tested with:

* wine 7.0-rc5
* wine 6
* Manjaro, Ubuntu 20.4
* please report your successes/failures with other environments

## Known issues:

* Audio for VATSIM sometimes starts fine, then on another day it might not start any more. It probably has something to
  do with its internal updater.
* EuroScope hangs on quitting, after saving changed settings.
  ([WineHQ AppDB entry](https://appdb.winehq.org/objectManager.php?sClass=version&iId=32239))
* [AFV_BRIDGE](https://github.com/AndyTWF/afv-euroscope-bridge) does not work. EuroScope
  message: `AFV_BRIDGE: Unable to open communication for AfV Bridge`.
* [VCH Plugin](https://github.com/DrFreas/VCH) outputs a message but seems to work fine. EuroScope
  message: `ERROR DATA: ERROR: Request didn't work`.

If you have any updates on these, please report. I would like to keep this list up-to-date.

## Suggestions:

Try updating `winetricks` if you experience problems with the "Installing libs…" step:

```bash
[sudo] winetricks --self-update
```

## Contact:

Contributions of any form are very welcome. You can approach me via the "discussions" or "issues" functions here
(prefered) or via my [VATSIM forums profile](https://forums.vatsim.net/profile/191848-jonas-eberle/).

## Thank you

This is built on top of the work of Samir Gebran https://forums.vatsim.net/topic/31019-euroscope-on-linux-howto/.

Thank you to the creators of EuroScope and Audio for VATSIM. I think both are very able and intelligent programs. Maybe
next time do something more portable.
