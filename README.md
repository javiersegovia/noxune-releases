# noxune-releases

Signed installers and the update feed for Noxune. No source code.

## Install

Download the latest release from the [Releases page](https://github.com/javiersegovia/noxune-releases/releases/latest). Ignore the `-beta` and `-rc` prereleases unless you want to test early builds.

### macOS (Apple silicon)

Intel Macs aren't supported yet.

1. Download `Noxune-<version>-arm64.dmg`.
2. Open it and drag **Noxune** into **Applications**.
3. Clear the download quarantine once, before the first launch:

   ```bash
   xattr -dr com.apple.quarantine /Applications/Noxune.app
   ```

4. Open Noxune from Applications.

Why step 3: Noxune is signed with its own certificate, not an Apple Developer ID, so it isn't notarized yet and Gatekeeper blocks the first launch with a "can't be opened" or "is damaged" message. Clearing the quarantine flag is the reliable way past it.

If you'd rather not use the terminal, open Noxune once, dismiss the warning, then go to **System Settings → Privacy & Security**, scroll down to the message about Noxune and click **Open Anyway**. Confirm with your password.

You only do this once. Updates install from inside the app.

#### Optional permissions

- **Full Disk Access**, to import cookies from Safari or a browser macOS protects. Noxune tells you when it needs it and opens the right settings page. Add Noxune under **System Settings → Privacy & Security → Full Disk Access**, then restart it.
- **Administrator password**, once, when you install the `noxune` command (see below).

### Linux (x86_64)

1. Download `Noxune-<version>-x86_64.AppImage`.
2. Make it executable and run it:

   ```bash
   chmod +x Noxune-*-x86_64.AppImage
   ./Noxune-*-x86_64.AppImage
   ```

If it doesn't start and mentions FUSE, install `libfuse2` (on Ubuntu 22.04 and later: `sudo apt install libfuse2`).

## What Noxune needs

- `git` on your `PATH`.
- The agent CLIs you want to use, such as [Claude Code](https://docs.anthropic.com/en/docs/claude-code) or [Codex](https://github.com/openai/codex). **Settings → Providers** shows which ones it found and updates them.
- Optional: the [GitHub CLI](https://cli.github.com/) (`gh`), signed in with `gh auth login`, for pull request and CI status.

## The `noxune` command

Open **Settings → General** and click **Install** under **Command Line**.

- macOS asks for your administrator password once and links `/usr/local/bin/noxune` into the app, so the command survives updates.
- Linux writes `~/.local/bin/noxune` and refreshes it on every launch. The command works while Noxune is running.

## Updates

Noxune checks for updates at launch and every few hours. A badge in the title bar shows the new version and its release notes, downloads it, and restarts now or once you're idle.

**Settings → General** has an update track: **Stable** takes only stable releases, **Beta** also takes the daily beta builds. Switching back to Stable never downgrades; you stay on your version until a newer stable release ships.

Builds from v0.2 and earlier can't update in place. Replace them once with a fresh download.
