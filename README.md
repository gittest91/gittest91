@'
import os
import importlib.util
from pathlib import Path
import requests

module_path = Path(__file__).parent / "src" / "agents" / "base_llm_agent" / "alphasense_client.py"

spec = importlib.util.spec_from_file_location("alphasense_client_direct", module_path)
module = importlib.util.module_from_spec(spec)
spec.loader.exec_module(module)

AlphaSenseClient = module.AlphaSenseClient

client = AlphaSenseClient()

try:
    email = os.environ["ALPHASENSE_TARGET_EMAIL"]
    print("Target email loaded:", email)

    target_user_id = client.get_target_user_id_by_email(email)
    print("Target user id found:", target_user_id)

    obo_token = client.get_obo_token(target_user_id)
    print("OBO token generated:", bool(obo_token))

except requests.exceptions.HTTPError as e:
    print("HTTP error status:", e.response.status_code)
    print("HTTP error response:")
    print(e.response.text)

except Exception as e:
    print("General error:")
    print(type(e).__name__, str(e))
'@ | Set-Content test_obo_smoke.py
