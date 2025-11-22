# ReelGuard Backup Checker

ReelGuard is a Windows-only safety net for anyone dealing with card media who needs confidence that every card has been copied before it’s reused or reformatted. It watches your removable media, confirms files exist in your backup destinations, and can wipe cards only after performing a match of **file name** and **file size** in your specified backup destination(s).

> **Important:** ReelGuard does **not** perform checksum or hash verification. It only compares file names and file sizes. You are responsible for using appropriate ingest and checksum tools in your workflow.

**TL;DR:** ReelGuard double-checks that files landed where they’re supposed to before you recycle your cards or shuttle drives.

---

## Highlights

- Built for Windows 10/11
- Watches SD/CF/CFexpress/SSDs/microSDs and other removable drives in real time
- Compares card contents against one or more backup folders
- Optional secure wipe once verification succeeds
- Global hotkey to run all checks without touching the UI

---

## Who It’s For

- DITs and data wranglers on set  
- Edit assistants and post-production teams handling shuttle drives  
- Anyone who wants a final “are these really backed up?” check before reusing cards

ReelGuard is designed to **avoid system drives and non-removable drives** for destructive operations. However, wiping and fake-formatting are always potentially destructive actions. **Always double-check you are operating on the correct card or drive** to avoid unwanted data loss.

---

## System Requirements

- Windows 10 or Windows 11 (64-bit)
- Administrator rights to install the desktop app
- At least one removable storage device
- Recommended: two backup destinations (primary + safety copy)

---

## Download & Install

1. Grab the latest `.zip` release from the GitHub Releases page.
2. Extract the archive. It contains the ReelGuard Windows installer (`ReelGuard_{version}_Setup.exe`).
3. Double-click the installer. Windows SmartScreen may flag the download because it’s new:
   - Choose **More info**.
   - Click **Run anyway** to continue.
4. Follow the installer prompts. All dependencies are bundled; no separate install is required.
5. Launch ReelGuard from the Start Menu. An uninstaller is created automatically if you ever need to remove it.

---

## First-Time Setup

1. Open ReelGuard and go to **Backup Destinations**.
2. Add folders or drives where you store card backups (e.g. SSD, RAID, NAS share).
3. Set the minimum number of destinations that must contain a file before the app considers it “safe”.
4. (Optional) Configure the global hotkey. It is disabled by default until you record a shortcut (e.g. `Ctrl+Shift+E`) and toggle it on in **Settings**.
5. (Optional) Decide whether hidden/system files should be excluded from backup checks.

---

## Daily Workflow

1. **Insert a card**  
   ReelGuard lists it using the volume label so you can see at a glance which card/shoot you’re checking.

2. **Press “Check Backup Status”**  
   The app compares files on the card to all configured backup destinations by **file name** and **file size**.

3. **Review the results**  
   You’ll see which destinations have matching files and which are missing copies according to the comparison rules.

4. **Run the global hotkey (optional)**  
   Once enabled in Settings, your recorded shortcut runs backup checks for all connected cards without opening the UI or Cards page.

5. **Wipe or fake-format when you’re ready**  
   After a successful verification, you can choose **Wipe Card** or **Fake Format** (depending on your Settings).  
   - Destructive operations are **restricted to removable drives** – system and fixed internal drives are protected.  
   - Even so, **always verify you’ve selected the correct card/drive** before proceeding.

---

## Updating

- ReelGuard checks GitHub for new releases. When an update is available, you’ll see a prompt inside the app with a download link.
- You can always visit the Releases page manually if you prefer to download the latest installer yourself.

---

## Verification Method (No Checksums)

ReelGuard does **not** calculate checksums or hashes.

Instead, it verifies that every file on the card exists in your backup destinations by comparing:

- **File name**, and  
- **File size**

If a file with the same name and size is found in the required number of destinations, ReelGuard treats it as “backed up” for the purposes of its checks.

> For end-to-end checksum verification (MD5/SHA/xxHash), you should use your preferred offloading or ingest tool.  
> ReelGuard is intended as a final **“did the files land where they’re supposed to?”** safety check before you recycle or prep the card.

---

## Operating Modes

### Wipe Mode

- Default destructive mode after a successful verification.
- Lets you securely delete the contents of a card once every file is confirmed across the required destinations.
- System and non-removable internal drives are locked out so you can’t wipe your OS or fixed storage by accident.
- **Caution:** Wipes are permanent. Always confirm you’re wiping the correct card or removable drive.

### Fake-Format Mode

- Destroys the card’s file system so it appears unreadable to cameras and computers.  
  Operators will be forced to **format the card in camera** before they can use it.
- **Fully reversible in ReelGuard:**  
  - When Fake-Format Mode is enabled, you can run the **Restore** tool to rebuild the original file system view.  
  - Click the **Scan** button in the Cards view to detect fake-formatted cards and restore the data.
- Useful if you want to ensure cards are always formatted by camera operators rather than reused without a fresh in-camera format.
- **Caution:** While reversible in ReelGuard, fake-formatting is still a low-level operation on the card’s file system. Double-check the device before using it.

### Folder Mode

- Ideal when the “card” is actually a shuttle drive or when you just want to sanity-check mirror copies.
- Instead of wiping or fake-formatting, you pick specific source folders (e.g. camera archives on the NAS) and verify that the same file names and file sizes exist on the target drives.
- Lets you validate multiple destinations quickly **without altering any device**.

**Example:**

1. Enable Folder Mode.
2. In the Cards view, select the folders on your main storage (e.g. NAS) that represent your “source”.
3. Add your shuttle drive as the backup destination.
4. ReelGuard will confirm that the folders on the shuttle drive match your selected source folders by file name and file size.

---

## Settings & Controls Overview

### Backup Destinations

- Add as many destinations as you need (local SSD, RAID, NAS, shuttle drive).
- Use the **Minimum backup destinations** dropdown to define how many copies must be present before a card is considered “safe”.
- Destinations can be local or network paths as long as Windows can access them.

### Hotkey Settings (disabled by default)

- Click **Set Hotkey** to record a shortcut (e.g. `Ctrl+Shift+E`).
- Flip **Enable hotkey** when you’re ready for the shortcut to run background checks.
- Use the hotkey to re-check all connected cards without opening the UI.
- If the hotkey doesn’t fire, another app may already be using that combination—pick a different one.

### File Scanning Options

- **Exclude hidden files and folders**  
  Skips `.Trash`, `.Spotlight-V100`, and similar clutter when comparing folders.
- **Show file counts**  
  Adds totals to the results dialogue. When it’s on, you can optionally **count hidden files** in those totals.

These options affect **verification checks only**. They do **not** change how wiping or fake-formatting behaves.

### Safety Options

- **Allow wiping/fake formatting when backup check fails** (off by default)  
  - When off, ReelGuard will block destructive operations if the backup verification fails.  
  - When on, you can override missing-file warnings and proceed anyway.  
  - Use this sparingly and only when you are certain the card is safe to reuse.

- **After successful backup check**  
  Choose the default destructive action button:
  - **Wipe Drive**, or
  - **Fake Format Drive**

- **Prep Mode**  
  - Temporarily bypasses verification and performs the selected card operation immediately (wipe or fake-format, depending on your setting).  
  - Intended for situations where you already know the card is redundant (e.g. brand-new cards or test media) and you just want to prep them quickly.  
  - **Use with extreme care**: ReelGuard will not check backups when Prep Mode is active.

> **Note:** All destructive operations (Wipe, Fake-Format, Prep Mode actions) are restricted to removable drives detected by Windows. System and non-removable drives are excluded. Even so, **always confirm the selected drive** before you proceed.

### Folder Mode Toggle

- Enable **Folder Mode** (Settings → Folder Mode switch) to treat local/network folders as “virtual cards”.
- In Folder Mode:
  - Only backup checks are available.
  - Wiping and fake-formatting are **disabled**.
- Perfect for confirming NAS storage matches shuttle drives before sending them off-site.

### Ignore & Flag Lists

ReelGuard lets you fine-tune what’s considered during **backup checks**:

- **Ignored drives**  
  Hide specific cards/readers from the Cards list so they never show up in day-to-day use.

- **File extensions**  
  - Add an extension as **Ignore** to skip those files entirely during verification (e.g. `.xmp`, `.tmp`).  
  - Add an extension as **Flag** to highlight those files in the results dialogue for manual review.

- **Ignored folders**  
  Provide folder names (case-sensitive) to exclude from scans—helpful for system folders that always appear on removable media.

- **Flagged hits**  
  Flagged files appear in the backup results dialogue with quick links to open the source and destination folders so you can inspect or clean them up.

> **Important:** Ignore & Flag settings affect **backup verification only**.  
> If you run a **Wipe** or **Fake-Format** operation on a card, **all files and folders on that card will be removed**, including anything you have configured to ignore or flag.  
> Ignore/flag rules do **not** protect files from being wiped.

---

## Troubleshooting

- **Windows SmartScreen warning**  
  - Click **More info** → **Run anyway**.  
  - The installer is code-signed, but brand new releases can still trigger SmartScreen until they build reputation.

- **Drive not showing**  
  - Make sure the card is mounted and visible in Windows Explorer.  
  - Some card readers expose multiple slots; only mounted volumes appear in ReelGuard.

- **Hotkey not firing**  
  - Check that you recorded a shortcut and enabled it in **Settings**.  
  - Try a different key combination if another application is using the same shortcut.

- **Verification looks wrong**  
  - Remember: only **file name** and **file size** are compared.  
  - If your ingest tool renames files or changes structure, make sure your backup destinations match how the card currently looks.

---

## Safety & Responsibility

ReelGuard is designed with protective defaults:

- Destructive operations are restricted to **removable** drives.
- System and fixed internal drives are excluded from wiping and fake-formatting.
- Backup checks fail safe by default (you cannot wipe/fake-format until verification passes, unless you explicitly override).

However, no software can fully protect against operator error. **You are responsible for:**

- Ensuring you’re operating on the correct card or drive.
- Maintaining a robust ingest and checksum workflow.
- Verifying that your backups are valid and complete.

Treat ReelGuard as an extra safety net in your backup chain, not as a replacement for good data management practices.

---

## License

ReelGuard ships with a proprietary licence. See `LICENSE.txt` (bundled with the installer) for the full legal terms.

