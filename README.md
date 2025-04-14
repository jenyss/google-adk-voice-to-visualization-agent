# google-adk-voice-to-visualization-agent

This project is a voice-powered AI agent built with Google ADK. You just say what kind of chart or analysis you need like “Show a bar chart of forecast by channel”, and the agent takes care of the rest.

It’s a fun way to explore your data without typing a single line! Talking is faster than writing, and LLMs are better at interpreting our ramblings than we are at organizing them into structured text, especially when those ramblings require specialized skills, like crafting the perfect prompt to generate correct SQL from a data question.

If you have any questions or would like to collaborate, feel free to reach out to me on [LinkedIn](https://www.linkedin.com/in/jenya-stoeva-60477249/). You're more than welcome!

## How It Works

1. Records and transcribes voice input using OpenAI Whisper
2. Refines spoken requests into structured prompts using GPT-4o
3. Loads Excel data and previews its structure
4. Generates SQL queries using DuckDB and matches user intent to schema
5. Builds Plotly visualizations (bar, line, pie, scatter, Sankey, etc.)
6. Uses ADK’s ToolContext to maintain state across tool invocations
7. Runs with your choice of LLM: GPT-4o, Gemini, Claude (via LiteLLM)

## How-To
To run the agent, follow these steps: 

1. *Install dependencies* (at the top of the Notebook)
2. *Add your API keys* to a ```.env``` file:
```
OPENAI_API_KEY=your_openai_key
GOOGLE_API_KEY=your_google_key
```
