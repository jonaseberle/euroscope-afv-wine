# VATSIM EuroScope and Audio for VATSIM on non-Windows

This is a script that's meant to facilitate installing an ATC-environment for Linux/Mac users.

If everything goes well, it does not require any additional interaction.

It uses *wine* for the Windows-only programs.

## Current recommendation

2022-02: Audio for VATSIM does currently not run with `wine`. Installing EuroScope in `wine` works though and runs fine.
But we don't need Audio for VATSIM any more because there is now a project that aims to provide a native client for all platforms:. 

Recommendation: 

Use this script only to install EuroScope (see "Usage" below).

For audio use the Mac/Linux AfV client project [pierr3/TrackAudio](https://github.com/pierr3/TrackAudio) (successor of [pierr3/VectorAudio](https://github.com/pierr3/VectorAudio)).

2023-05 We now have an RDF plugin for TrackAudio, too! The well known RDFPlugin by @chembergj has been extended in a [fork by @KingfuChan](https://github.com/KingfuChan/RDF). You can find downloads under "[Releases](https://github.com/KingfuChan/RDF/releases)".

## Requirements:

* On Mac, please install GNU `getopt`, for example via `brew install gnu-getopt`. Thanks to @daan33 for providing that solution.
* `bash`, `unzip`, `grep`, `wget`
* `wine` and `winetricks`. Suggested (unsure if needed): Packaged `wine-gecko` and `wine-mono`

## Usage:

```
# ./euroscope-afv-wine_install.sh --help
Usage: euroscope-afv-wine_install.sh [<options>]
  <options>:
        -h|--help       this help
        -a|--afv        install only afv
        -e|--euroscope  install only EuroScope
        -B|--no-euroscope-beta do not install EuroScope beta
        -y|--yes        no confirmations
        --cached        use cached versions of already downloaded files
        -v|--verbose    echo all script commands
```

### Quickstart

```bash
# create a new directory for your wine environment and change into it
wineDir=$USER/VATSIM-ATC/wine-install
mkdir -p "$wineDir" && cd "$wineDir"

# clone this repo
git clone https://github.com/jonaseberle/euroscope-afv-wine.git && cd euroscope-afv-wine

# make the installer script executable
chmod +x euroscope-afv-wine_install.sh

# switch into a directory where the wine environment will be created
mkdir -p wine && cd wine

# You'll now have a $USER/VATSIM-ATC/wine-install/euroscope-afv-wine/wine directory
# where we will setup the environment. This is called the "WINEPREFIX".

# check the script options
../euroscope-afv-wine_install.sh --help

# .. and install EuroScope with it
../euroscope-afv-wine_install.sh --euroscope --no-euroscope-beta
```

## Tested with:

* wine 6, 7.0-rc5, 7.5, 7.20, 7.22, 8.0-rc1, 8.0.1, 8.1
* Arch (Manjaro, EndeavourOS), Ubuntu (20.04, 23.04, 23.10), openSUSE Tumbleweed

Please report your successes/failures with these or other environments.

## Known issues:

* 2023-10: On Ubuntu 23.04, `winetricks` [would not run with `wine`](https://askubuntu.com/questions/1468904/winetricks-ubuntu-23-04-wont-launch) – use `wine-development` (`sudo apt install wine-development`)
* Audio for VATSIM sometimes starts fine, then on another day it might not start any more. It probably has something to
  do with its internal updater. Recommendation: Do not install AfV.
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
Don't do this on Debian/Ubuntu/... though. The packaged `winetricks` 
[contains a patch](https://github.com/Winetricks/winetricks/issues/2119#issuecomment-1793812033) 
that is important in those environments for working with win64.

## Contact:

Contributions of any form are very welcome. You can approach me via the "discussions" or "issues" functions here
(prefered) or via my [VATSIM forums profile](https://forums.vatsim.net/profile/191848-jonas-eberle/).

## Thank you

This is built on top of the work of Samir Gebran https://forums.vatsim.net/topic/31019-euroscope-on-linux-howto/.


Thank you to the creators of the [EuroScope](https://www.euroscope.hu/) and 
[Audio for VATSIM](https://audio.vatsim.net/) programs. 
It is a pity that they are not available cross-platform natively.
