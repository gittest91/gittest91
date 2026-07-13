Stage 1: Check file has content

Run:

Get-Item run_output.json | Select-Object Name,Length

If Length is very small or 0, then file did not save properly.

Stage 2: Search inside output

Run:

Select-String -Path run_output.json -Pattern "Microsoft|Google|AlphaSense|gensearch|functionCall|functionResponse|markdown|text" -CaseSensitive:$false
Stage 3: Open JSON properly in VS Code

Run:

code run_output.json

Then in VS Code search:

Microsoft

or:

functionResponse

or:

gensearch
If file is empty or no answer is visible

Run this complete command again:

$body = @{
  app_name = "base_llm_agent"
  user_id = "test-user"
  session_id = "fb592793-36dc-4ac3-a18c-fa2c39574ce8"
  new_message = @{
    role = "user"
    parts = @(
      @{
        text = "Use the AlphaSense gensearch tool to give a short summary comparing Microsoft and Google business performance. Include citations if available."
      }
    )
  }
} | ConvertTo-Json -Depth 10

$response = Invoke-RestMethod -Method POST "http://localhost:8081/run" `
  -ContentType "application/json" `
  -Body $body

$response | ConvertTo-Json -Depth 50 | Set-Content run_output.json
code run_output.json

Then search in run_output.json again.
