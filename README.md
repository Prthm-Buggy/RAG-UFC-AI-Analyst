# UFC-AI-Analyst
Ask any question about Fighters, fights, events and statistics. Engineering + RAG + tool-calling agent + UI

I created this project WITH COMPLETE OPEN SOURCE resources, built on Google Colab and using free Groq API key, using the gpt-oss-120b, so if you want to use this project, just change the dir links to your own folders and insert your own LLM API Key 

This is a hybrid RAG + SQL agent that answers natural-language questions about UFC fights, fighters, events, and statistics using a normalized fight database, vector search, and tool-calling using an LLM.

Tech Stack: 
- Pandas - for transformation and normalization 
- LangChain + LangGraph - for tool calling loop
- Gradio - for UI 
- DuckDB - For saving the normalized tables into a single highly compressed file 
- ChromaDB (for VectorStore) - To save document embeddings which could be semantically searched over 
- LLM - GPT-oss-120b - For reasoning and tool selection
- Embeddings - BAAI/bge-small-en - For creating document and query embeddings

A high level overview of the complete flow starting from the user query - 
<img width="824" height="1012" alt="image" src="https://github.com/user-attachments/assets/5192d03f-aed2-4cfa-b7e7-88d3294e22c6" />






