Stage 2A: Search OBO keywords in client

Run this command:

Select-String -Path src\agents\base_llm_agent\alphasense_client.py -Pattern "OBO|onBehalfOf|companyUsers|targetUserId|ALPHASENSE_TARGET_EMAIL|Bearer|Authorization|access_token|auth|token" -CaseSensitive:$false

This will tell us if OBO/token logic is already present.

Send me the output.

Stage 2B: Show top part of client file

Run this also:

Get-Content src\agents\base_llm_agent\alphasense_client.py | Select-Object -First 180

We need to see imports, env variables, auth function, _gql() function.

What we know from screenshot

Current file already has:

AlphaSense client exists ✅
GraphQL helper exists ✅
Company lookup exists ✅
Watchlist method exists ✅

But we still need to confirm:

Service auth exists?
OBO token generation exists?
companyUsers lookup exists?
Downstream _gql uses OBO token?
ALPHASENSE_TARGET_EMAIL is used?
