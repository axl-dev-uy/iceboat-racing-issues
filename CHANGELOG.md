# Changelog

All notable changes to Frostline Racing will be documented here.

## [Beta 0.2.0] - 2026-07-14

### Added

- Separate waiting countdown and start countdown settings for each arena
- New admin command to set the waiting countdown: `/iceboat admin setwaitingcountdown <arena> <seconds>`
- Admin commands to set arena minimum and maximum players independently
- Premium setup GUI controls for minimum players, maximum players, waiting countdown, and start countdown
- Config files now add missing default options automatically after updates, while keeping existing custom values
- Legacy color code support for messages, including hex colors
- Universal plus Linux, Windows, and macOS builds for both Free and Premium

### Changed

- Force starting a race now respects the waiting countdown instead of jumping straight into the race flow
- Arena setup edits no longer require disabling the arena first for normal changes
- Setup changes made while races are active are saved and applied after the race finishes
- Enable and disable command suggestions now show the correct arenas
- Start-line countdown wording is clearer in commands and the setup GUI

### Fixed

- Older arena configs missing countdown settings are filled in with safe defaults
- Missing message keys are restored from the latest bundled defaults
- SQLite license files are included in packaged jars

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
