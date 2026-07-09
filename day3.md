day3 learnings

memory why do we need it 
this is because our llm is stateless and every api call starts from zero and the only memory it have is the message we give it so in agent memory is the method of storing the information from the messages that we might need in our future convos

now there are 3 ways by which we can store memory 
1-conversation buffer:it is the messages list itself it takes alot of tokens if the message is burried deep in our messages so we use it just for recent turns current task like that 

2-key-value structered store:
this is a dict or sqlite table of explicit facts that are stored but one drawback in this is that the retrieval is an exact value match meaning if it is not an exact match the memory wont be used

3-vectorstore:
in this the text is stored in the form of embeddings and rag is used to retrieve the data in this we dont want the exact value match because the info is stored in the form of embeddings so the relative embedding to that value will be called in thsi way we get our result
