Stage 1: First fix .env consistency

Since OBO worked with Sumanth’s user ID, set both values correctly:

ALPHASENSE_TARGET_EMAIL=sboyina@allstate.com
ALPHASENSE_TARGET_USER_ID=509974

Save .env.

Then reload:

gc .env | ? { $_ -match '^\s*[^#].*=' } | % { $p = $_ -split '=',2; Set-Item -Path ("Env:" + $p[0].Trim()) -Value $p[1].Trim() }

Verify:

echo $env:ALPHASENSE_TARGET_EMAIL
echo $env:ALPHASENSE_TARGET_USER_ID

Expected:

sboyina@allstate.com
509974
Stage 2: Start app again

In server terminal:

$env:APP_ENV="local"
py app.py

Wait for:

Application startup complete
Uvicorn running on http://0.0.0.0:8081

Keep this terminal open.

Stage 3: Create new session

In new terminal:

Invoke-RestMethod -Method POST "http://localhost:8081/apps/base_llm_agent/users/test-user/sessions" `
  -ContentType "application/json" `
  -Body '{"state":{}}'

Copy the returned id.

Stage 4: Test /run with AlphaSense query

Use the new session id:

Invoke-RestMethod -Method POST "http://localhost:8081/run" `
  -ContentType "application/json" `
  -Body '{"app_name":"base_llm_agent","user_id":"test-user","session_id":"PASTE_SESSION_ID_HERE","new_message":{"role":"user","parts":[{"text":"Use AlphaSense gensearch to give a short summary comparing Microsoft and Google business performance. Include citations if available."}]}}'
Expected result

If tool calling works through /run, response should include AlphaSense-based content or tool execution events.
