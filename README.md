git grep -n -i -e "vault_key" -e '"alphasense"' -- .

Then run:

Get-ChildItem -Recurse -File |
Where-Object {
    $_.Extension -in ".json", ".yaml", ".yml", ".toml"
} |
Select-Object FullName
