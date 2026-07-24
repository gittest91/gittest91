git branch --show-current
git status

Expected branch:

feature/alphasense-vault-integration

Now list only the AlphaSense variable names from .env:

Get-Content .env |
Where-Object { $_ -match '^\s*ALPHASENSE_[A-Z0-9_]+\s*=' } |
ForEach-Object { ($_ -split '=', 2)[0].Trim() }
