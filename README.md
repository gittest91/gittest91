AlphaSense Agent - Local End-to-End Testing Guide (Postman)
Prerequisites
- Valid Development Token from the team.
- Start the application using 'py app.py' and keep the terminal open.
1. Start the Application
Run:
py app.py

Expected:
- Application startup complete
- Uvicorn running on http://0.0.0.0:8081
2. Create Session in Postman
POST http://localhost:8081/apps/alphasense_agent/users/sboyina/sessions

Authorization:
Bearer Token = AGENTIC_DEVTOKEN

Body:
{
  "state": {}
}

Expected:
HTTP 200 OK and a returned 'id' (session_id).
3. Execute /run
POST http://localhost:8081/run

Authorization:
Bearer Token = <Development Token>

Body:
{
  "app_name":"alphasense_agent",
  "user_id":"sboyina",
  "session_id":"<SESSION_ID>",
  "new_message":{
    "role":"user",
    "parts":[
      {
        "text":"Call the gensearch tool. Query: Compare Microsoft and Google business performance. Return the AlphaSense result with citations."
      }
    ]
  }
}

Replace <SESSION_ID> with the value returned from Step 2.
Expected Results
Terminal:
- Progress 0% -> 100%
- POST /run HTTP/1.1 200 OK

Postman:
- HTTP 200 OK
- AlphaSense response
- GenSearch output
- Citations
Evidence to Capture
1. Application startup terminal.
2. Terminal showing Progress 100% and POST /run HTTP/1.1 200 OK.
3. Session API response (200 OK).
4. /run API response (200 OK with AlphaSense output).

