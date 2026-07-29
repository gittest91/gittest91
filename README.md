$appName = "alphasense_agent"
$userId = $env:ALPHASENSE_TARGET_USER_ID
$encodedUserId = [uri]::EscapeDataString($userId)

Then create a fresh session:

$session = Invoke-RestMethod `
    -Method POST `
    -Uri "http://localhost:8081/apps/$appName/users/$encodedUserId/sessions" `
    -Headers $headers `
    -ContentType "application/json" `
    -Body '{"state":{}}'

$sessionId = $session.id

Prepare the body:

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

Run:

$params = @{
    Method      = "POST"
    Uri         = "http://localhost:8081/run"
    Headers     = $headers
    ContentType = "application/json"
    Body        = $body
    TimeoutSec  = 300
}

$response = Invoke-RestMethod @params
$response | ConvertTo-Json -Depth 30
