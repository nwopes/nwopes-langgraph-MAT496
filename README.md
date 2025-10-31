![LangChain Academy](https://cdn.prod.website-files.com/65b8cd72835ceeacd4449a53/66e9eba1020525eea7873f96_LCA-big-green%20(2).svg)

## Introduction

Welcome to LangChain Academy! 
This is a growing set of modules focused on foundational concepts within the LangChain ecosystem. 
Module 0 is basic setup and Modules 1 - 4 focus on LangGraph, progressively adding more advanced themes. 
In each module folder, you'll see a set of notebooks. A LangChain Academy accompanies each notebook 
to guide you through the topic. Each module also has a `studio` subdirectory, with a set of relevant 
graphs that we will explore using the LangGraph API and Studio.

## Setup

### Python version

To get the most out of this course, please ensure you're using Python 3.11 or later. 
This version is required for optimal compatibility with LangGraph. If you're on an older version, 
upgrading will ensure everything runs smoothly.
```
python3 --version
```

### Clone repo
```
git clone https://github.com/langchain-ai/langchain-academy.git
$ cd langchain-academy
```

### Create an environment and install dependencies
#### Mac/Linux/WSL
```
$ python3 -m venv lc-academy-env
$ source lc-academy-env/bin/activate
$ pip install -r requirements.txt
```
#### Windows Powershell
```
PS> python3 -m venv lc-academy-env
PS> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
PS> lc-academy-env\scripts\activate
PS> pip install -r requirements.txt
```

### Running notebooks
If you don't have Jupyter set up, follow installation instructions [here](https://jupyter.org/install).
```
$ jupyter notebook
```

### Setting up env variables
Briefly going over how to set up environment variables. You can also 
use a `.env` file with `python-dotenv` library.
#### Mac/Linux/WSL
```
$ export API_ENV_VAR="your-api-key-here"
```
#### Windows Powershell
```
PS> $env:API_ENV_VAR = "your-api-key-here"
```

### Set OpenAI API key
* If you don't have an OpenAI API key, you can sign up [here](https://openai.com/index/openai-api/).
*  Set `OPENAI_API_KEY` in your environment 

### Sign up and Set LangSmith API
* Sign up for LangSmith [here](https://smith.langchain.com/), find out more about LangSmith
* and how to use it within your workflow [here](https://www.langchain.com/langsmith), and relevant library [docs](https://docs.smith.langchain.com/)!
*  Set `LANGSMITH_API_KEY`, `LANGSMITH_TRACING_V2=true` `LANGSMITH_PROJECT="langchain-academy"`in your environment 

### Set up Tavily API for web search

* Tavily Search API is a search engine optimized for LLMs and RAG, aimed at efficient, 
quick, and persistent search results. 
* You can sign up for an API key [here](https://tavily.com/). 
It's easy to sign up and offers a very generous free tier. Some lessons (in Module 4) will use Tavily. 

* Set `TAVILY_API_KEY` in your environment.

### Set up LangGraph Studio

* LangGraph Studio is a custom IDE for viewing and testing agents.
* Studio can be run locally and opened in your browser on Mac, Windows, and Linux.
* See documentation [here](https://langchain-ai.github.io/langgraph/concepts/langgraph_studio/#local-development-server) on the local Studio development server and [here](https://langchain-ai.github.io/langgraph/cloud/how-tos/studio/quick_start/#local-development-server). 
* Graphs for LangGraph Studio are in the `module-x/studio/` folders.
* To start the local development server, run the following command in your terminal in the `/studio` directory each module:

```
langgraph dev
```

You should see the following output:
```
- 🚀 API: http://127.0.0.1:2024
- 🎨 Studio UI: https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024
- 📚 API Docs: http://127.0.0.1:2024/docs
```

Open your browser and navigate to the Studio UI: `https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024`.

* To use Studio, you will need to create a .env file with the relevant API keys
* Run this from the command line to create these files for module 1 to 5, as an example:
```
for i in {1..5}; do
  cp module-$i/studio/.env.example module-$i/studio/.env
  echo "OPENAI_API_KEY=\"$OPENAI_API_KEY\"" > module-$i/studio/.env
done
echo "TAVILY_API_KEY=\"$TAVILY_API_KEY\"" >> module-4/studio/.env
```


## Link to the small changes made - 
  -> https://docs.google.com/document/d/1GxDRLjBIpy97MGehXe8wULZUENQ_S7Pnn2m6o1tc3Zc/edit?usp=sharing

## Module 1 - Motivation 
-> This lecture showed that single LLMs aren't enough for complex tasks—you need structured steps, or "chains," to get things done reliably. But the shift now is toward agents, where LLMs choose their own steps. LangGraph helps build these flexible systems by combining fixed control with LLM driven decisions, using graphs to design smarter, more autonomous agents.

## Module 1 - simple-graph.ipynb Learning Summary
**What I learned:** Built a simple LangGraph with 3 nodes and conditional edges. Learned how StateGraph uses TypedDict for state management, how nodes are Python functions that modify state, and how conditional edges enable dynamic routing between nodes based on custom logic or probability.

**Code modifications:** Changed from mood-based example (happy/sad) to a cooking decision graph (pasta/pizza), adjusted probability from 50/50 to 70/30 split, and personalized the initial input message.

## Module 1 - langsmith studio
**What I learned:** In this video I learnt how to operate on langsmith studio and how easy it makes it to visualise everything that is going on behind the scenes of the code and it helps with making it easier to understand workflows that would be much harder to do by just reading the code.

## Module 1 - chain.ipynb Learning Summary
**What I learned:** Learned how to build LangGraph chains using chat messages as state, bind tools to chat models for function calling, and use the add_messages reducer to append messages instead of overwriting them. MessagesState simplifies state management by pre-building message handling with reducers.

**Code modifications:** Changed conversation theme from ocean mammals to space exploration, replaced multiply tool with calculate_distance tool (speed × time), and personalized all message exchanges with my name and space-related content.

## Module 1 - router.ipynb Learning Summary
**What I learned:** Built a router agent that uses conditional edges and tools_condition to dynamically route between direct LLM responses or tool execution. Learned how ToolNode executes tool calls automatically and how the LLM decides when to call tools based on user input.

**Code modifications:** Changed multiply function to calculate_area function (length × width for rectangles), updated the example query to calculate room area instead of multiplication, and modified ToolNode to use the new calculate_area tool.

## Module 1 - agent.ipynb Learning Summary
**What I learned:** Built a ReAct agent that creates a loop between assistant and tools nodes, allowing the model to act (call tools), observe (receive tool output), and reason (decide next action). The agent can chain multiple tool calls sequentially until the task is complete, demonstrating autonomous decision-making.

**Code modifications:** Changed from arithmetic operations (add/multiply/divide) to unit conversion tools (Celsius to Fahrenheit, kilometers to miles, kilograms to pounds), updated system message for conversion tasks, and modified example to chain multiple unit conversions.

## Module 1 - agent-memory.ipynb Learning Summary
**What I learned:** Implemented persistent memory in agents using LangGraph's checkpointer (MemorySaver) to maintain conversation context across multiple invocations. Learned how thread_id enables stateful conversations by storing graph state checkpoints, allowing agents to reference previous interactions and maintain context.

**Code modifications:** Changed from arithmetic operations (add/multiply/divide) to string manipulation tools (uppercase, reverse, count characters), updated system message for string operations, and modified examples to demonstrate memory retention with text transformations.

## Module 2 - state-schema.ipynb Learning Summary
**What I learned:** Explored three different ways to define state schemas in LangGraph: TypedDict (type hints only), dataclass (structured data), and Pydantic (runtime validation). Learned that TypedDict and dataclass provide type hints but don't enforce at runtime, while Pydantic validates data and catches errors before execution.

**Code modifications:** Changed from name/mood theme to student/grade theme (A-F letter grades), updated all state definitions across TypedDict, dataclass, and Pydantic examples, adjusted probability split from 50/50 to 60/40, and personalized examples with my name.

## Module 2 - state-reducers.ipynb Learning Summary
**What I learned:** Learned how reducers control state updates in LangGraph by specifying how to handle concurrent updates from parallel nodes. Used operator.add for list concatenation, created custom reducers to handle None values, and explored add_messages reducer for message management including appending, rewriting (same ID), and removal with RemoveMessage.

**Code modifications:** Changed from generic foo integer to score tracking system (adding points: 10, 5, 15), updated all state variables from "foo" to "score", changed initial value from 1 to 50, modified message examples to space exploration theme with my name, and updated custom reducer to work with score lists.

## Module 2 - multiple-schemas.ipynb Learning Summary
**What I learned:** Learned how to use multiple state schemas in LangGraph including private state (for internal node communication not in graph output), and explicit input/output schemas to filter what keys are exposed. Input/output schemas act as filters to constrain graph interfaces while internal schemas can contain all working data.

**Code modifications:** Changed from generic foo/baz to student_score/bonus_points for private state example, updated question/answer/notes to student_name/grade/feedback for input/output schemas, personalized with my name "Akshat", and modified values to reflect a student grading system with scores and performance feedback.

## Module 2 - trim-filter-messages.ipynb Learning Summary
**What I learned:** Learned three techniques to manage long-running conversations and control token usage: using RemoveMessage with add_messages reducer to delete old messages from state, filtering messages by slicing before passing to the model, and trimming messages based on token count using trim_messages function with configurable strategies.

**Code modifications:** Changed conversation theme from ocean mammals to space exploration (Mars rovers, James Webb Space Telescope, International Space Station), updated all message exchanges from "Lance" to "Akshat", and personalized greetings while maintaining the same message filtering and trimming demonstrations.

## Module 2 - chatbot-summarization.ipynb Learning Summary
**What I learned:** Built a chatbot with conversation summarization to maintain compressed memory of long conversations without high token costs. Learned to use conditional logic to trigger summarization after a threshold (6 messages), incorporate summaries into prompts as context, and combine summarization with MemorySaver checkpointing for persistent multi-turn conversations across sessions using thread IDs.

**Code modifications:** Changed conversation from sports (49ers, Nick Bosa) to AI/technology interests (artificial intelligence, LangGraph framework), updated name from "Lance" to "Akshat", and personalized conversation topics while demonstrating the same summarization and memory persistence features.

## Module 2 - chatbot-external-memory.ipynb Learning Summary
**What I learned:** Learned how to use external databases (SQLite) for persistent checkpointing, enabling conversation memory that survives across notebook restarts and application sessions. Discovered that SqliteSaver can create in-memory databases (":memory:") or persistent databases on disk, and how state is automatically saved to the database and can be reloaded from disk even after kernel restarts.

**Code modifications:** Changed conversation from sports theme (49ers) to programming interests (Python and LangGraph), updated name from "Lance" to "Akshat", and personalized the chatbot conversation while demonstrating the same external memory persistence with SQLite database checkpointing.

## Module 3 - breakpoints.ipynb Learning Summary
**What I learned:** Learned how to implement human-in-the-loop workflows using breakpoints by compiling graphs with interrupt_before parameter to pause execution at specific nodes for user approval, debugging, or state editing. Discovered that invoking the graph with None input resumes from the last checkpoint, enabling interactive control over tool execution and agent actions.

**Code modifications:** Changed from arithmetic operations (multiply, add, divide) to practical unit conversions and health calculations (Celsius to Fahrenheit, kilometers to miles, BMI calculator), updated system message to personalize for "Akshat", and modified all example queries to demonstrate temperature conversion, distance conversion, and BMI calculation with breakpoint approval.

## Module 3 - streaming-interruption.ipynb Learning Summary
**What I learned:** Learned multiple streaming modes in LangGraph including stream_mode="values" (full state after each node), stream_mode="updates" (only state changes), and stream_mode="messages" (message-specific events). Discovered how to use astream_events to stream chat model tokens in real-time by filtering on_chat_model_stream events, enabling token-by-token output for better user experience.

**Code modifications:** Changed conversation from sports theme (49ers NFL team) to technology topics (quantum computing advancements), updated name from "Lance" to "Akshat", and modified API streaming examples from arithmetic operations (Multiply 2 and 3) to unit conversions (Convert 100 kilometers to miles) to align with personalized examples throughout Module 3.

## Module 3 - edit-state-human-feedback.ipynb Learning Summary
**What I learned:** Learned how to directly edit graph state after breakpoints using update_state method, either by appending new messages or overwriting existing ones by supplying message IDs. Discovered how to create a human_feedback node as a placeholder for user input, and use as_node parameter to apply state updates as if they came from a specific node, enabling seamless human-in-the-loop workflows.

**Code modifications:** Changed from arithmetic operations (multiply, add, divide) to unit conversion tools (Celsius to Fahrenheit, kilometers to miles, pounds to kilograms), updated system message to personalize for "Akshat", and modified all example queries from multiplication tasks to temperature, distance, and weight conversions to maintain consistency with Module 3 theme.

## Module 3 - dynamic-breakpoints.ipynb Learning Summary
**What I learned:** Learned how to implement dynamic breakpoints using NodeInterrupt to conditionally pause graph execution from within nodes based on custom logic, unlike static breakpoints set during compilation. Discovered that NodeInterrupt can pass messages explaining why execution paused, and that updating state is necessary to move past the interrupt, otherwise the graph remains stuck re-running the same node.

**Code modifications:** Changed character limit from 5 to 10, updated input examples from generic "hello world" to personalized names ("Akshat Srivastava" shortened to "Akshat") and tech terms ("LangGraph Framework" shortened to "LangGraph"), and enhanced step messages to be more descriptive about validation and processing stages.

## Module 3 - time-travel.ipynb Learning Summary
**What I learned:** Learned how to use LangGraph's time travel feature to view, replay, and fork from past graph states by accessing checkpoint history with get_state_history. Discovered that replaying executes from a saved checkpoint without changes, while forking allows editing state at a checkpoint (by supplying message ID to overwrite) and then executing with modified state, creating new branches in execution history.

**Code modifications:** Changed from arithmetic operations (multiply, add, divide) to unit conversion tools (Celsius to Fahrenheit, kilometers to miles, meters to feet), updated system message to personalize for "Akshat", and modified all example queries from multiplication tasks (Multiply 2 and 3, Multiply 5 and 3, Multiply 3 and 3) to various unit conversions (temperature, distance conversions) demonstrating replay and fork capabilities with practical examples.

## Module 4 - parallelization.ipynb Learning Summary
**What I learned:** Learned how to implement parallel node execution in LangGraph using fan-out and fan-in patterns, where multiple nodes can execute simultaneously and their results are combined. Discovered that when parallel nodes write to the same state key, a reducer (like operator.add) is required to combine updates, otherwise an InvalidUpdateError occurs. The graph automatically waits for all parallel nodes to complete before proceeding to the next step, and custom reducers can control the order of state updates.

**Code modifications:** Changed node names from generic labels (a, b, c, d) to a data analysis workflow (gather_data, analyze_temperature, analyze_distance, convert_units, generate_report), personalized the answer template with "for Akshat", and updated the example question from Nvidia earnings to quantum computing technology developments to align with the technology theme used throughout the course.