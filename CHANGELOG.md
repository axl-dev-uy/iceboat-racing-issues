# Changelog

All notable changes to Frostline Racing will be documented here.

## [Beta 0.3.1] - 2026-07-24

### Changed
- Paper compatibility baseline is now 1.21.6, with the 0.3.1 jar intended for Paper 1.21.6 and newer builds, including 26.x; use Java 21 on pre-26.1 builds and Java 25 on 26.1+

## [Beta 0.3.0] - 2026-07-16

### Added

- Premium setup GUI controls for minimum players, maximum players, ranked mode, waiting countdown, and start countdown
- Optional PlaceholderAPI expansion for Premium and future Partner builds
- Generic Partner edition architecture for future custom builds without an active named Partner artifact
- Premium Ranked Foundation with casual/ranked arena modes, browser mode selection, ranked joins, Elo-style ratings, ranked stats, and ranked leaderboards
- Ranked arena configuration through `allowed-modes` and per-arena `ranked.minimum-players`
- Ranked setup command: `/iceboat admin setranked <arena> <enabled|disabled>`
- Ranked commands: `/iceboat join <arena> ranked`, `/iceboat join random ranked`, `/iceboat quickjoin [player] ranked`, `/iceboat rank [player]`, `/iceboat rankedtop [page]`, and `/iceboat admin ranked setrating <player> <rating> --confirm`
- Admin diagnostics command: `/iceboat admin about` for Frostline Racing support reports, with platform build metadata, generated timestamp, feature gates, active hooks, SQLite storage details, and an in-chat copy button
- Ranked PlaceholderAPI values for rating, races, wins, finishes, and DNFs when both PlaceholderAPI and Ranked are available
- Admin stats JSON export/import commands for backups and migrations

### Changed

- Paper compatibility baseline is now 26.1, with the 0.3 jar intended for Paper 26.1 through 26.2 on Java 25
- Start-line countdown wording is clearer in commands and the setup GUI
- Premium jars now package the Ranked feature module, while Free jars exclude ranked implementation classes and service metadata
- Final artifacts now include generated build metadata for platform, artifact name, and build timestamp
- Artifact validation now covers generated build metadata and active Free/Premium universal and OS-specific artifacts
- Legacy arenas missing ranked mode defaults are migrated to casual-only with `ranked.minimum-players: 2`

### Fixed

- Fixed obfuscated ranked arena mode loading so `/iceboat admin reload` handles `allowed-modes` safely
- Fixed obfuscated Premium startup issues affecting kept setup/ranked classes and optional feature loading

## [Beta 0.2.0] - 2026-07-14

### Added

- Separate waiting countdown and start countdown settings for each arena
- New admin command to set the waiting countdown: `/iceboat admin setwaitingcountdown <arena> <seconds>`
- Admin commands to set arena minimum and maximum players independently
- Config files now add missing default options automatically after updates, while keeping existing custom values
- Legacy color code support for messages, including hex colors

## [0.1-beta] - 2026-07-12

### Added

- Complete ice boat race lifecycle
- Ordered checkpoints and multiple laps
- Placement tracking, DNF handling, and race timeout
- Arena browser GUI and smart quick join
- Per-arena queues and queue management GUI
- Spectator mode and racer navigation
- Persistent SQLite statistics and leaderboards
- Configurable messages, sounds, bossbars, actionbars, and scoreboards
- In-game arena setup commands
- Optional WorldEdit integration
- Arena validation command
- Reconnect grace
- Configurable command rewards
- Linux, Windows, macOS, and Universal builds

### Notes

- This is the first public beta release.
- Wider multiplayer testing is still in progress.
- Windows and macOS builds have not been tested directly by the developer.
