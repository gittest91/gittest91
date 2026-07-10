Stage 2: Inspect AlphaSense client

Run this:

Get-Content src\agents\base_llm_agent\alphasense_client.py

Send me the output or screenshots.

Stage 3: Inspect AlphaSense tools

After that run:

Get-Content src\agents\base_llm_agent\alphasense_tools.py

Send output/screenshots.

Stage 4: Inspect agent definition

Then run:

Get-Content src\agents\base_llm_agent\agent.py
What we are checking now

We need to find:

1. Does alphasense_client.py use service auth?
2. Does it have companyUsers lookup?
3. Does it have onBehalfOfAccessToken?
4. Does it use OBO token in downstream GraphQL?
5. Are tools connected to base_llm_agent?
6. Does /run call AlphaSense tools or only normal LLM?

Start with only this:

Get-Content src\agents\base_llm_agent\alphasense_client.py
