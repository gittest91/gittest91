Stage 1: Create test file

In the same terminal, run this command:

notepad test_obo_smoke.py

Notepad open hoga.

Paste this code inside Notepad:

from src.agents.base_llm_agent.alphasense_client import AlphaSenseClient
import os

client = AlphaSenseClient()

email = os.environ["ALPHASENSE_TARGET_EMAIL"]
print("Target email loaded:", email)

target_user_id = client.get_target_user_id_by_email(email)
print("Target user id found:", target_user_id)

obo_token = client.get_obo_token(target_user_id)
print("OBO token generated:", bool(obo_token))

Save the file:

Ctrl + S

Close Notepad.

Stage 2: Run the file

Now in PowerShell run:

py test_obo_smoke.py
Expected success
Target email loaded: sboyina@allstate.com
Target user id found: <some id>
OBO token generated: True

Run this now and send me the output/error. This test will confirm whether target user lookup + OBO token generation is working.
