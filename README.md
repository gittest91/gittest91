In src/agents/base_llm_agent/alphasense_client.py, improve get_obo_token() error handling.

Current issue:
get_obo_token() does:
return response.json()["data"]["onBehalfOfAccessToken"]["accessToken"]

But during OBO smoke test, response.json()["data"] is None and it fails with:
'NoneType' object is not subscriptable

Please update get_obo_token() to:
1. Store payload = response.json()
2. If payload contains "errors", raise RuntimeError with joined error messages.
3. Safely read payload.get("data", {}).get("onBehalfOfAccessToken", {}).get("accessToken")
4. If accessToken is missing, raise RuntimeError with clear message and include the response payload, but do not log or expose any tokens/secrets.
5. Keep the existing request, headers, and OBO query unchanged.
