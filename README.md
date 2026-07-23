Get-ChildItem C:\Users\bdugi -Recurse -File -Filter "alphasense_vault_example.py" -ErrorAction SilentlyContinue |
Select-Object FullName

If nothing appears, search more broadly:

Get-ChildItem C:\Users\bdugi -Recurse -File -ErrorAction SilentlyContinue |
Where-Object { $_.Name -match "vault.*example|alphasense.*vault" } |
Select-Object FullName

Once you find it, do not copy it into the repository yet. Open it using:

code "FULL_PATH_FROM_THE_RESULT"
