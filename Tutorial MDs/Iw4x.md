# IW4x
![IW4x Banner](https://xlabs.dev/img/iw4x_banner.jpg "IW4x Banner")

Iw4x is a Call of Duty Modern Warfare 2 (2009) Client


| Fetures            | 
| -------------------|
| Additional Content |
| Improved Security  |
|Mods and Mod Tools  |
|Dedicated Servers   | 
|Anti-Cheat          |
|Support             |

## Links
* [Developers Website](https://xlabs.dev/)
* [GitHub Repo](https://github.com/XLabsProject/iw4x-client)
* [Torrent Download](https://dss0.cc/alterwarez/download/iw4x_full_game.torrent)
* [Download Site](https://xlabs.dev/support_iw4x_client#nonsteam)
* [Guide to installing on Linux](https://www.reddit.com/r/IW4x/comments/irdycg/can_you_play_iw4x_in_linux/?utm_medium=android_app&utm_source=share)



# README.md of the [IW4x-Github Repo](https://github.com/XLabsProject/iw4x-client/blob/develop/README.md)
![license](https://img.shields.io/github/license/IW4x/iw4x-client.svg)
![forks](https://img.shields.io/github/forks/IW4x/iw4x-client.svg)
![stars](https://img.shields.io/github/stars/IW4x/iw4x-client.svg)
![issues](https://img.shields.io/github/issues/IW4x/iw4x-client.svg)
[![build status](https://ci.appveyor.com/api/projects/status/rvljq0ooxen0oexm/branch/develop?svg=true)](https://ci.appveyor.com/project/iw4x/iw4x-client/branch/develop)
[![discord](https://img.shields.io/endpoint?url=https://momo5502.com/iw4x/members-badge.php)](https://discord.gg/sKeVmR3)
[![patreon](https://img.shields.io/badge/patreon-support-blue.svg?logo=patreon)](https://www.patreon.com/xlabsproject)

# IW4x: Client

## Commit message style

```
[Module] Imperative summary

- points or text

[ci skip]
```

`[ci skip]` is optional.

## How to compile

- Run `premake5 vs2019` or use the delivered `generate.bat`.
- Build via solution file in `build\iw4x.sln`. (You can use the `build.bat` script to do it quick and easy.)

## Premake arguments

| Argument                    | Description                                    |
|:----------------------------|:-----------------------------------------------|
| `--copy-to=PATH`            | Optional, copy the DLL to a custom folder after build, define the path here if wanted. |
| `--copy-pdb`                | Copy debug information for binaries as well to the path given via --copy-to. |
| `--ac-disable`              | Disable anticheat.                             |
| `--ac-debug-detections`     | Log anticheat detections.                      |
| `--ac-debug-load-library`   | Log libraries that get loaded.                 |
| `--force-unit-tests`        | Always compile unit tests.                     |
| `--force-exception-handler` | Install custom unhandled exception handler even for Debug builds. |
| `--force-minidump-upload`   | Upload minidumps even for Debug builds.        |
| `--disable-bitmessage`      | Disable use of BitMessage completely.          |
| `--disable-base128`         | Disable base128 encoding for minidumps.        |
| `--no-new-structure`        | Do not use new virtual path structure (separating headers and source files). |

## Disclaimer

This software has been created purely for the purposes of
academic research. It is not intended to be used to attack
other systems. Project maintainers are not responsible or
liable for misuse of the software. Use responsibly.