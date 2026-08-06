# UFC-AI-Analyst
Ask any question about Fighters, fights, events and statistics. Engineering + RAG + tool-calling agent + UI

I created this project WITH COMPLETE OPEN SOURCE resources, built on Google Colab and using free Groq API key, using the gpt-oss-120b, so if you want to use this project, just change the dir links to your own folders and insert your own LLM API Key and run the notebooks one by one 

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

<img width="1994" height="599" alt="image" src="https://github.com/user-attachments/assets/b1e31f57-fc4b-4d30-b05d-008abb037c80" />

<img width="2053" height="669" alt="image" src="https://github.com/user-attachments/assets/6b9dc24e-9934-4356-a2d4-43f2cc9d6aac" />

<img width="1985" height="597" alt="image" src="https://github.com/user-attachments/assets/ae48211c-94cf-43d2-8347-6fc83b017bf5" />
