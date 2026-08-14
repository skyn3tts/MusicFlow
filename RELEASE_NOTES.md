# MusicFlow 0.1.2

MusicFlow is a native 64-bit Windows music-library player focused on local files, classic Cover Flow, and a compact neutral Liquid Glass interface.

## Highlights

- Responsive multi-album Cover Flow with mouse, trackpad, keyboard, click-to-center, and snapping navigation.
- Native file and folder import for MP3, FLAC, WAV, OGG, M4A, and AAC libraries.
- Persistent Favourite Songs, playlists, queue, listening history, artwork overrides, and settings.
- Three local, date-stable Daily Mixes generated without an internet connection.
- Dense Songs, Albums, Artists, Recently Played, playlist, and queue views.
- Previous, play/pause, next, shuffle, repeat, queue, seek, and popover volume controls.
- Album-consistent artwork resolution with song-specific override support.

## System requirements

- Windows 10 or Windows 11, 64-bit.
- A working Windows audio output device.
- No internet connection or separate Qt installation is required.

## Downloads

- `MusicFlow-0.1.0-win64-setup.exe`: recommended Windows installer.
- `MusicFlow-0.1.0-win64-portable.zip`: portable build; extract the entire folder before running `MusicFlow.exe`.
- `MusicFlow-0.1.0-SHA256SUMS.txt`: SHA-256 checksums for release verification.

## Notes

- MusicFlow never modifies or deletes imported audio files.
- Application data is stored in the current user's Local AppData directory.
- Codec playback support depends on the bundled audio decoder. If a particular AAC/M4A file does not play, test a WAV, MP3, or FLAC file to verify the audio path.
- These artifacts are unsigned. Windows SmartScreen may show an “Unknown publisher” warning until the release is Authenticode-signed.
