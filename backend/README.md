# Backend API

FastAPI backend for Pool AI Knowledge Base with Google ADK (Agent Development Kit) integration.

## Setup

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Set up environment variables:
Create a `.env` file in the project root:
```bash
GOOGLE_API_KEY=your_api_key_here
OPENAI_API_KEY=your_openai_api_key_here  # Required for RAG functionality
```

You can get your API keys from:
- Google API key: [Google AI Studio](https://makersuite.google.com/app/apikey)
- OpenAI API key: [OpenAI Platform](https://platform.openai.com/api-keys)

Note: RAG functionality requires OPENAI_API_KEY. Without it, the system will use keyword matching instead.

3. Run the server:
```bash
python main.py
```

Or with uvicorn directly:
```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

## API Documentation

Once running, visit:
- Swagger UI: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc

## ADK Agents

This project includes several pre-configured ADK agents with different capabilities:

### Available Agents

1. **calculator** - Performs mathematical calculations
2. **time** - Provides current time information
3. **text** - Processes and formats text
4. **search** - Searches the web using Google Search
5. **multi** - Multi-tool agent with all capabilities

### API Endpoints

#### List Available Agents
```bash
GET /api/agents
```

#### Chat with an Agent
```bash
POST /api/chat
Content-Type: application/json

{
  "agent_name": "calculator",
  "message": "What is 25 * 4?",
  "stream": false
}
```

#### Get Agent Examples
```bash
GET /api/examples/{agent_name}
```

#### Get Agent Info
```bash
GET /api/agents/{agent_name}/info
```

### Example Usage

#### Using Python

```python
from adk_agents import get_agent

# Get an agent
agent = get_agent("calculator")

# Run a query
response = await agent.run("What is 25 * 4?")
print(response)

# Stream responses
async for chunk in agent.stream("Calculate 100 / 5"):
    print(chunk, end="")
```

#### Using the API

```bash
# List all agents
curl http://localhost:8000/api/agents

# Chat with calculator agent
curl -X POST http://localhost:8000/api/chat \
  -H "Content-Type: application/json" \
  -d '{
    "agent_name": "calculator",
    "message": "What is 25 * 4?"
  }'

# Get examples
curl http://localhost:8000/api/examples/calculator
```

### Running Examples

Run the example script to see all agents in action:

```bash
python examples.py
```

This will demonstrate:
- Calculator agent usage
- Time agent usage
- Text processing agent usage
- Search agent usage
- Multi-tool agent usage
- Streaming responses

## Custom Tools

The project includes several custom tools:

- `calculate(expression)` - Evaluates mathematical expressions
- `get_current_time(timezone)` - Gets current time
- `format_text(text, format_type)` - Formats text
- `word_count(text)` - Counts words and characters

You can create your own agents with these tools or add new custom tools.

## Project Structure

```
backend/
├── main.py              # FastAPI application
├── adk_agents.py        # ADK agent definitions
├── examples.py          # Usage examples
├── requirements.txt     # Dependencies
└── README.md           # This file
```
