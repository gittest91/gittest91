POST

http://localhost:8081/apps/alphasense_agent/users/sboyina/sessions

Body

{
  "state": {}
}

You should get

200 OK

Copy the returned

id

(session id)

3. Call /run
POST

http://localhost:8081/run

Body

{
  "app_name": "alphasense_agent",
  "user_id": "sboyina",
  "session_id": "<SESSION_ID>",
  "new_message": {
    "role": "user",
    "parts": [
      {
        "text": "Call the gensearch tool. Query: Compare Microsoft and Google business performance."
      }
    ]
  }
}
