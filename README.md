POST http://localhost:8081/apps/base_llm_agent/users/test-user/sessions

{
  "state": {}
}


http://localhost:8081/run

{
  "app_name": "base_llm_agent",
  "user_id": "test-user",
  "session_id": "PASTE_SESSION_ID_HERE",
  "new_message": {
    "role": "user",
    "parts": [
      {
        "text": "Call the gensearch tool. Query: Compare Microsoft and Google business performance."
      }
    ]
  }
}
