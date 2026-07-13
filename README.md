$sessionId = (Invoke-RestMethod -Method POST "http://localhost:8081/apps/base_llm_agent/users/test-user/sessions" -ContentType "application/json" -Body '{"state":{}}').id; $sessionId
