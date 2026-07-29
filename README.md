$appName = "alphasense_agent"

$session = Invoke-RestMethod `
    -Method POST `
    -Uri "http://localhost:8081/apps/$appName/users/test-user/sessions" `
    -Headers $headers `
    -ContentType "application/json" `
    -Body '{"state":{}}'

$sessionId = $session.id

$session

Then prepare the request body:

$body = @{
    app_name   = $appName
    user_id    = "test-user"
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
