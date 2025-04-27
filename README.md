# google-adk-voice-to-visualization-agent

This project is a voice-powered AI agent built with Google ADK. You just say what kind of chart or analysis you need like “Show a bar chart of forecast by channel”, and the agent takes care of the rest.

It’s a fun way to explore your data without typing a single line! Talking is faster than writing, and LLMs are better at interpreting our ramblings than we are at organizing them into structured text, especially when those ramblings require specialized skills, like crafting the perfect prompt to generate correct SQL from a data question.

![YouTube Video](https://www.youtube.com/watch?v=IRqqnE_v7N0)

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
3. *Setup the session and runner*:

```
session_service = InMemorySessionService()
app_name = "viz_app"
user_id = "jeny"
session_id = "session_viz_001"
session = session_service.create_session(app_name=app_name, user_id=user_id, session_id=session_id)

runner = Runner(agent=root_agent, app_name=app_name, session_service=session_service)
```
4. *Record a question towards your data*
```
record_on_enter("question.wav")
```
5. *Transcribe & refine the question into a proper data query*
```
transcribed_text = transcribe_audio("question.wav")
refined_prompt = refine_prompt(transcribed_text)

combined_prompt = f"Use file: data_export.xlsx\n{refined_prompt}"

user_message = Content(role="user", parts=[Part(text=combined_prompt)])
```
6. *Run the agent*
```
for event in runner.run(user_id=user_id, session_id=session.id, new_message=user_message):
    if event.is_final_response():
        if event.content and event.content.parts:
            print(event.content.parts[0].text)
        else:
            print("No final text response was returned by the agent.")
```
7. *Choose your LLM*
```
llm = LiteLlm(model="openai/gpt-4o", temperature=0.0 )
```
8. *Agent set-up*
```
root_agent = Agent(
    name="voice_viz_agent",
    model=llm,
    description="Agent to create data visualizations from spoken queries.",
    instruction="(full ReAct-style instructions + tool usage strategy here)",
    tools=[preview_excel_structure, complex_duckdb_query, create_visualization],
    output_key="last_agent_response",
)
```
