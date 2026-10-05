# AI Shopping Agent

A conversational shopping assistant built with Python, Streamlit, LangChain, and Groq. It helps users search products, filter by price and organic status, evaluate product ratings, and place orders through a simple chat interface.

The app also supports image-based shopping: you can upload a product photo and the agent will analyze it, find a matching product type, and search the store catalog for similar items.

## Features

- Search products by keyword, category, and description
- Filter by maximum price and organic preference
- Check average ratings and review counts
- Compare shortlisted items before buying
- Order a product after explicit confirmation
- Upload a product image to find visually similar items
- Built as a Streamlit app for quick local demos

## Tech Stack

- Python 3.14+
- Streamlit
- LangChain / LangChain Core
- Groq LLM API
- SQLite product catalog
- Python-dotenv

## Project Structure

```text
ai-shopping-agent/
├── .env.example
├── .env.schema
├── pyproject.toml
├── README.md
├── src/
│   └── ai_shopping_agent/
│       ├── app.py
│       ├── reviews_api.py
│       ├── shopping_agent.py
│       └── store.db
├── tests/
│   └── test_basic.py
└── .venv/   # local virtual environment
```

## Prerequisites

- Python 3.14 or newer
- A Groq API key
- Optional: Google AI or LangSmith keys if you want to extend the environment further

## Setup

1. Clone the repository and change into the project directory.

2. Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
```

3. Install project dependencies:

```bash
pip install --upgrade pip
pip install -e .
```

4. Copy the sample environment file and add your API key:

```bash
cp .env.example .env
```

Then update `.env` with your credentials, at minimum:

```env
GROQ_API_KEY=your_groq_api_key_here
```

You may also keep the optional keys in place if you are using the wider LangChain setup:

```env
GOOGLE_API_KEY=
LANGSMITH_API_KEY=
```

## Run the App

From the project root, start the Streamlit app:

```bash
streamlit run src/ai_shopping_agent/app.py
```

This launches the shopping assistant in your browser.

## Example Usage

Try prompts like:

- I want organic honey under $15 with a rating above 4.5
- Show me the best coffee beans under $20
- Find a non-organic olive oil with at least 4 stars
- Upload a product image and find similar items

After the assistant lists products, you can confirm your order by saying things like:

- yes
- order the first one
- buy product 3

## How It Works

The app is organized around a LangChain agent that exposes a set of tools:

- `search_products`: looks through the SQLite product catalog
- `get_rating`: fetches average rating and review counts
- `checkout`: creates an order only after explicit confirmation
- `describe_product_image`: analyzes an uploaded image and extracts product attributes

These tools are orchestrated by the agent in `src/ai_shopping_agent/shopping_agent.py`, while the Streamlit interface in `src/ai_shopping_agent/app.py` handles chat input and UI interactions.

## Testing

The project includes a basic smoke test:

```bash
pytest
```

## Notes

- The SQLite database lives under `src/ai_shopping_agent/store.db`.
- The app expects to be launched with the script path as shown above so the local module imports resolve correctly.
- This project is intended for local experimentation and product demos rather than production deployment.

## License

This project is provided as a learning/demo application. Add a license file if you intend to distribute it publicly.
