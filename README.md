# NewsWise - Intelligent News Q & A Agent

An intelligent news Q&A agent built with LangChain and LangGraph. Using RAG (Retrieval Augmented Generation) to answer questions from BBC New articles (Source: Kaggle) with conversation memory.

## Features
- RAG Pipeline: Retrieves relevant BBC news articles using FAISS vector search
- LLM-powered answer: Using Claude (Anthropic) model to answer question from retrieved context (from RAG's retrieval)
- Conversation Memory: Remember previous question and answer across turns
- LangGraph Flow: Built with StateGraph production ready workflow
- MemorySaver: Persist graph state between interactions
- HuggingFaceEmbeddings: for semantic search

## Architecture

```
  User Question
       ↓
  [LangGraph StateGraph]
       ↓
  [ask] → get user input
       ↓
  [route] → /exit or continue
       ↓
  [answer] → RAG Chain
       ├── FAISS Retriever (top 3 articles)
       ├── ChatPromptTemplate + History
       └── Claude LLM → StrOutputParser
       ↓
  Loop back to [ask]
```

## Dataset
- Source: [BBC News Archive - Kaggle](https://www.kaggle.com/datasets/hgultekin/bbcnewsarchive)
- Size: `2,225 articles`
- Categories: `Business, Sport, Politics, Tech, Entertainment`
- Columns: `category, filename, title, content`

## Tech Stack
|-----|-------|
| Tool	| Purpose
| LangChain	| LLM chaining, prompt templates, RAG |
|LangGraph |	Agent flow, state management |
|Anthropic | Claude	LLM for answer generation |
|FAISS |	Vector store for semantic search |
|HuggingFace	| Sentence embeddings |
|Pandas	|Dataset loading and processing |
|-----|-------|

## Setup
1. Clone the repository
```bash
git clone https://github.com/yourusername/newswise.git
cd newswise
```

3. Install dependencies
```bash
pip install langchain langchain-anthropic langchain-community langchain-huggingface faiss-cpu langgraph sentence-transformers pandas
```
4. Set up API keys
Add to your environment or Google Colab secrets:
```bash
ANTHROPIC_API_KEY=your_anthropic_api_key
KAGGLE_USERNAME=your_kaggle_username
KAGGLE_KEY=your_kaggle_api_key
```

4. Download dataset
```bash
kaggle datasets download -d hgultekin/bbcnewsarchive
unzip bbcnewsarchive.zip
```

5. Run the notebook
Open `newswise.ipynb` in Google Colab or Jupyter and run all cells.

## Usage

```
Enter a Question: What happened in football?
Agent: Based on the provided context...

Enter a Question: Who was mentioned in the last answer?
Agent: Based on the previous answer...

Enter a Question: /exit
```

- Type any news-related question
- Type `/exit` to end the session

## Future Improvements
- [ ] Add category filter tool
- [ ] Swap MemorySaver to PostgreSQL for production
- [ ] Add Gradio UI for web interface
- [ ] Add source citation in answers
- [ ] Deploy to Hugging Face Spaces

## License
MIT License: free to use, modify and share.

## Acknowledgements
- BBC News Archive Dataset by Habib Gültekin on Kaggle
- LangChain and LangGraph teams
- Anthropic for Claude
