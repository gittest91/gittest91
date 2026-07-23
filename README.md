Select-String `
  -Path ".\.venv\Lib\site-packages\python_appfabric_vault\vault.py" `
  -Pattern "class VaultBuilder|def build|def get_secured_data|approle|ldap|SecuredData" `
  -Context 3,10

Also run:

Get-Content `
  .\src\inv_alphasense_agents\alphasense_agent\alphasense_client.py `
  -First 40
