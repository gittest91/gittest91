Hi Sumanth,

I have raised the PR for AlphaSense OBO integration.

PR Link: https://github.com/Allstate-Internal/inv-alphasense-agent/pull/1

Summary:
- Added numeric ALPHASENSE_TARGET_USER_ID support for OBO.
- Fixed companyUsers GraphQL query syntax.
- Added safe OBO token error handling.
- Updated GenSearch start and polling to use OBO token.
- Added local-mode auth middleware bypass while keeping non-local auth intact.
- Verified /run → base_llm_agent → AlphaSense gensearch → OBO → response flow successfully.

The OBO token generation and AlphaSense GenSearch through /run are working and returning AlphaSense content/citations.
