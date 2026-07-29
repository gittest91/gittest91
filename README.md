$params = @{
    Method      = "POST"
    Uri         = "http://localhost:8081/run"
    Headers     = $headers
    ContentType = "application/json"
    Body        = $body
}

$response = Invoke-RestMethod @params
$response | ConvertTo-Json -Depth 20
