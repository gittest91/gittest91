ALPHASENSE_TARGET_USER_ID=426695
ALPHASENSE_TARGET_EMAIL=ray.kramer@allstate.com
gc .env | ? { $_ -match '^\s*[^#].*=' } | % { $p = $_ -split '=',2; Set-Item -Path ("Env:" + $p[0].Trim()) -Value $p[1].Trim() }
echo $env:ALPHASENSE_TARGET_USER_ID
echo $env:ALPHASENSE_TARGET_EMAIL
