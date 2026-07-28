Do this next
1. Check whether a development token is available locally

Run without displaying any secret value:

if ($env:DEVELOPMENT_TOKEN) {
    Write-Host "DEVELOPMENT_TOKEN is loaded"
} else {
    Write-Host "DEVELOPMENT_TOKEN is missing"
}

Also check whether .env contains the variable name:

Select-String -Path .env -Pattern "DEVELOPMENT_TOKEN"

Do not share its value.

2. Inspect the middleware to confirm how it accepts the token

Run:

py -c "import inspect; from investments_agentic_framework_adk.middleware import BearerAuthMiddleware; print(inspect.getsourcefile(BearerAuthMiddleware))"

Then:

py -c "import inspect; from investments_agentic_framework_adk.middleware import BearerAuthMiddleware; print(inspect.getsource(BearerAuthMiddleware))"

Search specifically inside the package:

Get-ChildItem .\.venv\Lib\site-packages -Recurse -File |
Select-String -Pattern "DEVELOPMENT_TOKEN" |
Select-Object Path, LineNumber, Line

This will tell us whether the local token should be sent as:

Authorization: Bearer <DEVELOPMENT_TOKEN>

or through another header.

If DEVELOPMENT_TOKEN exists

Restart the app after loading .env:

Get-Content .env |
Where-Object { $_ -match '^\s*[^#].*=' } |
ForEach-Object {
    $parts = $_ -split '=', 2
    Set-Item -Path ("Env:" + $parts[0].Trim()) -Value $parts[1].Trim()
}

$env:APP_ENV = "local"
py app.py

In Postman:

Authorization → Bearer Token

Paste the value of DEVELOPMENT_TOKEN only.

Then send:

POST http://localhost:8081/apps/base_llm_agent/users/test-user/sessions

Body:

{
  "state": {}
}
If DEVELOPMENT_TOKEN is missing

You need to obtain a valid JWT from the team’s approved authentication flow. Ask Nandita or Kyle:

For local Postman E2E testing of the AlphaSense Agent, should I use a DEVELOPMENT_TOKEN or obtain an OAuth JWT? Could you share the approved method or working Postman authentication configuration?

The JWT must match this audience:

http://inv-agentic-platform-dev.allstate.com

Do not use:

mock_valid_token

That is only a pytest fixture.

The immediate next action is to run the middleware inspection commands. They will confirm the exact local authentication method instead of guessing.
