$response = Invoke-RestMethod -Method POST -Uri "http://localhost:8081/run" -Headers $headers -ContentType "application/json" -Body $body

Then print the result:

$response | ConvertTo-Json -Depth 20
