Meanwhile, we can prepare fallback code

We can add support for:

ALPHASENSE_TARGET_USER_ID=

Logic:

If ALPHASENSE_TARGET_USER_ID exists → use it directly
Else → use ALPHASENSE_TARGET_EMAIL and companyUsers lookup

This is best because then both paths work.

Next technical step

Ask Copilot to update alphasense_client.py with fallback:

Add support for ALPHASENSE_TARGET_USER_ID. If it exists, use that integer directly and do not call companyUsers. If it does not exist, fall back to ALPHASENSE_TARGET_EMAIL and get_target_user_id_by_email().

Copilot prompt:

In src/agents/base_llm_agent/alphasense_client.py, add support for ALPHASENSE_TARGET_USER_ID.

Currently OBO flow resolves target_user_id using:
os.environ["ALPHASENSE_TARGET_EMAIL"] and get_target_user_id_by_email(), which calls companyUsers.

companyUsers is currently not allowed for our service account. Please add a helper method resolve_target_user_id() that:
1. Checks os.getenv("ALPHASENSE_TARGET_USER_ID")
2. If present, returns int(ALPHASENSE_TARGET_USER_ID)
3. Otherwise uses ALPHASENSE_TARGET_EMAIL and get_target_user_id_by_email(email)
4. Raises a clear error if neither is provided.

Then replace direct usages of:
self.get_target_user_id_by_email(os.environ["ALPHASENSE_TARGET_EMAIL"])
with:
self.resolve_target_user_id()

Do not change existing auth, OBO token, or GenSearch logic.

But for actual test, we still need either companyUsers permission or ALPHASENSE_TARGET_USER_ID.
