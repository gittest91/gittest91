Get-ChildItem -Recurse -File -Force |
Where-Object {
    $_.FullName -notmatch '\\.git\\|__pycache__'
} |
Select-String -Pattern `
    'jwk-set-uri|jwks|audience|issuer|development.token|development_token|auth.bypass|skip.auth|oauth2|bearer|authorization' `
    -CaseSensitive:$false |
Select-Object Path, LineNumber, Line

Also inspect environment variable names without displaying their values:

Get-Content .env |
Where-Object { $_ -match '^[A-Za-z_][A-Za-z0-9_]*=' } |
ForEach-Object { ($_ -split '=', 2)[0] } |
Sort-Object
