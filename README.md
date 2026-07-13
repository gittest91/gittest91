import os
import importlib.util
from pathlib import Path
import traceback

module_path = Path(__file__).parent / "src" / "agents" / "base_llm_agent" / "alphasense_client.py"

spec = importlib.util.spec_from_file_location("alphasense_client_direct", module_path)
module = importlib.util.module_from_spec(spec)
spec.loader.exec_module(module)

AlphaSenseClient = module.AlphasenseClient

client = AlphaSenseClient()

try:
    print("Target user ID:", os.environ.get("ALPHASENSE_TARGET_USER_ID"))
    print("Target email:", os.environ.get("ALPHASENSE_TARGET_EMAIL"))

    prompt = "Give a short summary of Microsoft and Google business performance."
    print("Starting GenSearch...")

    conversation_id = client.auto(prompt)
    print("Conversation ID:", conversation_id)

    print("Waiting for result...")
    result = client.wait_for_result(conversation_id, mode="auto", timeout=180)

    print("GenSearch completed.")
    print("Result:")
    print(result.get("markdown") or result)

except Exception:
    print("Full traceback:")
    traceback.print_exc()
