$sessionId = (Invoke-RestMethod -Method POST "http://localhost:8081/apps/base_llm_agent/users/test-user/sessions" -ContentType "application/json" -Body '{"state":{}}').id

$body = @{
    app_name="base_llm_agent"
    user_id="test-user"
    session_id=$sessionId
    new_message=@{
        role="user"
        parts=@(
            @{
                text="Call the gensearch tool. Query: Compare Microsoft and Google business performance. Return the AlphaSense result with citations."
            }
        )
    }
} | ConvertTo-Json -Depth 10

$raw = Invoke-WebRequest -Method POST "http://localhost:8081/run" `
    -ContentType "application/json" `
    -Body $body `
    -UseBasicParsing

$raw.StatusCode
