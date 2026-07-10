Stage 1: Run safe OBO smoke test

In the same terminal where .env is loaded, create a temporary test file:

@'
from src.agents.base_llm_agent.alphasense_client import AlphaSenseClient
import os

client = AlphaSenseClient()

email = os.environ["ALPHASENSE_TARGET_EMAIL"]
print("Target email loaded:", email)

target_user_id = client.get_target_user_id_by_email(email)
print("Target user id found:", target_user_id)

obo_token = client.get_obo_token(target_user_id)
print("OBO token generated:", bool(obo_token))
'@ | Set-Content test_obo_smoke.py

Then run:

py test_obo_smoke.py
Expected success output
