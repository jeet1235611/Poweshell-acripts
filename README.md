
What is Windows Backup?

It’s a built-in backup app in Windows 11 (22H2+ and 23H2+).

It lets you back up your files, settings, and apps to the cloud, using OneDrive + your Microsoft account.

It’s designed to make moving to a new PC easy — when you sign in with the same Microsoft account, Windows restores your files and settings automatically.



---

🔹 What Windows Backup Saves

1. Files & Folders

Desktop

Documents

Pictures

Videos

Music
(→ These go to OneDrive if enabled.)



2. App List

It remembers which apps you had installed, so when you sign in on a new PC, the Microsoft Store reinstalls them.



3. System Settings

Wi-Fi networks & passwords

Accessibility options

Personalization (wallpapers, themes)

Language & keyboard settings



4. Credentials & Preferences

Microsoft Edge settings, favorites, and passwords (if synced).

Wi-Fi and Bluetooth device pairings.





---

🔹 Difference between Windows Backup and OneDrive

Windows Backup = umbrella service (remembers apps, settings, and connects to your OneDrive).

OneDrive = handles the actual file syncing and cloud storage.

So, when you see “Windows Backup” in Start menu, it’s basically a shortcut into your OneDrive + settings backup service.



---

🔹 How to Check Your Backup

1. Open Windows Backup (search in Start).


2. You’ll see toggles for:

OneDrive folder backup (Desktop, Documents, Pictures)

Settings backup

Apps backup



3. You can manage or restore from there.




---

✅ In your setup with mklink for D:\ → OneDrive, your D: data is already syncing to OneDrive.
If you also turn on Windows Backup, then:

Files (D: mirrored folders) → sync via OneDrive.

PC settings, apps, preferences → backed up for new device restore.



$$$$$$$



Nice 👍 I can clearly see your OneDrive → John - Personal structure with folders like Documents, Downloads, Music, Pictures, Videos, Desktop, etc. — and the green tick / cloud icons show that syncing is already happening.

Now let’s nail Step 2: constant sync between D: drive and OneDrive in a clean way.


---

🔹 Step-by-Step Guide (Constant Sync for D:)

1. Decide: Move or Mirror

If you want all your D: files always in OneDrive, you have two main choices:

1. Move files into OneDrive folders (simplest, 100% supported by Microsoft).


2. Mirror (link) your D: folders into OneDrive (advanced, using symbolic links).





---

2. The Recommended Method (Move)

1. Go to **D:**.


2. Create subfolders inside D:\OneDrive for each category (e.g., D:\OneDrive\Projects, D:\OneDrive\Media).


3. Move your existing D:\ files into these OneDrive subfolders.

Example:

Move D:\Work → D:\OneDrive\Work

Move D:\Photos → D:\OneDrive\Photos




4. From now on, every file you save into these OneDrive subfolders will constantly sync.




---

3. Advanced Method (Mirror via mklink)

If you don’t want to move your D: content, you can link D: folders into OneDrive:

1. Open Command Prompt (Admin).


2. Run commands like these (replace <YourUser> with your Windows username):



mklink /d "C:\Users\<YourUser>\OneDrive\John - Personal\D_Documents" "D:\Documents"
mklink /d "C:\Users\<YourUser>\OneDrive\John - Personal\D_Downloads" "D:\Downloads"
mklink /d "C:\Users\<YourUser>\OneDrive\John - Personal\D_Backup" "D:\"

This creates a “bridge” inside OneDrive pointing to your D: folders.

OneDrive will sync them as if they’re stored directly in OneDrive.


⚠️ Note: Symbolic links are powerful but unsupported by Microsoft. If you want reliability, moving files into OneDrive folders is safer.


---

4. Verify Constant Sync

In your screenshot, check the Status column:

✅ Green tick = file is synced and offline copy exists.

☁ Cloud icon = file is synced, online only.

🔄 Two arrows = syncing in progress.


Test: Create a new file in D: → confirm it appears in OneDrive → John - Personal with a sync icon → confirm it also shows up at onedrive.live.com.



---

👉 Do you want me to prepare a ready-to-paste mklink script that will link your entire D: drive into OneDrive (one shortcut), so you don’t have to link each folder separately?



-----
Awesome—here’s Step 2 in full detail to make your D: drive content sync constantly to OneDrive on Windows 11.
(The safest, supported way is to keep your data inside the OneDrive folder. OneDrive only syncs what’s inside its folder.)

1) Put OneDrive itself on D:

1. Click the OneDrive cloud icon → Settings → Accounts tab → Unlink this PC.


2. OneDrive sign-in window appears. Sign in.


3. When it shows “Your OneDrive folder”, click Change location → pick D:\OneDrive (create the folder if needed) → Next.


4. Keep Files On-Demand enabled (recommended): “Save space and download files as you use them.”



> Result: Your OneDrive folder lives at D:\OneDrive. Anything you keep under this folder syncs automatically.



2) Put your D: data under D:\OneDrive (so it syncs)

You have two clean options—pick one or mix:

A. Move folders into OneDrive (recommended)

Create structure under D:\OneDrive (e.g., D:\OneDrive\Documents, Pictures, Videos, Work, etc.).

Move your existing D:\ folders/files into these.

From now on, save inside these OneDrive subfolders.


B. Redirect Windows libraries to OneDrive on D: (for convenience)

Right-click Documents in File Explorer → Properties → Location tab → Move…

Choose D:\OneDrive\Documents → Apply.

Repeat for Pictures, Music, Videos, Desktop (point to matching folders under D:\OneDrive).


3) Turn on Known Folder Backup (Desktop, Documents, Pictures)

1. OneDrive Settings → Sync and backup → Manage backup.


2. Toggle Desktop, Documents, Pictures to Back up.

This keeps those key folders protected and synced, even if apps save to the default library paths.




4) Make it “constant” (reliability settings)

Start OneDrive with Windows: Settings → General → “Start OneDrive when I sign in”.

Do not pause on battery saver/metered: Settings → Sync and backup → Advanced settings → disable auto-pause if you want nonstop sync.

Bandwidth: Settings → Network → leave Don’t limit (or set limits if your internet is capped).

Always keep on this device: Right-click critical folders in D:\OneDrive → Always keep on this device (keeps local copies while still syncing).

Folder selection: Settings → Account → Choose folders to ensure the folders you care about are included.


5) Verify it’s working

In D:\OneDrive, check icons:

Solid green tick = local + synced

Cloud = online-only (download on demand)

Sync arrows = uploading/downloading now


Also check at OneDrive on the web; edits on PC should appear within seconds/minutes.


6) What if you want “ALL of D:” to sync?

OneDrive cannot sync the entire D: root. It only syncs the OneDrive folder.

Best practice: keep everything you want protected inside D:\OneDrive\….

Avoid trying to sync with junctions/symlinks—these are unsupported and can cause loops or missed files.


7) Things OneDrive doesn’t like (avoid in your D:\OneDrive)

Very large constantly-open files (e.g., Outlook .pst), temporary/cache folders, or database files that are open all day.

Invalid characters in names (* ? " < > |), or super-long paths (keep total path under ~400 chars).


8) Do the same on your laptop

Install/sign in to OneDrive, choose the same folder structure, and turn on Known Folder Backup.

Both machines will then stay in lockstep via the cloud.


If you want, tell me your Windows username (e.g., C:\Users\Jeet) and the exact folders you keep on D:, and I’ll map them to a clean D:\OneDrive\... structure for you so you can just move them and be done.


---# Poweshell-acripts
# Fix-BrokenWindowsApps.ps1
# Run as Administrator

Write-Host "=== Starting Fix for Broken Windows Default Apps ===`n"

# Step 1: Re-register all built-in apps
Write-Host "Re-registering built-in apps..."
Get-AppxPackage -AllUsers | ForEach-Object {
    Try {
        Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml" -ErrorAction Stop
    } Catch {
        Write-Warning "Failed to register: $($_.Name)"
    }
}

# Step 2: Reset Microsoft Store
Write-Host "`nResetting Microsoft Store..."
Get-AppxPackage -AllUsers Microsoft.WindowsStore | ForEach-Object {
    Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml"
}

# Step 3: Fix permissions for WindowsApps folder
Write-Host "`nFixing permissions on WindowsApps..."
icacls "C:\Program Files\WindowsApps" /grant "ALL APPLICATION PACKAGES":(OI)(CI)(F) /t

# Step 4: Ensure services are running
Write-Host "`nEnsuring AppX and App Readiness services are running..."
Start-Service -Name "AppReadiness" -ErrorAction SilentlyContinue
Start-Service -Name "AppXSvc" -ErrorAction SilentlyContinue

# Step 5: Install broken apps via winget (if installed)
if (Get-Command winget -ErrorAction SilentlyContinue) {
    Write-Host "`nReinstalling Calculator, Store, and Snipping Tool via winget..."
    winget install --id Microsoft.WindowsCalculator -e --silent
    winget install --id Microsoft.WindowsStore -e --silent
    winget install --id Microsoft.ScreenSketch -e --silent
} else {
    Write-Warning "`nWinget is not installed. Please install 'App Installer' from the Microsoft Store website manually if needed."
}

Write-Host "`n=== Done. Please RESTART your computer now. ==="

---
updated 3

# Step 3: Fix permissions on WindowsApps (SAFE method)
Write-Host "`nResetting permissions on WindowsApps folder..."

# Take ownership first
takeown /f "C:\Program Files\WindowsApps" /r /d Y

# Grant read/execute to ALL APPLICATION PACKAGES
icacls "C:\Program Files\WindowsApps" /grant "ALL APPLICATION PACKAGES":(RX) /t

# Restore SYSTEM full control
icacls "C:\Program Files\WindowsApps" /grant "SYSTEM":(F) /t

Write-Host "Permissions set safely."
@@@@@@@
# Step 3: Take ownership and fix permissions safely
Write-Host "`nAttempting to take ownership of WindowsApps folder..."

$folder = "C:\Program Files\WindowsApps"
$user = "$env:USERNAME"

# Take ownership
icacls "$folder" /setowner "$user" /T /C

# Grant minimal necessary access
icacls "$folder" /grant "$user":(RX) /T /C
icacls "$folder" /grant "ALL APPLICATION PACKAGES":(RX) /T /C
icacls "$folder" /grant SYSTEM:(F) /T /C

Write-Host "Ownership and permissions adjusted. Proceeding..."