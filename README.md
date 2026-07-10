Stage 1: Clean file list nikalo

Run this command:

Get-ChildItem src\agents -Recurse -File -Include *.py | Where-Object { $_.FullName -notmatch "__pycache__" } | Select-Object FullName

Send me output.

Stage 2: Check base_llm_agent folder

Run:

Get-ChildItem src\agents\base_llm_agent -Force

Send output.

Stage 3: Clean search only in .py files

Run this:

Get-ChildItem src\agents -Recurse -File -Include *.py | Where-Object { $_.FullName -notmatch "__pycache__" } | Select-String -Pattern "alphasense|base_llm_agent|instruction|tools|agent|OBO|onBehalfOf|companyUsers" -CaseSensitive:$false

This time output clean aayega.
