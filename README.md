Add AlphaSense Managed Vault integration and OBO configuration
Suggested PR description
## Summary

Implemented and validated AlphaSense Managed Vault and OBO configuration changes.

## Changes

- Verified AlphaSense credentials are retrieved from Managed Vault.
- Added/updated the required OBO user configuration.
- Confirmed AlphaSense authentication using the Vault-provided credentials.
- Completed local end-to-end validation using Postman and PowerShell.
- Prepared local testing and Managed Vault/OBO documentation.

## Validation completed

- Application started successfully.
- Development Token authentication succeeded.
- Session creation returned HTTP 200.
- OBO user mapping resolved successfully.
- GenSearch completed from 0% to 100%.
- `/run` returned HTTP 200.
- AlphaSense response included citations.
- All 5 automated tests passed.
- The generated coverage report for the executed test suite showed 100%.

## Notes

- Generated test output files were not committed.
- No AlphaSense credentials or Development Tokens were added to the repository.
