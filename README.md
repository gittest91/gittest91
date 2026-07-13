In src/agents/base_llm_agent/alphasense_client.py, fix get_target_user_id_by_email() to safely handle companyUsers results where email may be missing, None, or not a string.

Current failing line:
active_users = [u for u in users if u["email"].lower() == email.lower() and u.get("isActive")]

Error:
TypeError: 'builtin_function_or_method' object is not subscriptable

Please update the logic to:
- Iterate users normally
- Use user_email = str(u.get("email") or "").lower()
- Compare with email.lower()
- Check u.get("isActive") is True
- Return the first matching active user's id
- If none found, raise RuntimeError(f"No active user found for email {email}")

Do not change OBO token, auth, _gql, or GenSearch logic.
