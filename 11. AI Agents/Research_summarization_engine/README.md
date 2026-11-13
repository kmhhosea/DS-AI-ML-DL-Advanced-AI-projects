# Research Summarization Engine

This project researches a question by generating focused web searches, retrieving and summarizing pages, and combining the summaries into a structured report. It uses LangChain chains, OpenAI chat models, DuckDuckGo search, and HTTP/HTML scraping.

## How it works

The chain-based pipeline in `chain5.py` connects these stages:

1. `chain1.py` selects research-assistant instructions for the question.
2. `chain2.py` generates search queries.
3. `chain3.py` searches the web and returns result URLs.
4. `chain4.py` scrapes each page and summarizes its content.
5. `chain5.py` combines the summaries and asks the LLM to write the final report.

`research_engine_seq.py` contains a separate, sequential version of the workflow.
`prompts.py` defines the prompts, `llm_models.py` configures the chat model, and
`web_searching.py` and `web_scraping.py` provide the search and retrieval helpers.

## Requirements and configuration

- Python 3.10 or newer
- An OpenAI API key with access to the `gpt-5-nano` model
- Internet access for OpenAI requests, DuckDuckGo searches, and fetching web pages

From this directory, install the packages:

```powershell
python -m pip install -r requirements.txt
python -m pip install python-dotenv
```

`python-dotenv` is needed by `llm_models.py` but is not currently listed in
`requirements.txt`. Set `OPENAI_API_KEY` in your environment or in a local
`.env` file in this directory:

```text
OPENAI_API_KEY=your-api-key
```

Do not commit the `.env` file or share its contents.

## Run the workflows

Run commands from this project directory so the modules can be imported:

```powershell
python research_engine_seq.py
```

To run the chain-based workflow, use its example script:

```powershell
python tests/chain5_test.py
```

Both workflows make live LLM and web requests and may incur API charges.

## Test scripts

The files in `tests/` are currently manual example scripts, not isolated
automated tests: they execute at import time, make live network or LLM requests,
and do not contain test functions or assertions. In particular, running them
through `pytest` does not provide a reliable offline test suite. The individual
chain scripts can be run manually from the project directory (for example,
`python tests/chain1_test.py`), with the same API and internet requirements.
