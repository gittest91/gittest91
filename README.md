Step 1: Open PR link

Open this link from terminal output:

https://github.com/Allstate-Internal/inv-alphasense-agent/pull/new/Bala/alphasense
Step 2: Select correct branches

On PR page, make sure:

Base branch: dev
Compare branch: Bala/alphasense

Very important: base should be dev, not main/master.

Step 3: PR title

Use:

Bala/alphasense - AlphaSense OBO integration
Step 4: PR description

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
Step 5: After PR is created, send Sumanth this
Hi Sumanth,

I have raised the PR for AlphaSense OBO integration.

PR Link: <paste PR link>

Summary:
- Added numeric ALPHASENSE_TARGET_USER_ID support for OBO.
- Fixed companyUsers GraphQL query syntax.
- Added safe OBO token error handling.
- Updated GenSearch start and polling to use OBO token.
- Verified /run → base_llm_agent → AlphaSense gensearch → OBO → response flow successfully.

The OBO token generation and AlphaSense GenSearch through /run are working and returning AlphaSense content/citations.
Note about git warning

This warning is not blocking:

Your name and email address were configured automatically...

Commit and push already succeeded. Later, you can set correct Git identity if required.
