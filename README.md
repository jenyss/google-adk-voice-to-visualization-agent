# google-adk-voice-to-visualization-agent

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
