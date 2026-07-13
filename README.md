$response | ConvertTo-Json -Depth 20 | Set-Content run_output.json
notepad run_output.json
