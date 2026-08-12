

MusicFlow turns a folder of audio files into a fast, private desktop library. It combines a compact player, classic Cover Flow, playlists, favourites, listening history, and locally generated Daily Mixes without requiring an account or an internet connection.

> [!IMPORTANT]
> MusicFlow never modifies or deletes imported audio files. Library edits and artwork overrides are stored in MusicFlow's own local database.

## Contents

- [Features](#features)
- [Download](#download)
- [Install MusicFlow](#install-musicflow)
- [First run](#first-run)
- [Supported audio files](#supported-audio-files)
- [Data, privacy, and updates](#data-privacy-and-updates)
- [Troubleshooting](#troubleshooting)
- [Error and exit codes](#error-and-exit-codes)
- [Build from source](#build-from-source)
- [Create a release package](#create-a-release-package)

## Features

### Listen

- Play, pause, seek, skip, shuffle, and change volume from the compact player.
- Cycle repeat between Off, Repeat Once, and Repeat Continuously.
- Build and reorder a persistent queue that survives application restarts.
- Review recently played tracks and continue where you left off.

### Organize

- Import individual files, multiple files, or complete folders recursively.
- Read titles, artists, albums, artwork, duration, bitrate, and other metadata with TagLib.
- Search songs, albums, artists, and playlists from one place.
- Create playlists, add descriptions and custom artwork, and reorder or remove tracks.
- Mark favourite songs and generate three date-stable Daily Mixes locally.

### Explore

- Browse a responsive Cover Flow interface with mouse, keyboard, and trackpad navigation.
- Switch between Songs, Albums, Artists, Playlists, Favourites, Daily Mixes, and Recently Played.
- Use compact classic library views for information-dense browsing.
- Apply song, album, artist, playlist, and Cover Flow artwork overrides.

### Personalize

- Choose neutral appearance, glass intensity, accent, darkness, blur, and motion settings.
- Select solid, gradient, custom-image, blurred-artwork, or dynamic Cover Flow backgrounds.
- Start MusicFlow with Windows using the current user's startup setting; administrator access is not required.

## Download

Open the repository's [latest release](../../releases/latest), expand **Assets**, and choose the file that matches how you want to use MusicFlow.

| File | Best for |
| --- | --- |
| `MusicFlow-0.1.0-win64-setup.exe` | Most users. Installs MusicFlow and creates Start menu shortcuts. |
| `MusicFlow-0.1.0-win64-portable.zip` | Portable use or systems where installation is not preferred. |
| `MusicFlow-0.1.0-SHA256SUMS.txt` | Verifying that the downloaded files are complete and authentic. |

Requirements:

- Windows 10 or Windows 11, 64-bit
- A working Windows audio output device
- Approximately 150 MB of free storage
- No separate Qt installation or internet connection

## Install MusicFlow

### Recommended: Windows installer

1. Download `MusicFlow-0.1.0-win64-setup.exe` from the latest GitHub release.
2. Optionally [verify its SHA-256 checksum](#verify-a-download).
3. Close any running copy of MusicFlow.
4. Run the installer and choose the destination and optional desktop shortcut.
5. Select **Launch MusicFlow** when setup finishes.

The current release is not Authenticode-signed. Windows SmartScreen may therefore show **Unknown publisher**. If that happens, first confirm that the file came from this repository and that its checksum matches. You can then choose **More info** and **Run anyway**.

### Portable version

1. Download `MusicFlow-0.1.0-win64-portable.zip`.
2. Right-click the ZIP and select **Extract All**.
3. Move the extracted `MusicFlow` folder anywhere you have write access.
4. Run `MusicFlow.exe` from inside that folder.

Do not run the program inside the ZIP and do not copy only `MusicFlow.exe`. The adjacent Qt DLLs, QML modules, plugins, and `qt.conf` are required.

### Verify a download

Download the checksum file into the same folder as the installer or portable archive. In PowerShell, run:

```powershell
Set-Location "$env:USERPROFILE\Downloads"
Get-FileHash .\MusicFlow-0.1.0-win64-setup.exe -Algorithm SHA256
Get-Content .\MusicFlow-0.1.0-SHA256SUMS.txt
```

The two installer hashes must match exactly. Replace the installer filename with the portable ZIP filename to verify that download instead.

## First run

1. Open **Songs** and choose **Add Files** or **Add Folder**.
2. Select supported audio files or a folder containing your library.
3. Wait for the import summary to show how many tracks were added or skipped.
4. Double-click a track or use its context menu to play it.
5. Right-click tracks to play next, add them to the queue, mark favourites, or add them to a playlist.
6. Open **Settings** to adjust appearance, Cover Flow, artwork, motion, and Windows startup behavior.

MusicFlow scans and extracts metadata away from the UI thread. Large libraries may take time on their first import, but the interface remains available.

## Supported audio files

| Format | Extension | Notes |
| --- | --- | --- |
| MPEG audio | `.mp3` | Metadata and common MP3 playback are supported. |
| FLAC | `.flac` | Lossless metadata and playback are supported. |
| Waveform Audio | `.wav` | Useful as a baseline when diagnosing playback. |
| Ogg audio | `.ogg` | Support depends on the codec contained in the file. |
| MPEG-4 audio | `.m4a` | Some codec variants may not be decoded by the bundled backend. |
| Advanced Audio Coding | `.aac` | Some profiles or protected files may not play. |

Recognition and metadata extraction do not guarantee that every codec variant can be decoded. Playback ultimately depends on the bundled miniaudio decoder and the contents of the file.

## Data, privacy, and updates

MusicFlow is local-first:

- No account, telemetry service, or online library is required.
- Imported audio files remain in their original locations and are opened read-only.
- The library database, settings, managed artwork, queue, playlists, favourites, and history are stored under `%LOCALAPPDATA%\MusicFlow`.
- The Windows startup option writes only to `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run`.

### Update

- **Installer:** close MusicFlow and run the newer installer. It upgrades the application while preserving the Local AppData library.
- **Portable:** extract the new release into a new folder and run it. User data remains available because it is stored outside the portable folder.

### Uninstall

Open **Windows Settings > Apps > Installed apps**, find **MusicFlow**, and select **Uninstall**. The uninstaller intentionally preserves `%LOCALAPPDATA%\MusicFlow` so reinstalling does not erase the library.

To remove personal MusicFlow data as well, first close the application and make a backup of that folder. Deleting personal data is not performed automatically.

## Troubleshooting

### MusicFlow does not open

- Extract the complete portable ZIP before launching it.
- Keep `MusicFlow.exe`, its DLLs, `plugins`, `Qt6`, and `qt.conf` together.
- Confirm that you downloaded the x64 release on 64-bit Windows 10 or 11.
- Re-download the artifact and verify its checksum if Windows reports a corrupt file.
- If a previous process is still running, close it in Task Manager and try again.

### Windows SmartScreen blocks the installer

The release is currently unsigned, so this warning can be expected. Verify the SHA-256 checksum, confirm the download came from this repository, then use **More info > Run anyway**. Do not bypass SmartScreen for an unverified copy from another source.

### Music imports but does not play

- Try a known-good WAV, MP3, or FLAC file first.
- Confirm the original file still exists at the imported path.
- Check the Windows output device and volume mixer.
- Close applications holding the output device in exclusive mode.
- AAC/M4A profiles, protected media, or corrupt files may not be decodable.

### An import reports failed files

MusicFlow reports a failure when metadata cannot be read, a file is corrupt, its extension is unsupported, or the current user cannot access it. Failed imports do not alter the source file. Try copying one affected file to a local folder and importing it again.

### Artwork cannot be imported

Use a readable JPEG, PNG, WebP, BMP, or GIF image. Confirm that the image opens normally in Windows and that `%LOCALAPPDATA%\MusicFlow` is writable. MusicFlow copies and optimizes artwork; it does not edit the selected source image.

### Database startup failure

Close MusicFlow and confirm that `%LOCALAPPDATA%\MusicFlow` is writable and has free disk space. For a non-destructive reset, rename the folder and start MusicFlow again:

```powershell
Rename-Item -LiteralPath "$env:LOCALAPPDATA\MusicFlow" -NewName "MusicFlow.backup"
```

MusicFlow will create a fresh database. Keep the backup until you confirm the new library works.

### Installer failure

Run the installer with logging enabled:

```powershell
& .\MusicFlow-0.1.0-win64-setup.exe "/LOG=$env:TEMP\MusicFlow-install.log"
```

Review the final error and the log near the failure point. Ensure MusicFlow is closed, the target directory is writable, and antivirus software has not quarantined a required file.

## Error and exit codes

### MusicFlow application codes

| Code | Meaning | Suggested action |
| --- | --- | --- |
| `0` | Normal exit. | No action is required. |
| `2` | The SQLite library could not be opened or migrated. | Check Local AppData permissions and disk space; then follow the database recovery steps above. |
| `-1` / `0xFFFFFFFF` | The root QML user interface could not be created. | Reinstall or re-extract the full package; missing QML modules or damaged files are the usual cause. |
| `0xC0000135` / `-1073741515` | Windows could not find a required DLL. This is a Windows loader status, not an application-generated code. | Restore the complete portable folder or reinstall MusicFlow. Do not distribute the EXE by itself. |
| `0xC000007B` / `-1073741701` | Windows loaded a DLL with the wrong architecture or an invalid binary image. | Remove mixed 32/64-bit files and install a clean x64 release. |

### User-facing messages

| Message | Meaning | Suggested action |
| --- | --- | --- |
| `Could not initialize the audio device` | miniaudio could not start a Windows output device. | Check the active output device, reconnect it, and restart MusicFlow. |
| `Cannot decode: <path>` | The selected file could not be decoded. | Test a known-good WAV/MP3/FLAC file; the original may be corrupt or use an unsupported codec. |
| `Unsupported or corrupt audio file` | Metadata extraction failed. | Confirm the format and file integrity, then import again. |
| `That file is not a supported or readable image.` | Artwork decoding failed. | Choose a valid image that opens in Windows. |
| `The artwork was imported, but the library could not be updated.` | The optimized image was created but its database record was not saved. | Check Local AppData permissions and database health. |

### Installer exit codes

The installer uses Inno Setup. Any non-zero result means setup did not complete.

| Code | Meaning |
| --- | --- |
| `0` | Installation completed successfully, or help was displayed. |
| `1` | Setup failed to initialize. |
| `2` | The user cancelled before installation started. |
| `3` | A fatal error occurred while moving to the next setup phase. |
| `4` | A fatal error occurred during installation. |
| `5` | The user cancelled during installation or selected Abort. |
| `6` | Setup was forcefully terminated by its debugger; not expected in a public release. |
| `7` | The Preparing to Install stage determined that setup could not continue. |
| `8` | Setup could not continue and Windows must be restarted to correct the problem. |

See the official [Inno Setup exit-code reference](https://jrsoftware.org/ishelp/topic_setupexitcodes.htm) for the authoritative definitions.

## Build from source

### Prerequisites

Install the following on Windows 10 or 11:

1. **Visual Studio 2022 Community** with:
   - Desktop development with C++
   - A current Windows SDK
   - C++ CMake tools
2. **Git**
3. **CMake 3.25 or newer**
4. **Ninja**
5. **vcpkg** with the `x64-windows` triplet

The manifest installs Qt 6, TagLib, and miniaudio. The initial Qt build can take significant time and disk space.

### Configure and build

Open **Developer PowerShell for VS 2022**, change to the repository folder, and run:

```powershell
Set-ExecutionPolicy -Scope Process Bypass
.\scripts\bootstrap-vcpkg.ps1
$env:VCPKG_ROOT = "$env:USERPROFILE\vcpkg"
.\scripts\build.ps1
```

Or run each CMake stage manually:

```powershell
$env:VCPKG_ROOT = "$env:USERPROFILE\vcpkg"
cmake --preset windows-release
cmake --build --preset windows-release
ctest --preset windows-release
```

Run the development build with:

```powershell
.\scripts\run.ps1
```

The tests cover database behavior and QML startup at multiple resolutions and Windows scaling factors.

### Common build errors

| Error | Fix |
| --- | --- |
| `cl is not recognized` | Use Developer PowerShell for VS 2022. |
| `Ninja not found` | Install Ninja and restart the terminal. |
| `VCPKG_ROOT is not set` | Set it in the same terminal before configuring. |
| Qt or TagLib not found | Confirm `VCPKG_ROOT`, then run `cmake --fresh --preset windows-release`. |
| `LNK1104: cannot open file MusicFlow.exe` | Close every running MusicFlow process before rebuilding. |
| `LNK1181: cannot open input file user32.lib` | Build from Developer PowerShell so Windows SDK library paths are configured. |
| `QSQLITE driver not loaded` | Rebuild/deploy the Qt `sqldrivers` plugin; do not copy only the EXE. |
| `No Qt platform plugin could be initialized` | Restore `plugins`, QML modules, and `qt.conf`, or run `scripts\run.ps1`. |

## Create a release package

Build and test first. Install Inno Setup to produce the Windows installer, then run:

```powershell
.\scripts\package.ps1 -Version 0.1.0
```

The packaging script:

1. Creates a clean staging folder at `dist\MusicFlow`.
2. Deploys required Qt/QML modules, plugins, TagLib, and Visual C++ runtime files.
3. Excludes Windows system DLLs and development debug symbols.
4. Collects third-party license texts and creates `PACKAGE-MANIFEST.json`.
5. Produces the portable ZIP and, when Inno Setup is available, the installer.
6. Writes SHA-256 checksums into `dist\release`.

GitHub-ready artifacts are written to:

```text
dist\release\MusicFlow-<version>-win64-setup.exe
dist\release\MusicFlow-<version>-win64-portable.zip
dist\release\MusicFlow-<version>-SHA256SUMS.txt
dist\release\RELEASE_NOTES.md
```

Public binaries should be Authenticode-signed before broad distribution to reduce SmartScreen warnings.

## Project structure

| Path | Purpose |
| --- | --- |
| `src` | C++ application, audio, database, library, queue, playlist, and platform services. |
| `qml` | Qt Quick interface, pages, reusable controls, and theme. |
| `resources/windows` | Application logo, multi-resolution icon, resource script, and release `qt.conf`. |
| `tests` | Database and application smoke tests. |
| `scripts` | Dependency bootstrap, build, run, deployment, and packaging automation. |
| `installer` | Inno Setup definition for the Windows installer. |
| `dist/release` | Generated GitHub release artifacts; not source code. |

## Current limitations

- MusicFlow currently targets Windows x64.
- Codec support varies for AAC, M4A, protected media, and unusual containers.
- Metadata changes are stored as local overrides; source-file tag write-back is not implemented.
- Global media keys, watched folders, online artist images, and generated artwork mosaics are future work.
- Public artifacts are currently unsigned.

## Third-party software and licensing

MusicFlow uses Qt, TagLib, miniaudio, and their transitive dependencies. Packaged builds include complete dependency notices under `licenses`; see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for a summary.

A project-level source license has not yet been selected. Do not assume reuse rights beyond those explicitly granted by the third-party licenses until a repository `LICENSE` file is added.
