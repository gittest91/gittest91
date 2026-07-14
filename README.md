PR title
Bala/alphasense - AlphaSense OBO integration
PR description

Paste this:

Implemented and verified AlphaSense OBO integration.

Changes:
- Added numeric ALPHASENSE_TARGET_USER_ID support for OBO.
- Fixed companyUsers GraphQL query syntax.
- Added safe OBO token response/error handling.
- Ensured GenSearch start and polling both use OBO token.
- Added local-mode auth middleware bypass while keeping non-local auth intact.

Verified:
- App startup successful.
- Healthcheck working.
- Session creation working.
- /run invokes base_llm_agent.
- OBO token generation working.
- AlphaSense GenSearch through OBO reaches 100%.
- /run returns AlphaSense response with gensearch/functionResponse content.
