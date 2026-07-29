$appName = "alphasense_agent"
$userId = $env:ALPHASENSE_TARGET_EMAIL
$encodedUserId = [uri]::EscapeDataString($userId)

Write-Host "Testing with mapped user:" $userId
