Step 1: Keep server terminal open

Do not close the terminal where py app.py is running.

Server should be running at:

http://localhost:8081
Step 2: Open a new terminal

In VS Code:

Terminal → New Terminal

Use this new terminal for API commands.

Step 3: Create a new session

Run this single command:

$sessionId = (Invoke-RestMethod -Method POST "http://localhost:8081/apps/base_llm_agent/users/test-user/sessions" -ContentType "application/json" -Body '{"state":{}}').id; $sessionId

It should print a session ID like:

xxxxx-xxxx-xxxx-xxxx
Step 4: Create request body

Run this:

$body = '{"app_name":"base_llm_agent","user_id":"test-user","session_id":"' + $sessionId + '","new_message":{"role":"user","parts":[{"text":"Use the AlphaSense gensearch tool to give a short summary comparing Microsoft and Google business performance. Include citations if available."}]}}'
Step 5: Call /run

Run this:

$raw = Invoke-WebRequest -Method POST "http://localhost:8081/run" -ContentType "application/json" -Body $body -UseBasicParsing

This may take some time because AlphaSense GenSearch runs and polls.

Step 6: Check status

Run:

$raw.StatusCode

Expected:

200
Step 7: Save output to file

Run:

$raw.Content | Set-Content run_output_raw.json -Encoding UTF8

Then check file size:

Get-Item run_output_raw.json | Select-Object Name,Length

Expected: Length should be greater than 0.

Step 8: Open output file

Run:

code run_output_raw.json

Inside VS Code, search for:

Microsoft

or

functionResponse

or

gensearch

or

citations
Step 9: Check server logs also

In the server terminal, confirm you see something like:

generating obo token
Starting GenSearch
Progress: 100%
POST /run HTTP/1.1 200 OK
Do now

Start with only Step 3:

$sessionId = (Invoke-RestMethod -Method POST "http://localhost:8081/apps/base_llm_agent/users/test-user/sessions" -ContentType "application/json" -Body '{"state":{}}').id; $sessionId

Send me the session ID output, then we’ll do the /run call.
