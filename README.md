Yes, I see the issue. In your file first line has:

import os

But the error says line 22:

print("OBO token generated:", bool(obo_token)
SyntaxError: '(' was never closed

In Notepad screenshot, it looks correct, but maybe file is not saved properly or one closing bracket is missing in actual file.

Let’s make it clean using terminal instead of manual typing.

Stage 1: Overwrite test file correctly

Copy-paste this full PowerShell command:

@'
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
'@ | Set-Content test_obo_smoke.py
Stage 2: Confirm file content

Run:

Get-Content test_obo_smoke.py

Check last line should be exactly:

print("OBO token generated:", bool(obo_token))

There should be two closing brackets at the end:

))
Stage 3: Run again
py test_obo_smoke.py
