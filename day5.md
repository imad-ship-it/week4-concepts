day5 learnings

plugins why do we need them
till now every skill like web search or calculator was hardcoded inside the agent so if i want to add a new ability i have to open the agent code and change it. plugins fix this, a plugin is a separate piece of code that lives outside the agent and the agent discovers it and loads it at runtime so the agent code never changes we just drop a new file and the agent gets a new ability

how a plugin works
every plugin follows the same contract meaning it has the same shape like a name, a description and a run function. the agent has a plugin loader that scans a folder finds the plugin files loads them and registers them into the tool list automatically. this is why the contract matters if every plugin looks the same the loader can treat them all the same way without knowing what is inside them
the description is still the most important part just like in function calling because the llm picks which plugin to use only by reading the description not the code

multi step reasoning
a single llm call answers in one shot but real tasks need more than one step like first search then calculate then summarize. in multi step reasoning the agent breaks the goal into smaller steps and does them one by one, the output of one step becomes the input of the next step

how it works in the loop
the agent plans the steps first then executes step 1 observes the result then decides what step 2 should be based on that result and keeps going, this is why it is stronger than a fixed workflow because the plan can change in the middle if a step fails or gives something unexpected the agent replans instead of crashing
for example if i ask what is the population of france times 2 the agent first uses web search to get the population thats step 1 then it takes that number and uses the calculator thats step 2 then gives the final answer, one call alone cant do this because the calculator needs the search result first

when to stop
the agent needs a stopping condition otherwise it loops forever, it stops when the goal is reached or when it hits a max step limit so a stuck agent doesnt burn tokens forever
