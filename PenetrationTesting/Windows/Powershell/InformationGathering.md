# Get-WmiObject
```powershell
Get-WmiObject -Class win32_OperatingSystem
```

# Get-Service
```powershell
Get-Service | ? {$_.Status -eq "Running}
```