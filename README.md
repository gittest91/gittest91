Stage 1: Open first 60 lines of AlphaSense client

Run this:

Get-Content src\agents\base_llm_agent\alphasense_client.py | Select-Object -First 70

Look for:

COMPANY_USERS_QUERY

You will likely see something like:

Query CompanyUsers($query:String){

If yes, change Query to lowercase query.

Correct should be something like:

COMPANY_USERS_QUERY = """
query CompanyUsers($query: String) {
  companyUsers(query: $query) {
    users {
      id
      email
      username
      isActive
    }
  }
}
"""
Stage 2: Use Copilot prompt

Give Copilot this:

The OBO smoke test reaches AlphaSense /gql but companyUsers lookup fails with GraphQL parsing error: expected definition.

Please inspect COMPANY_USERS_QUERY in src/agents/base_llm_agent/alphasense_client.py. GraphQL operation keyword should be lowercase `query`, not `Query`. Fix the companyUsers GraphQL query syntax only. Do not change auth or OBO logic yet.
Stage 3: Run smoke test again

After fixing and saving:

py test_obo_smoke.py

Expected next success:

Target email loaded: sboyina@allstate.com
Target user id found: <id>
OBO token generated: True

If another error comes, send it. But this current one is clearly a GraphQL query syntax issue, not credentials issue.
