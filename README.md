What to do

Open this link:

https://github.com/Allstate-Internal/inv-alphasense-agent/compare/dev...Bala%2Falphasense?expand=1

Then on GitHub:

Base: dev
Compare: Bala/alphasense
Click: Create pull request

After PR is created, GitHub will give a link like:

https://github.com/Allstate-Internal/inv-alphasense-agent/pull/123

That /pull/123 link is what you should send to Sumanth.

Message:

Hi Sumanth,

I have raised the PR for AlphaSense OBO integration.

PR Link: <paste actual /pull/number link here>

Summary:
- Added numeric ALPHASENSE_TARGET_USER_ID support for OBO.
- Fixed companyUsers GraphQL query syntax.
- Added safe OBO token error handling.
- Updated GenSearch start and polling to use OBO token.
- Verified /run → base_llm_agent → AlphaSense gensearch → OBO → response flow successfully.
