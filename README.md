Get-Content .env |
Where-Object { $_ -match '^\s*[^#].*=' } |
ForEach-Object {
    $parts = $_ -split '=', 2
    Set-Item -Path ("Env:" + $parts[0].Trim()) -Value $parts[1].Trim()
}


$userId = $env:ALPHASENSE_TARGET_EMAIL

Write-Host "Testing with mapped user:" $userId

$encodedUserId = [uri]::EscapeDataString($userId)

$session = Invoke-RestMethod `
    -Method POST `
    -Uri "http://localhost:8081/apps/$appName/users/$encodedUserId/sessions" `
    -Headers $headers `
    -ContentType "application/json" `
    -Body '{"state":{}}'

$session
