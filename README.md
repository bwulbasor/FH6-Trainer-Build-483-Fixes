# FH6 Trainer — experimental weather and seasons

This is an independent copy of [changcheng967's FH6 All-in-One Trainer](https://github.com/changcheng967/FH6-AllInOne-Trainer), with experimental changes for a particular Windows PC build. Credit for the original trainer belongs to its authors and contributors. This copy is based on trainer source version **8.7.0** and remains licensed under [GPL-3.0](LICENSE).

## Compatibility and status

The new paths were developed against **Forza Horizon 6 executable version 6.483.970.0, build 26422872**, on Windows PC. They are experimental and should not be assumed to work on other versions. Use offline free roam. The existing project contains other cheats and legacy mechanisms; their behavior is not covered by the results below.

The original trainer attached to this game but reported a successfully installed rain getter hook without capturing a weather entity. Season detection also failed. On this build, the new weather path resolves the live weather manager through a verified code signature and pointer chain instead of waiting for that getter to capture an entity. Season switching uses a build-checked game function dispatched on the game's own update thread. The weather script and clock are coordinated to hold time without the flickering seen in an earlier test. Attachment now retries and ignores windowless helper processes.

| Control | Observed result |
| --- | --- |
| Winter | User confirmed winter scenery in free roam. All four season selections were observed in game state; the other seasons' visuals were not individually verified. |
| Night | User confirmed stable night in free roam and from the packaged trainer. |
| Day and early morning | Buttons available; the latest early-morning visual result was not separately confirmed. |
| Evening | Available, but the user reported it still looked like night after adjustment to 16:30. |
| Precipitation | User confirmed steady snow in winter. The maximum setting produced snow but was not visibly heavier in that test. |
| Wind and storm intensity | Controls available; maximum wind produced some wind, not a confirmed gale. The new one-click storm preset has not been visually verified. |
| Fog | **Not implemented.** A named fog sky and a possible selection path were investigated, but visible fog was not verified. |

## Use and build

Start the game, enter offline free roam, and launch the trainer. It attempts to attach automatically. On the Unlocks page, use the experimental season, weather, and time-of-day controls. The time control holds the weather script; Restore returns its previous time state. Precipitation appears as snow under the tested winter conditions.

To build on Windows with the .NET 10 SDK:

```powershell
dotnet restore FH6Mod.csproj -r win-x64
dotnet publish FH6Mod.csproj -c Release -r win-x64 --self-contained true -o publish
```

The self-contained executable is `publish/FH6AllInOneTrainer.exe`. Source is provided; this repository does not claim an official upstream release.

## Adapting to a different game version

See [Compatibility investigation](docs/COMPATIBILITY.md) for a practical checklist for maintainers and AI agents. Do not copy offsets or signatures from this build to a different executable without verifying them. Keep unsupported builds from using the build-specific path, and distinguish a successful attachment or hook installation from a visually verified result.

The original project includes legacy code for other features, including integrity-related behavior; the build-specific season, weather, and clock work described here does not require disabling security protections or bypassing DRM or anti-cheat. Do not use these instructions to do so.
