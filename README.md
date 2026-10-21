# UFC AI Analyst

### Your conversational AI assistant for UFC statistics, fighters, fights, and events.

Ask questions in natural language. Get answers powered by structured fight data, semantic search, and an LLM agent that selects the appropriate tools to answer your query.

**UFC AI Analyst** is an open-source project that combines Retrieval-Augmented Generation (RAG), SQL-based data analysis, and agentic AI in a single conversational interface.

<p align="center">
  <img src="https://github.com/user-attachments/assets/5192d03f-aed2-4cfa-b7e7-88d3294e22c6" alt="UFC AI Analyst architecture" width="720"/>
</p>

## What makes it different?

Traditional chatbots rely primarily on information learned during model training. UFC AI Analyst combines a language model with searchable documents and structured UFC data, allowing it to retrieve relevant context or query the database depending on the question.

- **Ask in natural language:** Query fighter profiles, fight history, events, and statistics without manually writing SQL.
- **Hybrid RAG + SQL:** Combine semantic document retrieval with structured database queries.
- **Agentic tool calling:** Use LangChain and LangGraph to orchestrate tool selection and response generation.
- **Structured data processing:** Transform and normalize data using Pandas and store it in DuckDB.
- **Semantic search:** Use ChromaDB and dense embeddings to retrieve relevant document context.
- **Interactive interface:** Explore the system through a Gradio-based chat interface.
- **Open-source workflow:** Run the project in Google Colab using the provided notebooks and your own API credentials.

## Architecture

The system follows a query-driven workflow:

1. **User query** — The user asks a question about a fighter, fight, event, or statistic.
2. **LLM agent** — The language model interprets the question and determines which available tool is appropriate.
3. **Tool execution** — The agent uses structured database queries, semantic retrieval, or other configured tools.
4. **Context and results** — Retrieved records and relevant document context are returned to the agent.
5. **Response generation** — The LLM converts the available evidence into a readable answer.
6. **Gradio UI** — The final response is displayed in the chat interface.

The exact execution path depends on the query and the tools configured in the notebooks.

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Pandas & NumPy | Data transformation and processing |
| DuckDB | Local analytical database for structured fight data |
| ChromaDB | Vector storage and semantic retrieval |
| BAAI/bge-small-en | Text and query embeddings |
| LangChain | LLM integrations and tool abstractions |
| LangGraph | Agent workflow and tool-calling orchestration |
| Groq API | Access to the configured language model |
| GPT-OSS-120B | Language model used for reasoning and tool selection |
| Gradio | Interactive user interface |
| Google Colab | Notebook-based execution environment |

## How the RAG + SQL approach works

### Structured retrieval

Structured questions are best answered using the normalized database.

Example questions:

- How many fights has a particular fighter won?
- What are the recorded statistics for a specific fight?
- Which events feature a particular fighter?
- Compare two fighters using available database statistics.

The agent can use the configured database tools to retrieve relevant records rather than relying entirely on the LLM's internal knowledge.

### Semantic retrieval

Semantic search helps locate relevant information from indexed documents based on meaning rather than requiring an exact keyword match.

Example questions:

- Find documents discussing a fighter's career.
- Retrieve relevant context about a particular fight.
- Search indexed material related to an event or fighter.

The embedding model converts text into vectors, and ChromaDB stores and searches those vectors.

### Agent orchestration

LangGraph coordinates the agent's execution flow. The model interprets the query, selects from the available tools, receives their results, and generates a response.

This allows the application to handle different types of questions through one conversational interface.

## Example Questions

Try questions such as:

- Who is Conor McGregor, and what fight statistics are available for him?
- What historical records are available for Jon Jones?
- Show the available statistics for a specific UFC event.
- Compare the recorded fight statistics of two fighters.
- Find relevant information about a fighter using the indexed documents.

**Note:** These are example prompts, not claims of verified outputs. Actual answers depend on the datasets, indexed documents, and tools available in your current setup.

## Getting Started

### Prerequisites

You will need:

- A Google account to use Google Colab.
- A Groq API key or credentials for the configured LLM provider.
- Access to the project's datasets, documents, and notebooks.
- Python dependencies listed in `requirements.txt`.

### 1. Clone the repository

```bash
git clone https://github.com/adiP66/UFC-AI-Analyst.git
cd UFC-AI-Analyst
```

### 2. Install dependencies

In a local Python environment, run:

```bash
pip install -r requirements.txt
```

Alternatively, install the dependencies in a Google Colab notebook:

```python
%pip install -r requirements.txt
```

### 3. Configure your API key

Create a Groq API key through the [Groq Console](https://console.groq.com/).

In your notebook, configure the API key using the environment-variable or secret-management approach supported by the existing code.

For example, in Colab:

```python
import os
from google.colab import userdata

os.environ["GROQ_API_KEY"] = userdata.get("GROQ_API_KEY")
```

Add `GROQ_API_KEY` to Colab Secrets before running this example.

**Security:** Never commit API keys, tokens, or other credentials to GitHub.

### 4. Configure dataset paths

Review the notebooks and update any dataset, document, or storage paths to match your environment.

If running in Colab, upload the required files or mount Google Drive as appropriate.

### 5. Run the notebooks

Open the notebooks in the `notebooks/` directory and execute them in the order required by their dependencies.

Follow the notebook workflow for data processing, database preparation, embedding generation, agent initialization, and interface startup.

The exact notebook names and execution order should be taken from the current repository.

## Project Structure

```text
UFC-AI-Analyst/
├── data/           # UFC datasets and related data
├── documents/      # Documents used by the retrieval workflow
├── notebooks/      # Data processing, RAG, agent, and UI workflows
├── requirements.txt
└── README.md
```

The directories above reflect the repository's current top-level structure. The precise contents and responsibilities of individual notebooks may vary.

## Screenshots & Demonstrations

### Architecture

<p align="center">
  <img src="https://github.com/user-attachments/assets/5192d03f-aed2-4cfa-b7e7-88d3294e22c6" alt="System architecture and query flow" width="800"/>
</p>

### Sample questions and answers

The following screenshots illustrate example interactions with the application.

<p align="center">
  <img src="https://github.com/user-attachments/assets/b1e31f57-fc4b-4d30-b05d-008abb037c80" alt="Example AI analyst interaction" width="900"/>
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/6b9dc24e-9934-4356-a2d4-43f2cc9d6aac" alt="Example UFC question and answer" width="900"/>
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/ae48211c-94cf-43d2-8347-6fc83b017bf5" alt="Additional UFC AI Analyst example" width="900"/>
</p>

## Limitations

- Response quality depends on the completeness and accuracy of the available data.
- Semantic retrieval can miss relevant documents if they are not indexed or the retrieval configuration is unsuitable.
- LLM-generated answers can contain errors and should be checked against the underlying records.
- API availability, model limits, and execution costs depend on the selected provider and account.
- The project is not a guarantee of fight outcomes and should not be treated as professional betting advice.

## Future Improvements

Potential extensions include:

- Add automated data ingestion and refresh pipelines.
- Improve metadata filtering, chunking, and retrieval ranking.
- Add source references to make answers easier to verify.
- Evaluate retrieval quality and answer correctness using a test dataset.
- Add caching, query tracing, and latency monitoring.
- Deploy the Gradio interface as a hosted application.

## Contributing

Contributions, bug reports, and suggestions are welcome.

1. Fork the repository.
2. Create a feature branch.
3. Implement and test your changes.
4. Submit a pull request describing the change.

## License

Please refer to the repository's `LICENSE` file for the applicable license. If no license file exists, add one before explicitly granting reuse or redistribution rights.

## Disclaimer

This project is intended for educational, research, and analytical purposes. UFC statistics and AI-generated responses may be incomplete or incorrect. Predictions or interpretations should not be considered guarantees of future outcomes or financial advice.

---

**Built by [adiP66](https://github.com/adiP66)**

If you find this project useful, consider giving the repository a star or contributing improvements.
