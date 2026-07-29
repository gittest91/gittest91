$sessionId = $session.id
Prepare the request body:
$body = @{
    app_name   = $appName
    user_id    = $userId
    session_id = $sessionId
    new_message = @{
        role = "user"
        parts = @(
            @{
                text = "Call the gensearch tool. Query: Compare Microsoft and Google business performance. Return the AlphaSense result with citations."
            }
        )
    }
} | ConvertTo-Json -Depth 10
Prepare the request:
$params = @{
    Method      = "POST"
    Uri         = "http://localhost:8081/run"
    Headers     = $headers
    ContentType = "application/json"
    Body        = $body
    TimeoutSec  = 300
}
Run the agent:
$response = Invoke-RestMethod @params
Display the response:
$response | ConvertTo-Json -Depth 30
Save the response:
$response |
ConvertTo-Json -Depth 30 |
Set-Content "alphasense_run_output.json" -Encoding UTF8
