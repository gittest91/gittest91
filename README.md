cd C:\Users\bdgwi\inv-agentic-platform\inv-alphasense-agent
Activate the virtual environment:
.\.venv\Scripts\Activate.ps1
Set Kyle’s development token:
$devToken = "PASTE_KYLE_TOKEN_HERE"
Create the header:
$headers = @{
    Authorization = "Bearer $devToken"
}
Set the correct app and mapped username:
$appName = "alphasense_agent"
$userId = "sboyina"
Create a fresh session:
$session = Invoke-RestMethod `
    -Method POST `
    -Uri "http://localhost:8081/apps/$appName/users/$userId/sessions" `
    -Headers $headers `
    -ContentType "application/json" `
    -Body '{"state":{}}'
Check the session:
$session
