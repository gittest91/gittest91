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
