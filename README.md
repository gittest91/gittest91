Good. This error is not OBO failure.

Error reason:

PromptRegistry has not been initialized.

It happened because this import:

from src.agents.base_llm_agent.alphasense_client import AlphaSenseClient

first loads:

src/agents/base_llm_agent/__init__.py

and that imports agent.py, which expects app startup initialization. So direct import is triggering the full agent package.

We will bypass __init__.py and load only alphasense_client.py.

Stage 1: Replace test file

Run:

notepad test_obo_smoke.py

Delete old code and paste this:

import os
import importlib.util
from pathlib import Path

module_path = Path(__file__).parent / "src" / "agents" / "base_llm_agent" / "alphasense_client.py"

spec = importlib.util.spec_from_file_location("alphasense_client_direct", module_path)
module = importlib.util.module_from_spec(spec)
spec.loader.exec_module(module)

AlphaSenseClient = module.AlphaSenseClient

client = AlphaSenseClient()

email = os.environ["ALPHASENSE_TARGET_EMAIL"]
print("Target email loaded:", email)

target_user_id = client.get_target_user_id_by_email(email)
print("Target user id found:", target_user_id)

obo_token = client.get_obo_token(target_user_id)
print("OBO token generated:", bool(obo_token))

Save and close Notepad.

Stage 2: Run again
py test_obo_smoke.py

Expected success:

Target email loaded: sboyina@allstate.com
Target user id found: <id>
OBO token generated: True

If error comes, send exact
