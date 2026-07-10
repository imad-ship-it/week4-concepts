day4 learnings

hooks why do we need them
an agent calls tools on its own so we cant see what it is doing, hooks are functions that fire automatically at lifecycle events like pre_tool (before a tool runs) and post_tool (after it finishes) so we get observability without touching the tool code itself

how we built it
we made a registry which is just a dict of event name -> list of functions, register_hook adds a function to an event and fire(event, payload) runs all functions registered for that event. important thing is fire wraps every hook in try/except because a broken hook should never crash the agent

