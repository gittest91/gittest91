Get-Content .env |
Where-Object { $_ -match '^\s*[^#][A-Za-z0-9_]+\s*=' } |
ForEach-Object { ($_ -split '=', 2)[0].Trim() }
