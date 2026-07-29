$sessionId = (Invoke-RestMethod -Method POST "http://localhost:8081/apps/base_llm_agent/users/test-user/sessions" -ContentType "application/json" -Body '{"state":{}}').id

$sessionId
Expected result: a session ID is printed.
2. Create /run Request Body
$body = @{ app_name="base_llm_agent"; user_id="test-user"; session_id=$sessionId; new_message=@{ role="user"; parts=@(@{ text="Call the gensearch tool. Query: Compare Microsoft and Google business performance. Return the AlphaSense result with citations." }) } } | ConvertTo-Json -Depth 10
3. Call /run
$raw = Invoke-WebRequest -Method POST "http://localhost:8081/run" -ContentType "application/json" -Body $body -UseBasicParsing
4. Check HTTP Status
$raw.StatusCode
Expected result: 200.
Expected Server Logs
In Terminal 1, the server logs should show the OBO and GenSearch flow completing.
generating obo token
Progress: 45%
Progress: 85%
Progress: 100%
POST /run HTTP/1.1 200 OK
Generate Output JSON File
$raw.Content | Set-Content run_output_raw.json -Encoding UTF8

Get-Item run_output_raw.json | Select-Object Name,Length

code run_output_raw.json
Search in run_output_raw.json
Search for the following keywords to confirm the AlphaSense tool response is present:
gensearch
functionResponse
Microsoft
citations
has content and contains gensearch/functionResponse/Microsoft/citations.
Cleanup After Demo
Remove-Item run_output_raw.json -ErrorAction SilentlyContinue

git status

