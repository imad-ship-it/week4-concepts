day4 learnings

hooks why do we need them
an agent calls tools on its own so we cant see what it is doing, hooks are functions that fire automatically at lifecycle events like pre_tool (before a tool runs) and post_tool (after it finishes) so we get observability without touching the tool code itself

how we built it
we made a registry which is just a dict of event name -> list of functions, register_hook adds a function to an event and fire(event, payload) runs all functions registered for that event. important thing is fire wraps every hook in try/except because a broken hook should never crash the agent

logging
we registered 2 built in hooks, log_pre_tool writes the tool name and args before it runs and log_post_tool writes the result preview, duration and error after. each event goes as one json line into tool_calls.log (jsonl format) so later we can read the file and see exactly what the agent did, which tools it called, how long each took and if it failed

in execute_tool we fire pre_tool at start, run the tool inside try/except so errors go back to the agent as text instead of crashing, then fire post_tool with the duration measured by time.perf_counter

there is also a decorator version @hooked_tool that wraps any function so hooks fire around it automatically, we didnt use it in the agent since execute_tool fires hooks manually for all tools in one place
