Step 2: Create body

Run only this:

$body = @{ app_name="base_llm_agent"; user_id="test-user"; session_id=$sessionId; new_message=@{ role="user"; parts=@(@{ text="Call the gensearch tool. Query: Compare Microsoft and Google business performance. Return the AlphaSense result with citations." }) } } | ConvertTo-Json -Depth 10
Step 3: Call /run

Run only this:

$raw = Invoke-WebRequest -Method POST "http://localhost:8081/run" -ContentType "application/json" -Body $body -UseBasicParsing

Wait until it completes.

Step 4: Check status

Run:

$raw.StatusCode

Expected:

200
Step 5: Save output

Run:

$raw.Content | Set-Content run_output_raw.json -Encoding UTF8

Then:

Get-Item run_output_raw.json | Select-Object Name,Length

Length should be greater than 0.

Step 6: Open output

Run:

code run_output_raw.json

Search inside file for:

gensearch
functionResponse
Microsoft
citations
