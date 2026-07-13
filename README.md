What those logs mean
1. GET / HTTP/1.1 404 Not Found

This means something opened:

http://localhost:8081/

But your app does not have a / homepage route, so 404 is normal.

Use only:

http://localhost:8081/healthcheck
http://localhost:8081/docs
2. GET /login/login 404 Not Found

This is also not your OBO issue. Some browser/app tried to open a login route, but your local app does not have /login/login.

3. /main_static... 404 Not Found

These are static UI files the browser tried to load. They are not needed for our /run API test.

4. EventHub not configured

This is only logging/export warning:

EVENTHUB_CONNECTION_STRING not found

It does not block OBO.

5. LiteLLM completion model=gpt-5.1

This means the base agent responded using the LLM. But to confirm AlphaSense tool was used, we need to see logs like:

base_llm_agent.alphasense_client - generating obo token
Starting GenSearch
Progress: 100%

If those logs are missing, the agent may have answered directly instead of calling the gensearch tool.

What is done so far

Confirmed completed:

Local app running ✅
Healthcheck working ✅
Docs working ✅
Session creation working ✅
/run working ✅
OBO token generation working ✅
Standalone AlphaSense GenSearch with OBO working ✅
Agent has AlphaSense tools attached ✅

Now remaining:

Confirm /run response visibly contains AlphaSense tool output
Make agent reliably use gensearch tool
Clean test/output files
Commit only required code
Next step: Force /run to call AlphaSense tool

In the same API terminal, create a new session:

$sessionId = (Invoke-RestMethod -Method POST "http://localhost:8081/apps/base_llm_agent/users/test-user/sessions" -ContentType "application/json" -Body '{"state":{}}').id; $sessionId

Then run this stronger prompt:

$body = '{"app_name":"base_llm_agent","user_id":"test-user","session_id":"' + $sessionId + '","new_message":{"role":"user","parts":[{"text":"Call the gensearch tool. Query: Compare Microsoft and Google business performance. Return the AlphaSense result with citations."}]}}'

Now call /run and save output:

$raw = Invoke-WebRequest -Method POST "http://localhost:8081/run" -ContentType "application/json" -Body $body -UseBasicParsing
$raw.StatusCode
$raw.Content | Set-Content run_output_raw.json -Encoding UTF8
Get-Item run_output_raw.json | Select-Object Name,Length

Then open it:

code run_output_raw.json

Search inside:

gensearch
functionCall
functionResponse
Microsoft
citations

Also check server terminal for:

generating obo token
Progress: 100%

If the server logs show generating obo token and Progress: 100%, then /run → AlphaSense OBO → answer is confirmed.
