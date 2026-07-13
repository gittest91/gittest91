Stage 2: Reload .env

Run this in terminal:

gc .env | ? { $_ -match '^\s*[^#].*=' } | % { $p = $_ -split '=',2; Set-Item -Path ("Env:" + $p[0].Trim()) -Value $p[1].Trim() }
Stage 3: Verify target email loaded

Run:

echo $env:ALPHASENSE_TARGET_EMAIL

Expected:

ray.kramer@allstate.com

Also run:

Test-Path Env:ALPHASENSE_TARGET_USER_ID

Expected for now:

False

If it says True, show me before running test.

Stage 4: Run OBO smoke test

Run:

py test_obo_smoke.py
