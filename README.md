# Poweshell-acripts
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