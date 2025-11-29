# ReelGuard Backup Checker

ReelGuard is a Windows-only safety net for anyone dealing with card media who needs confidence that every card has been copied before it’s reused or reformatted. It watches your removable media, confirms files exist in your backup destinations and can wipe or fake-format cards after performing a match of **file name** and **file size** in your specified backup destination(s).

> **Important:** ReelGuard does **not** perform checksum or hash verification. It compares file names and file sizes. You are responsible for using appropriate ingest and checksum tools in your workflow.

Download link: https://webmojo.com.au/wp-content/uploads/2025/11/reelguard_backup_checker_0.5_Win_Setup.zip

---

## Highlights

- Built for Windows 10/11
- Compares cards file names and file sizes against one or more backup destinations
- Lists mounted SD/CF/CFexpress/SSDs/microSDs and other removable drives to perform backup checks
- Multiple post backup check operation modes - Wipe Card or Fake-Format Card (reversible)
- Force operators to format cards in camera with the fake-format mode
- Folder Mode for simple mirror file comparison of 2 destinations
- Prep-Mode to quickly prepare (wipe/fake-format) cards for an upcoming shoot 
- Detailed settings to adjust the app to your workflow such as ignoring files and folders during backup-checks, flag certain filetypes, hotkeys, and more...

---

## Who It’s For

- DITs, Media Managers and Data Wranglers
- Edit assistants and post-production teams handling card media
- Anyone who wants a final “did we really back up this card?” check before reusing cards

Important: ReelGuard is designed to **ignore system drives and non-removable drives** to avoid potentially dangerous operations. However, wiping and fake-formatting are always potentially destructive actions. **Always double-check you are operating on the correct card or drive** to avoid unwanted data loss. Make sure you read and understand the documentation and use at your own risk!

---

## System Requirements

- Windows 10 or Windows 11 (64-bit)
- Local Admin rights to install the desktop app
- Administrator rights to use the fake-format function

---

## Download & Install

1. Grab the latest `.zip` release from the GitHub Releases page.
2. Extract the .zip file. It contains the ReelGuard Windows installer (`ReelGuard_{version}_Setup.exe`).
3. Double-click the installer. Windows SmartScreen may flag the download because it’s new:
   - Choose **More info**.
   - Click **Run anyway** to continue.
4. Follow the installer prompts. All dependencies are bundled, no separate install is required.
5. Launch ReelGuard from the Start Menu. An uninstaller is created automatically if you ever need to remove it.

---

## First-Time Setup

1. Open ReelGuard and go to **Backup Destinations**.
2. Set the minimum number of destinations that must contain a file before the app considers it “safe”.
3. Add folders or drives where you store card backups (e.g. SSD, RAID, NAS share).
4. Go through the settings to configure the app to your workflow and needs.
5. Return to the cards view and start the backup check by clicking on the "Check Backup Status" button.
6. ReelGuard lists any removable volumes formatted as FAT/exFAT/UDF as "Cards"

---

## Workflow

1. **Insert Card Media**  
   ReelGuard lists removable card media and other devices using the volume label so you can see at a glance which card you’re checking.

3. **Press “Check Backup Status”**  
   The app compares files on the card to all configured backup destinations by **file name** and **file size**.

4. **Review the results**  
   You’ll see which destinations have matching files and which are missing copies according to the comparison rules.

5. **Run the global hotkey (optional)**  
   Once enabled in Settings, you can set your own keyboard shortcut to run backup checks for all connected cards.

6. **Wipe or fake-format when you’re ready**  
   After a successful verification, you can directly perform your selected operation which is **Wipe Card** or **Fake Format**.  
   - Destructive operations are **restricted to removable drives** – system and fixed internal drives are ignored and protected.  
   - Even so, **always verify you’ve selected the correct card/drive** before proceeding. Use at your own risk!

---

## Verification Method (No Checksums)

ReelGuard does **not** calculate checksums or hashes.

Instead, it verifies that every file on the card exists in your backup destinations by comparing:

- **File name**, and  
- **File size**

If a file with the same name and size is found in the required number of destinations, ReelGuard treats it as “backed up” for the purposes of its checks.
This means there is a chance of false-positives if two or more files have the same file name and size on the backup destination.

> For end-to-end checksum verification (MD5/SHA/xxHash), you should use your preferred offloading or ingest tool.  
> ReelGuard is intended as a final **“did the files land where they’re supposed to?”** safety check before you recycle or prep cards for reuse.

---

## Operating Modes

### Wipe Mode

- Default operation mode after a successful verification.
- Lets you directly delete the contents of a card once every file is confirmed across the required destinations.
- System and non-removable internal drives are locked out so you shouldn't be able to wipe your OS or fixed storage by accident.
- **Caution:** Wipes are permanent. Always confirm you’re wiping the correct card or removable drive.

### Fake-Format Mode

- Destroys the card’s file system so it appears unreadable to cameras, computers and other devices.  
  Operators will be forced to **format the card in their device (e.g. camera)** before they can use it.
- **Fully reversible in ReelGuard:**  
  - When Fake-Format Mode is enabled, you can run the **Restore** tool to rebuild the original file system view.  
  - Click the **Scan** button in the Cards view to detect fake-formatted cards and restore the data.
- Useful if you want to ensure cards are always formatted by operators rather than reused without a fresh in-camera format.
- **Caution:** While reversible in ReelGuard, fake-formatting is still a low-level operation on the card’s file system and can be prone to data-loss with untested devices. Double-check the device before using it.

### Tested Cameras & Cards
- SONY FX9/FX6/FX3/A7S -> XQD, CFexpress Type-A
- GoPros -> microSD

### Folder Mode

- Ideal when the “card” is actually folders on a shuttle drive or NAS or when you just want to sanity-check mirror copies.
- Instead of wiping or fake-formatting, you pick specific source folders (e.g. specific media folders on the NAS) and verify that the same file names and file sizes exist on the target drives.
- Lets you validate multiple destinations quickly **without altering any device**.

**Folder Mode Example:**

1. Enable Folder Mode.
2. In the Cards view, select the folders on your main storage (e.g. NAS) that represent your “source”.
3. Add your shuttle drive or certain folders of it as the backup destination.
4. ReelGuard will confirm that the folders on the shuttle drive match your selected source folders by file name and file size.

---

## Settings & Controls Overview

### Backup Destinations

- Add as many destinations as you need (local SSD, RAID, NAS, shuttle drive).
- Use the **Minimum backup destinations** dropdown to define how many copies must be present before a card is considered “safe”.
- Destinations can be local or network paths as long as Windows can access them.

### Hotkey Settings (disabled by default)

- Click **Set Hotkey** to record a shortcut (e.g. `Ctrl+Shift+E`).
- Toggle **Enable hotkey** when you’re ready for the shortcut to run background checks.
- Use the hotkey to re-check ALL connected cards without opening the UI.
- If the hotkey doesn’t fire, another app may already be using that combination—pick a different one.

### File Scanning Options

- **Exclude hidden files and folders**  
  Skips skipps any hidden files and folders during the backup check.
  Important: Hidden files and folders will still be deleted during when performing the wipe operation.
- **Show file counts**  
  Adds totals to the results dialogue. When it’s on, you can optionally **count hidden files** in those totals.

These options affect **verification checks only**. They do **not** change how wiping or fake-formatting behaves.

### Safety Options

- **Allow wiping/fake formatting when backup check fails** (off by default)  
  - When off, ReelGuard will block destructive operations if the backup verification fails.  
  - When on, you can override missing-file warnings and proceed with the wipe or fake-format operation anyway. 
  - Use this options with care and only when you are certain the card is safe to reuse.

- **After successful backup check**  
  Choose the default destructive action button:
  - **Wipe Drive**, or
  - **Fake Format Drive**

- **Prep Mode**  
  - Temporarily bypasses the backup checks and performs the selected card operation immediately (wipe or fake-format, depending on your setting).
  - Intended for situations where you already know the card is redundant and you just want to prep them quickly.  
  - When enabled you will see a warning notification in the cards view. For safety, the prep-mode will automatically be turned off after 15 minutes. You then have to re-enable it again.
  - **Use with extreme care**: ReelGuard will not check backups when Prep Mode is active.

> **Note:** All destructive operations (Wipe, Fake-Format, Prep Mode actions) are restricted to removable drives detected by Windows. System and non-removable drives are excluded. Even so, **always confirm the selected drive** before you proceed.

### Folder Mode Toggle

- Enable **Folder Mode** (Settings → Folder Mode switch) to treat local/network folders as “virtual cards”.
- In Folder Mode:
  - Only backup checks are available.
  - Wiping and fake-formatting are **disabled**.
- Perfect for confirming NAS storage matches shuttle drives.

### Ignored drives
- Let's you hide specific cards/drives from the Cards list so they never show up in day-to-day use.
- Once hidden, you can remove them via Settings -> Ignored Drives at the bottom

### Ignore & Flag Lists

ReelGuard lets you fine-tune what’s considered during **backup checks**:

- **Ignore or Flag certain File extensions**  
  - Add an extension as **Ignore** to skip those files entirely during the backup check. These files will still be deleted when performing the wipe operation.
  - Add an extension as **Flag** to highlight those files in the results dialogue when they're detected during a backup check.

- **Ignored folders**  
  Provide folder names (case-sensitive) to exclude from scans—helpful for system folders that always appear on removable media.
  These folders will still be deleted when performing the wipe operation.

> **Important:** Ignore & Flag settings affect **backup verification only**.  
> If you run a **Wipe** or **Fake-Format** operation on a card, **all files and folders on that card will be removed**, including anything you have configured to ignore or flag.  
> Ignore rules do **not** protect files from being wiped.

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
  - If your offloading tool renames files the backup check will fail.
  - Be vary of false-positives. Any files with the same file name AND file size will be considered backed up.

---

## Safety & Responsibility

ReelGuard is designed with protective defaults:

- Destructive operations are restricted to **removable** drives.
- System and fixed internal drives are excluded from wiping and fake-formatting.

However, no software can fully protect against operator error. **You are responsible for:**

- Ensuring you’re operating on the correct card or drive.
- Maintaining a robust offload and checksum verification workflow with an offload tool of your choice.
- Verifying that your backups are valid and complete.

Treat ReelGuard as an extra safety net in your backup workflow, not as a replacement for good data management practices.

---

## License

ReelGuard ships with a proprietary licence. See `LICENSE.txt` (bundled with the installer) for the full legal terms.

