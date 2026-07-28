# Activate virtual environment
.\.venv\Scripts\Activate.ps1

# Load all variables from .env into the current PowerShell session
Get-Content .env |
Where-Object { $_ -match '^\s*[^#].*=' } |
ForEach-Object {
    $parts = $_ -split '=',2
    Set-Item -Path ("Env:" + $parts[0].Trim()) -Value $parts[1].Trim()
}

$env:APP_ENV="local"; py app.py

Dev Token Authenticated

{
  "state": {}
}
$env:APP_ENV="local"; Write-Host "APP_ENV=$env:APP_ENV"; py app.py
