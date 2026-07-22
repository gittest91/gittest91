git ls-tree -r --name-only origin/beta-release | Select-String -Pattern "alphasense|obo|gensearch|vault|agent"

This will show the current file paths in beta-release.

Then search the current branch content for OBO terms:

git grep -n -i -e "onBehalfOfAccessToken" -e "ALPHASENSE_TARGET_USER_ID" -e "get_obo_token" -e "gensearch" origin/beta-release
How to interpret
