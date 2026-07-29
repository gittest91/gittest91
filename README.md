$session = Invoke-RestMethod `
    -Method POST `
    -Uri "http://localhost:8081/apps/$appName/users/$encodedUserId/sessions" `
    -Headers $headers `
    -ContentType "application/json" `
    -Body '{"state":{}}'

$sessionId = $session.id
$session
