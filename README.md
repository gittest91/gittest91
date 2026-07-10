Use this Copilot prompt now:

In src/agents/base_llm_agent/alphasense_client.py, add support for ALPHASENSE_TARGET_USER_ID as a fallback/override for OBO.

Current issue:
The OBO smoke test reaches AlphaSense, but get_target_user_id_by_email() calls companyUsers and fails with:
"Request is not allowed - user does not have permission to fetch this information."

Required change:
1. Add a helper method inside AlphaSenseClient:

def resolve_target_user_id(self) -> int:
    - First check os.getenv("ALPHASENSE_TARGET_USER_ID")
    - If present, return int(ALPHASENSE_TARGET_USER_ID)
    - If not present, check os.getenv("ALPHASENSE_TARGET_EMAIL")
    - If email exists, call self.get_target_user_id_by_email(email)
    - If neither exists, raise RuntimeError with a clear message:
      "Set ALPHASENSE_TARGET_USER_ID or ALPHASENSE_TARGET_EMAIL for OBO."

2. Replace all direct usages of:
self.get_target_user_id_by_email(os.environ["ALPHASENSE_TARGET_EMAIL"])

with:
self.resolve_target_user_id()

3. Do not change existing authentication, OBO token generation, headers, GenSearch, or polling logic.

4. Do not log tokens or secrets.

After Copilot updates, run:

Select-String -Path src\agents\base_llm_agent\alphasense_client.py -Pattern "resolve_target_user_id|ALPHASENSE_TARGET_USER_ID|ALPHASENSE_TARGET_EMAIL"

Then send me that output.
