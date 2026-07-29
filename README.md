$body = @{
    app_name = "base_llm_agent"
    user_id = "test-user"
    session_id = $sessionId
    new_message = @{
        role = "user"
        parts = @(
            @{
                text = "Call the gensearch tool. Query: Compare Microsoft and Google business performance."
            }
        )
    }
} | ConvertTo-Json -Depth 10
Step 2: Execute /run
$response = Invoke-RestMethod `
    -Method POST `
    -Uri "http://localhost:8081/run" `
    -Headers $headers `
    -ContentType "application/json" `
    -Body $body

$response
