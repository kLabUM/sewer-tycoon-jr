SEWER TYCOON JR
Digitalwaterlab.org
See HTML file for workshop overview and the Sewer Tycoon Jr fame
See this  readme file for more advanced usecases 
Open Source, MIT License, 


## Stretch goals (beyond the competition): build the interfaces yourself

Finished the challenge, or want to go further? These extensions turn Sewer Tycoon Jr.
into the start of your own agentic workflow. Ask your coding agent to build them; you
should not need to write the code yourself.

### 1. Ground the storm in real open data
Ask your agent to pull recent hourly rainfall for Glasgow (latitude 55.86, longitude
-4.25) from a free open weather API such as Open-Meteo, which needs no key. Then ask it
to compare that rainfall with the design storm in `data/inflows.csv`: how big was the
biggest recent event, and would this system have overflowed?

Example prompt:
> Fetch the last 30 days of hourly rainfall for Glasgow from the Open-Meteo API. Plot it,
> find the largest 12-hour event, and compare it with the design storm in
> data/inflows.csv. Would our sewer have overflowed?

### 2. Turn the model into a tool
Ask your agent to wrap the grader as a tool that any LLM can call, for example an MCP
server (Model Context Protocol, a standard way to connect AI assistants to external
tools) with one function, `run_model(plan)`, that returns the overflow by outfall. Then
connect it to a chat assistant and ask the assistant to find a better plan using the tool.

Example prompt:
> Build a small MCP server in this repo that exposes one tool, run_model(plan), which
> calls stormline.grade.run and returns the result as JSON. Show me how to connect it to
> my AI assistant.

## Take it home

The same pattern works on your own system:

1. **Swap in your own model.** Replace `model/storm_line.inp` with your own SWMM model
   and point `stormline/grade.py` at your control elements (orifices, weirs, pumps) and
   the outfalls you care about.
2. **Define what "better" means.** Change the score in `grade.py`: overflow volume,
   flooding, energy use, water quality, or a mix.
3. **Write the rules down.** Edit `AGENTS.md` to describe your system, the decision
   variables and the constraints, so any coding agent can work on it safely.
4. **Let the agent loop,** and review its strategy before you trust it. The agent finds
   plans; engineers decide whether they are sensible.
