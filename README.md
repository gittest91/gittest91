.\.venv\Scripts\Activate.ps1

gc .env | ? { $_ -match '^\s*[^#].*=' } | % {
    $p = $_ -split '=',2
    Set-Item -Path ("Env:" + $p[0].Trim()) -Value $p[1].Trim()
}

$env:APP_ENV="local"

py app.py
