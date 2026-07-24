Run these commands:

git grep -n -E 'ALPHASENSE_(API_KEY|EMAIL|PASSWORD|CLIENT_ID|CLIENT_SECRET|TARGET_EMAIL|TARGET_USER_ID)'

Then run:

git grep -n -E 'os\.getenv\("ALPHASENSE_|os\.environ\[.*ALPHASENSE_'
