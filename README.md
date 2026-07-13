Stage 1: Check tool and agent registration

Run these two commands:

Get-Content src\agents\base_llm_agent\agent.py

Then:

Get-Content src\agents\base_llm_agent\alphasense_tools.py | Select-Object -First 260

We need to confirm:

1. AlphaSense tools are imported in agent.py
2. Tools are attached to base_llm_agent
3. /run can call AlphaSense GenSearch

Send me the output/screenshots of these two files.
