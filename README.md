Step 1: Create/switch to branch

Run:

git checkout -b Bala/alphasense

If it says branch already exists, run:

git checkout Bala/alphasense
Step 2: Add only required files

Run:

git add app.py src/agents/base_llm_agent/alphasense_client.py
Step 3: Check staged files

Run:

git status

You should see these two files under Changes to be committed:

modified: app.py
modified: src/agents/base_llm_agent/alphasense_client.py
Step 4: Commit

Run:

git commit -m "Add AlphaSense OBO support"
Step 5: Push branch

Run:

git push origin Bala/alphasense

After push, create PR:

Base branch: dev
Compare branch: Bala/alphasense

PR title:

Bala/alphasense - AlphaSense OBO integration

Run Step 1 to Step 3 first and send me git status output before commit.
