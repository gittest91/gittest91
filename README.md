Get-Content .\src\resources\config-dev.yml | Select-String -Pattern "alphasense:|vault_key|UseOBO|obo_user_ids" -Context 0,8
