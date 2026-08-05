# Music Setup Guide

Frostline Racing can play music during a race. Free and simple Premium arenas can have one race song. Premium can also use Advanced Music phase playlists.

You can use either:

- An `.nbs` file, which is a Note Block Studio song.
- A custom resource-pack sound key, which plays an `.ogg` sound from a Minecraft resource pack.

Simple music starts when the race begins and stops when the race ends. Premium Advanced Music can select one configured track when lobby, countdown, race, final-lap, or results playback begins.

Continuous playlist chaining, fades, crossfades, and deeper per-player preferences are not part of the first Advanced Music pass.

## Player Controls

Players can turn Frostline music on or off for themselves:

```text
/frostline music on
/frostline music off
```

This only affects that player.

## Admin Preview

Admins can preview the music before starting a race:

```text
/frostline admin previewmusic <arena>
```

By default, previews play for 15 seconds. You can change that in `plugins/FrostlineRacing/config.yml`:

```yaml
music:
  preview-seconds: 15
```

After changing config values, run:

```text
/frostline admin reload
```

## Option 1: Use an NBS File

This is usually the easiest option.

1. Start the server once with the plugin installed.
2. Find this folder:

```text
plugins/FrostlineRacing/music
```

3. Put your `.nbs` file in that folder.

Example:

```text
plugins/FrostlineRacing/music/sandy_desert.nbs
```

4. Set the arena music:

```text
/frostline admin setmusic sandy_desert nbs sandy_desert.nbs
```

The `.nbs` file extension matters. Use the full filename, including `.nbs`.

You can also set volume and pitch:

```text
/frostline admin setmusic sandy_desert nbs sandy_desert.nbs 0.8 1.0
```

Volume must be between `0.0` and `1.0`.

Pitch must be between `0.1` and `2.0`.

## Option 2: Use a Resource-Pack Sound

Use this option if you already have a server resource pack, or if you want to play a normal music file.

Minecraft resource-pack sounds must be `.ogg` files.

Example resource pack layout:

```text
FrostlineTestPack/
  pack.mcmeta
  assets/
    frostline/
      sounds.json
      sounds/
        music/
          sandy_desert.ogg
```

Example `sounds.json`:

```json
{
  "music.sandy_desert": {
    "sounds": [
      {
        "name": "frostline:music/sandy_desert",
        "stream": true
      }
    ]
  }
}
```

The sound key for that example is:

```text
frostline:music.sandy_desert
```

Set the arena music with:

```text
/frostline admin setmusic sandy_desert resource-pack frostline:music.sandy_desert
```

With volume and pitch:

```text
/frostline admin setmusic sandy_desert resource-pack frostline:music.sandy_desert 0.8 1.0
```

Players must have the resource pack enabled, or they will not hear resource-pack music.

## Turn Music Off For An Arena

To remove race music from an arena:

```text
/frostline admin setmusic sandy_desert off
```

## Premium Advanced Music

Premium builds support `music.advanced` in `arenas.yml`. A playlist is a track pool that selects one track when the phase begins; it does not continuously chain tracks.

Supported phases:

- `lobby`
- `countdown`
- `race`
- `final-lap`
- `results`

Supported strategies:

- `shuffle`
- `ordered`
- `weighted`

Example:

```yaml
music:
  enabled: true
  track:
    type: nbs
    file: sandy_desert.nbs
    volume: 0.8
    pitch: 1.0
  advanced:
    enabled: true
    defaults:
      strategy: shuffle
      volume: 0.8
      pitch: 1.0
    playlists:
      race:
        strategy: weighted
        tracks:
          - type: nbs
            file: sandy_desert.nbs
            weight: 2
          - type: resource-pack
            key: frostline:music.sandy_desert_alt
            volume: 0.7
            pitch: 1.0
      final-lap:
        strategy: ordered
        tracks:
          - type: resource-pack
            key: frostline:music.final_lap
```

Fallback order:

```text
phase-specific playlist
→ race playlist
→ legacy music.track
→ no music
```

The Premium setup GUI can show the loaded music summary and preview the same race-phase selection used by playback. Full inventory editing for advanced playlists is deferred.

## Config Settings

In `plugins/FrostlineRacing/config.yml`:

```yaml
music:
  enabled: true
  default-volume: 0.8
  preview-seconds: 15
```

`enabled` turns the whole music system on or off.

`default-volume` is used when an arena track does not have its own volume.

`preview-seconds` controls how long admin previews last.

## Troubleshooting

If preview says the song is playing but you hear nothing:

- Check your Minecraft "Jukebox/Note Blocks" volume slider.
- For NBS files, make sure the file is in `plugins/FrostlineRacing/music`.
- For NBS files, make sure the command includes `.nbs` at the end.
- For resource-pack sounds, make sure the resource pack is enabled on your client.
- For resource-pack sounds, make sure the sound key matches `sounds.json`.

If an NBS preview fails:

- Check the server log. The plugin should say if the file is missing or invalid.
- Try tab completion after `nbs` to see files the plugin can find:

```text
/frostline admin setmusic sandy_desert nbs <tab>
```

If resource-pack music does not play:

- Make sure the sound file is `.ogg`.
- Make sure `pack.mcmeta` is at the root of the zip.
- Make sure `sounds.json` is inside `assets/<namespace>/sounds.json`.
- Make sure the command uses the full sound key, like `frostline:music.sandy_desert`.
