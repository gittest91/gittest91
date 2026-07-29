Get-ChildItem .\src\inv_alphasense_agents -Directory | Select-Object Name

Also run:

Get-ChildItem .\src\inv_alphasense_agents -Recurse -Filter "agent.py" |
Select-Object FullName
