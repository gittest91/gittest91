.\.venv\Scripts\Activate.ps1

gc .env | ? { $_ -match '^\s*[^#].*=' } | % {
    $p = $_ -split '=',2
    Set-Item -Path ("Env:" + $p[0].Trim()) -Value $p[1].Trim()
}

$env:APP_ENV="local"

py app.py


Do this first
1. Find the expected local token

Run this in PowerShell from the project folder:

git grep -n "DEVELOPMENT_TOKEN"

Also run:

git grep -n "Authorization"

and:

git grep -n "Bearer"

This will show:

the environment-variable name used by the middleware
whether the token must be sent as a Bearer token
whether there is a special local-development header
2. Check whether the token exists in your environment
Get-ChildItem Env: | Where-Object {
    $_.Name -match "TOKEN|AUTH|OAUTH"
}

Do not share the actual values in chat.

You can also check only the development token:

if ($env:DEVELOPMENT_TOKEN) {
    Write-Host "DEVELOPMENT_TOKEN is loaded"
} else {
    Write-Host "DEVELOPMENT_TOKEN is missing"
}

If it is missing, load your .env again:

Get-Content .env |
Where-Object { $_ -match '^\s*[^#].*=' } |
ForEach-Object {
    $parts = $_ -split '=', 2
    Set-Item -Path ("Env:" + $parts[0].Trim()) -Value $parts[1].Trim()
}

Then restart the application:

py app.py
3. Add the token in Postman

Open the session request, then go to:

Authorization → Type: Bearer Token

Enter the same local development token used by the application.

Postman should send:

Authorization: Bearer <your-development-token>

Do not manually type the word Bearer in the token field if Postman already adds it.

4. Send the request again

Use:

POST http://localhost:8081/apps/base_llm_agent/users/test-user/sessions

Under Body → raw → JSON, send:

{
  "state": {}
}

Expected result:

{
  "id": "..."
}

The status should be 200 or another successful 2xx response.

If Bearer Token still returns 403

Your middleware may expect a custom development-token header instead of standard Bearer authentication. Use the git grep output to confirm the exact header name. It may look similar to:

DEVELOPMENT_TOKEN: <token>

or:

X-Development-Token: <token>

Do not guess the header name; confirm it from the middleware code.
