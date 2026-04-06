# SFTP File Browser

Synapse includes a built-in SFTP browser for navigating and transferring files without leaving the app. It integrates with iOS Files.app, so downloaded files are immediately available to other apps.

---

## Opening the SFTP Browser

Long-press any connection card on the home screen → **Browse Files**. The browser opens directly to your home directory.

Alternatively, tap the **…** menu on a connection card → **Browse Files**.

> SFTP browsing is a Pro feature.

---

## Navigating

- **Tap a folder** to enter it
- **Breadcrumb bar** at the top shows your current path — tap any segment to jump back up
- **Swipe back** from the left edge to go up one directory
- **Pull to refresh** the current directory listing

---

## Downloading Files

Tap any file to download it. A progress indicator appears during transfer. Once complete, the file opens in a preview or is saved to Synapse's local storage.

**Open in another app**

After downloading, tap **Share** (the iOS share sheet icon) to open the file in any compatible app — text editors, PDF readers, image viewers, code editors, etc. This is how you edit a remote config file locally: download → open in your editor → make changes → upload back.

**Save to Files.app**

From the share sheet, tap **Save to Files** to save the downloaded file to any location in Files.app — iCloud Drive, On My iPhone, or any connected provider.

---

## Uploading Files

Tap **+** (or the upload icon) in the toolbar to upload:

- **From Files.app** — browse and select any file from iCloud Drive, local storage, or connected providers
- **From Photos** — select images or videos from your photo library

The file is uploaded to the current directory. Progress is shown in the toolbar.

---

## Workflows

**Edit a remote config file**
1. Navigate to the file in the SFTP browser
2. Tap to download
3. Share → open in a text editor (e.g. Textastic, Kodex, Working Copy)
4. Make your edits and save
5. Return to Synapse SFTP browser, navigate to the same directory
6. Upload the edited file

**Back up a remote file before editing**
1. Download the file
2. Save to Files.app → iCloud Drive
3. Open an SSH session and edit on the server
4. If something goes wrong, upload the backup from Files.app

**Transfer files between two servers**
1. Download from server A via SFTP
2. Save to Files.app
3. Open a second tab connected to server B
4. Open SFTP browser for server B → upload from Files.app

---

## Tips

**Hidden files** — files and folders starting with `.` are shown by default. Look for config files like `.bashrc`, `.ssh/`, `.config/` in your home directory.

**Permissions errors** — if a download or upload fails, the remote file or directory may not be readable/writable by your SSH user. Check permissions with `ls -la` in the terminal.

**Large files** — there is no hard size limit, but very large files (multi-GB) will take time depending on your connection. Keep the app in the foreground during large transfers.
