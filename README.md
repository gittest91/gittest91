Get-ChildItem -Recurse -File | Where-Object {
    $_.Name -match "vault|alphasense"
} | Select-Object FullName

Then run:

Get-ChildItem .\src\inv_alphasense_agents\alphasense_agent -File | Select-Object Name
