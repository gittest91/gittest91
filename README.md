This is Python code bug, not permission issue. Most likely somewhere code has this type of mistake:

os.getenv["ALPHASENSE_TARGET_EMAIL"]   # wrong

instead of:

os.getenv("ALPHASENSE_TARGET_EMAIL")   # correct

or:

response.json["data"]   # wrong

instead of:

response.json()["data"] # correct
Do not run app.py now

You typed:

py app.py

Cancel it if it starts. Right now we need to debug test_obo_smoke.py.

Press:

Ctrl + C

if needed.

Step 1: Update test file to show full error line

Run:

notepad test_obo_smoke.py

Replace full file with this:

import os
import importlib.util
from pathlib import Path
import traceback

module_path = Path(__file__).parent / "src" / "agents" / "base_llm_agent" / "alphasense_client.py"

spec = importlib.util.spec_from_file_location("alphasense_client_direct", module_path)
module = importlib.util.module_from_spec(spec)
spec.loader.exec_module(module)

AlphaSenseClient = module.AlphaSenseClient

client = AlphaSenseClient()

try:
    email = os.environ["ALPHASENSE_TARGET_EMAIL"]
    print("Target email loaded:", email)

    target_user_id = client.resolve_target_user_id()
    print("Target user id found:", target_user_id)

    obo_token = client.get_obo_token(target_user_id)
    print("OBO token generated:", bool(obo_token))

except Exception:
    print("Full traceback:")
    traceback.print_exc()
