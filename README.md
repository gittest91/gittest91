.\.venv\Scripts\Activate.ps1

gc .env | ? { $_ -match '^\s*[^#].*=' } | % {
    $p = $_ -split '=',2
    Set-Item -Path ("Env:" + $p[0].Trim()) -Value $p[1].Trim()
}

$env:APP_ENV="local"

py app.py




Step 2

Open Postman.

Create:

POST

http://localhost:8081/apps/base_llm_agent/users/test-user/sessions

Generate Session ID.

Step 3

Run

POST

http://localhost:8081/run

Body:

{
  "app_name": "base_llm_agent",
  "user_id": "test-user",
  "session_id": "...",
  "new_message": {
    "role": "user",
    "parts": [
      {
        "text": "Compare Microsoft and Google business performance."
      }
    ]
  }
}
