$headers = @{
    Authorization = "Bearer $devToken"
}
Step 5: Create a Session

Run:

$session = Invoke-RestMethod `
    -Method POST `
    -Uri "http://localhost:8081/apps/base_llm_agent/users/test-user/sessions" `
    -Headers $headers `
    -ContentType "application/json" `
    -Body '{"state":{}}'

$session
