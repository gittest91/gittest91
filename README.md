$params = @{
    Method      = "POST"
    Uri         = "http://localhost:8081/run"
    Headers     = $headers
    ContentType = "application/json"
    Body        = $body
    TimeoutSec  = 300
}
2. Call the agent
$response = Invoke-RestMethod @params
