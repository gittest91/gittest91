In src/agents/base_llm_agent/alphasense_client.py, please fix GenSearch start to use OBO as well.

Current issue:
poll_conversation() now uses:
target_user_id = self.resolve_target_user_id()
data = self._gql(POLL_QUERY, {"conversationId": conversation_id}, target_user_id)

But gen_search() currently starts GenSearch using:
data = self._gql(MUTATIONS[mode], {"input": input_payload})

For correct OBO behavior, the initial GenSearch mutation must also use the same OBO target user.

Please update gen_search() so it does:
target_user_id = self.resolve_target_user_id()
data = self._gql(MUTATIONS[mode], {"input": input_payload}, target_user_id)

Do not change auth, headers, polling, or other tools.
Do not log tokens or secrets.



Get-Content src\agents\base_llm_agent\alphasense_client.py | Select-Object -Skip 485 -First 20

