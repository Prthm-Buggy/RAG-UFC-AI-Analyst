# UFC-AI-Analyst
Ask any question about Fighters, fights, events and statistics. Engineering + RAG + tool-calling agent + UI

I created this project WITH COMPLETE OPEN SOURCE resources, built on Google Colab and using free Groq API key, using the gpt-oss-120b 

This is a hybrid RAG + SQL agent that answers natural-language questions about UFC fights, fighters, events, and statistics using a normalized fight database, vector search, and tool-calling using an LLM.

Tech Stack: 
Pandas - for transformation and normalization 
LangChain + LangGraph - for tool calling loop
Gradio - for UI 
DuckDB - For saving the normalized tables into a single highly compressed file 
ChromaDB (for VectorStore) - To save document embeddings which could be semantically searched over 
LLM - GPT-oss-120b - For reasoning and tool selection
Embeddings - BAAI/bge-small-en - For creating document and query embeddings

A high level overview of the complete flow from user query to result - 
<img width="824" height="1012" alt="image" src="https://github.com/user-attachments/assets/5192d03f-aed2-4cfa-b7e7-88d3294e22c6" />
- The User asks the question from the gradio interface - the question can be statistical, a summary of an event, or description of a fighter, for ex - Summmarize UFC 300.
- The langchain agent passes the query to the LLM, the query ONLY gets embedded if we have to use the RAG agent to retrieve_documents, so we can use it for semantic search, else it just passes through the LLM directly to the other tools (run_sql_query, get_fight, etc)
- The LLM decides the tool to use based on the query, if its a summary question, it passes it to retrieve_documents, if statistical then to the other tools for creating an sql query, or it can utilize multiple tools based on the question.
- Then the flow goes either to
A. DuckDB (structured)
Which has Normalized tables built from the wide CSV:
fighters
events
fights
fight_performances (long format — one row per fighter per fight)
This powers exact numbers, rankings, and career stats
OR/AND to
B. Chroma (unstructured / semantic)
~12k generated natural-language documents:
Fight summaries
Event summaries
Fighter career docs
- Both stores come from the same raw wide CSV, just processed differently.



