git show origin/beta-release:src/agents/base_llm_agent/alphasense_client.py | Select-String -Pattern "resolve_target_user_id|ALPHASENSE_TARGET_USER_ID|get_obo_token|onBehalfOfAccessToken" -CaseSensitive:$false


git show origin/beta-release:app.py | Select-String -Pattern "APP_ENV|BearerAuthMiddleware" -CaseSensitive:$false
