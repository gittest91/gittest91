git grep -n -i -e "os.getenv" -e "environ" -e "client_id" -e "client_secret" -e "username" -e "password" -- src/inv_alphasense_agents/alphasense_agent

Then display the AlphaSense client file:

Get-Content .\src\inv_alphasense_agents\alphasense_agent\alphasense_client.py
