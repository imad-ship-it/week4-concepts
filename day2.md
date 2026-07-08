day2 learnings

a skill is a code that gives the llms the abilities like web search, calculation, and read filoe through a path
an llm by itself can only do one thing u give it an input and it gives out an output so skills make it more capable in this way

function calling
in function calling u send the request which is our message and the tool definitions like query for websearch expreession for calculations path to read file like that 
then the deepseek decides that is the apikey which u have added in the code this can have 2 outcomes 1 that it knows the answer and gives it immediately or it decides it needs a tool so instead of an answer it responds with a tool use block and tells to use a block then the code executes and the websearch happens and gets the answer so we will get 2 things in the message block one is the tool that ran and the other the answer