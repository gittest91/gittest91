Good. Now OBO code is reaching AlphaSense, but we hit a permission issue, not a coding syntax issue.

Current output:

Target email loaded: sboyina@allstate.com ✅
companyUsers request reached AlphaSense ✅
GraphQL error: Request is not allowed - user does not have permission to fetch this information ❌

Meaning: the service account/token can call AlphaSense, but it is not allowed to run companyUsers. AlphaSense OBO works by letting a service account call on behalf of a target user, and downstream calls use the target user’s entitlements. But to do our current flow, the service account must be allowed to resolve the user or we need the user ID directly.

What to do now

We have two options.

Option A: Ask team to allow companyUsers

Ask AlphaSense/team to allow this operation for the service account:

companyUsers
onBehalfOfAccessToken
GenSearch
Option B: Ask team for direct AlphaSense target user ID

If companyUsers is not allowed, ask them for the numeric AlphaSense user ID for:

sboyina@allstate.com

Then we can skip companyUsers lookup and directly call:

onBehalfOfAccessToken(targetUserId)
Message to send team

Send this:

Hi Team, OBO smoke test is reaching AlphaSense successfully, but the companyUsers lookup is failing with: “Request is not allowed - user does not have permission to fetch this information.”

Can you please confirm one of the following:
1. Enable/allow the companyUsers GraphQL operation for our AlphaSense service account, or
2. Provide the numeric AlphaSense target user ID for sboyina@allstate.com so we can skip companyUsers lookup and directly test onBehalfOfAccessToken.

We also need confirmation that onBehalfOfAccessToken and GenSearch are enabled for this service account.
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
