Step 2: Create request body

Copy-paste this:

$body = '{"app_name":"base_llm_agent","user_id":"test-user","session_id":"' + $sessionId + '","new_message":{"role":"user","parts":[{"text":"Use the AlphaSense gensearch tool to give a short summary comparing Microsoft and Google business performance. Include citations if available."}]}}'
Step 3: Call /run
$raw = Invoke-WebRequest -Method POST "http://localhost:8081/run" -ContentType "application/json" -Body $body -UseBasicParsing

This may take some time because AlphaSense GenSearch will run.

Step 4: Save output
$raw.Content | Set-Content run_output_raw.json -Encoding UTF8
Step 5: Check file size
Get-Item run_output_raw.json | Select-Object Name,Length

Expected: Length should be greater than 0.

Then open it:

code run_output_raw.json

Search inside for:

Microsoft

or

functionResponse

or

gensearch

Run Step 2–5 now and send me the file size output.
