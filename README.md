Stage 2: Search current agent references

After that, run:

Get-ChildItem src\agents -Recurse -File | Select-String -Pattern "base_llm_agent|instruction|tools|alphasense|agent" -CaseSensitive:$false

Send me the output.

What we will do after this

Once we see the files, we will identify:

1. Where base_llm_agent is defined
2. Where the prompt/instruction is coming from
3. Whether tools folder exists
4. Whether AlphaSense client already exists
5. Where to add OBO client code

Start with only this first:

Get-ChildItem src\agents -Recurse -File
