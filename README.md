Write-Host "Session ID:" $sessionId
Then prepare the body again
$body = @{
    app_name   = $appName
    user_id    = $userId
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
