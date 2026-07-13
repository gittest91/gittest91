Step 1: New session create karo

Run:

$session = Invoke-RestMethod -Method POST "http://localhost:8081/apps/base_llm_agent/users/test-user/sessions" `
  -ContentType "application/json" `
  -Body '{"state":{}}'

$session.id

Ye ek new session id print karega.

Step 2: /run raw response save karo

Now run this full command:

$body = @{
  app_name = "base_llm_agent"
  user_id = "test-user"
  session_id = $session.id
  new_message = @{
    role = "user"
    parts = @(
      @{
        text = "Use the AlphaSense gensearch tool to give a short summary comparing Microsoft and Google business performance. Include citations if available."
      }
    )
  }
} | ConvertTo-Json -Depth 20

$raw = Invoke-WebRequest -Method POST "http://localhost:8081/run" `
  -ContentType "application/json" `
  -Body $body `
  -UseBasicParsing

$raw.StatusCode
$raw.Content | Set-Content run_output_raw.json -Encoding UTF8
Get-Item run_output_raw.json | Select-Object Name,Length

Expected:

200
Name                Length
----                ------
run_output_raw.json some-big-number
Step 3: Open output

Run:

code run_output_raw.json

Then search inside file:

Microsoft

or

functionResponse

or

gensearch
Step 4: If still empty

Run this command and send me output:

$raw.StatusCode
$raw.Content.Length
$raw.Content.Substring(0, [Math]::Min(1000, $raw.Content.Length))

Important: don’t commit these files:

run_output.json
run_output_raw.json
test_obo_smoke.py
.env

Your server logs already confirmed /run → AlphaSense OBO → Progress 100%; now we are only capturing the readable response properly.
