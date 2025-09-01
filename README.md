# Local RAG AI Agent for Restraunt queries

This repository contains the code for building a local AI agent using Python, featuring Retrieval Augmented Generation (RAG) capabilities. The agent allows you to query local documents, such as CSV or PDF files, to get contextually relevant answers from a locally run Large Language Model (LLM). This entire setup is completely free and runs on your local machine, eliminating the need for OpenAI or other cloud accounts.

✨ Features

*   **Local LLM**: Utilizes Ollama to run open-source models (like Llama 3.2) directly on your computer, leveraging your own hardware.
*   **Retrieval Augmented Generation (RAG)**: Integrates a vector store (ChromaDB) to retrieve relevant information from your documents before generating a response with the LLM.
*   **Vector Search Database**: Employs ChromaDB as a local vector database for efficient similarity searches.
*   **LangChain Integration**: Uses the LangChain framework to orchestrate the LLM, prompting, and vector database interactions.
*   **Data Ingestion**: Processes CSV files (and can be extended to other document types) to create an embeddable and searchable knowledge base.
*   **Interactive Querying**: Allows continuous questioning of the AI agent through a simple command-line interface.

## 🚀 Project Demo

The project demonstrates building an AI agent that can answer questions about a restaurant based on a CSV file containing reviews.

**Example Scenario:**
Imagine you have a CSV file named `realistic_restaurant_reviews.csv` with columns like `title`, `date`, `rating`, and `review`.

1.  **Question**: "How is the quality of the pizza?"
    *   The agent retrieves relevant reviews from the CSV file.
    *   It analyzes these reviews and provides a conclusion based on the actual feedback, e.g., mentioning potential room for improvement in presentation and consistency.

2.  **Question**: "Are there vegan options?"
    *   The agent searches the reviews for mentions of vegan options.
    *   It concludes that based on the reviews, there appears to be at least one vegan pizza and possibly more, highlighting both positive and negative feedback regarding vegan choices.

This setup ensures that the AI's responses are grounded in the provided document, reducing hallucinations and providing more accurate, data-driven answers.

## 🛠️ Technologies Used

*   **Python**: The core programming language.
*   **Ollama**: For running large language models and embedding models locally.
*   **LangChain**: A framework for developing applications powered by language models.
*   **ChromaDB**: A lightweight, in-memory vector database for storing and querying document embeddings.
*   **Pandas**: A data manipulation and analysis library for reading CSV files.

## ⚙️ Setup and Installation

Follow these steps to get your local AI agent up and running.

### 1. Project Setup

1.  **Create a Project Folder**:
    Open your code editor (e.g., VS Code) and create a new folder for your project (e.g., `local-ai-agent`).

2.  **Add Your Data**:
    Place your CSV file (e.g., `realistic_restaurant_reviews.csv`) into this new folder. You can also adapt the code for other data types later.

3.  **Create `requirements.txt`**:
    In your project folder, create a file named `requirements.txt` and add the necessary dependencies.

### 2. Python Environment Setup

1.  **Create a Virtual Environment**:
    Open your terminal or command prompt, navigate to your project directory, and create a virtual environment using Python's `venv` module.

2.  **Activate the Virtual Environment**:
    Activate the newly created virtual environment. The command differs slightly between Windows and Mac/Linux.

3.  **Install Python Dependencies**:
    With your virtual environment activated, install the libraries listed in your `requirements.txt` file. You can also install them individually.

### 3. Ollama Setup

Ollama allows you to run LLMs locally.

1.  **Download and Install Ollama**:
    Go to [Ollama.com](https://ollama.com/) and download the appropriate software for your operating system. Install it according to the instructions.

2.  **Verify Ollama Installation**:
    Open a new terminal (or the same one, ensuring Ollama is accessible) and type `ollama`. You should see Ollama's help message.

3.  **Pull Ollama Models**:
    You will need an LLM and an embedding model. Pull the Llama 3.2 model for the LLM and the Nomic Embed Text model for embeddings. You can verify the installed models by running `ollama list`.

### 4. Code Files

Create two Python files in your project directory: `main.py` and `vector.py`.

#### `vector.py`

This file handles the document embedding and vector store creation. It loads your CSV file, defines the embeddings model, and sets up the ChromaDB vector store. It checks if the database already exists to avoid re-embedding documents unnecessarily. It prepares documents by combining relevant text fields (like title and review) for search and includes metadata (like rating and date). Finally, it creates a retriever to fetch relevant documents from the vector store based on a query.

#### `main.py`

This file contains the main application logic. It defines the Ollama LLM and a prompt template. It then sets up a LangChain chain to connect the prompt and the model. The script includes a main loop that continuously prompts the user for questions. For each question, it uses the retriever (imported from `vector.py`) to find relevant reviews, then passes these reviews and the user's question to the LLM to generate a response. The user can type 'Q' to quit the application.

## ▶️ Usage

1.  **Run the application**:
    Ensure your virtual environment is activated and Ollama is running in the background. Then, execute your `main.py` file using Python.

2.  **Initial Setup**:
    The first time you run the application, it will create a directory for your ChromaDB database and embed all your documents. This process might take some time depending on your data size and hardware. Subsequent runs will be faster as it will load the existing database.

3.  **Ask Questions**:
    Once the setup is complete, you'll be prompted to "Ask your question". Type your questions related to the restaurant reviews.
    *   Example: "How are the vegan options?"
    *   Example: "What do customers say about the ambiance?"

4.  **Quit**:
    Type `Q` (or `q`) and press Enter to exit the application.

## 📝 Customization

*   **CSV File**: You can easily replace your current CSV file with your own data. Remember to update the file name in the `vector.py` script.
*   **Page Content**: In `vector.py`, the `page_content` is created by combining fields from your CSV. Modify this to include any content you want the agent to use for querying.
*   **Metadata**: The `metadata` dictionary in `vector.py` can be updated to include other relevant information from your CSV that you want to retrieve but not necessarily query on.
*   **LLM Model**: In `main.py`, the LLM model can be changed to any other model you have pulled with Ollama (e.g., `mistral`, `llama2`), provided your hardware can run it.
*   **Number of Retrieved Documents**: In `vector.py`, the `search_kwargs={"k": 5}` parameter in the retriever definition controls how many top-matching documents are passed to the LLM. Adjust `k` to your preference.
*   **Prompt Template**: The `template` string in `main.py` can be modified to guide the LLM's behavior and response style.

## 🙏 Acknowledgements

This project was built following a tutorial that highlighted the utility of various tools, including GitHub Copilot for accelerating the coding process.


