Get-ChildItem "$env:USERPROFILE\Downloads" -File |
Where-Object { $_.Name -match "vault|alphasense" } |
Select-Object Name, FullName
Get-ChildItem "$env:USERPROFILE\Desktop" -File |
Where-Object { $_.Name -match "vault|alphasense" } |
Select-Object Name, FullName
Get-ChildItem "$env:USERPROFILE\Documents" -Recurse -File -ErrorAction SilentlyContinue |
Where-Object { $_.Name -match "vault|alphasense" } |
Select-Object Name, FullName
