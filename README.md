# 🤖 Agentic AI Software Engineer

> An autonomous AI-powered software engineering system that generates fully functional web applications from natural language prompts using LangGraph and Claude.

[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![LangGraph](https://img.shields.io/badge/LangGraph-latest-green.svg)](https://github.com/langchain-ai/langgraph)
[![Claude API](https://img.shields.io/badge/Claude-Sonnet%204-orange.svg)](https://www.anthropic.com/claude)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Usage Examples](#usage-examples)
- [Configuration](#configuration)
- [Agent System](#agent-system)
- [Development](#development)
- [Testing](#testing)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [Roadmap](#roadmap)
- [License](#license)

## 🌟 Overview

Agentic AI Software Engineer is a multi-agent system inspired by tools like Devin and Lovable that can autonomously design, develop, test, and deploy web applications from simple text descriptions. Built on LangGraph for robust agent orchestration and powered by Claude Sonnet 4, it manages complex software engineering workflows with multiple specialized agents working in coordination.

### What Can It Build?

- ✅ Interactive calculators
- ✅ Todo list applications
- ✅ Dashboard interfaces
- ✅ Form builders
- ✅ Data visualization tools
- ✅ CRUD applications
- ✅ API-integrated apps
- ✅ Real-time collaborative tools

## ✨ Features

### Core Capabilities

- **Natural Language to Code**: Describe your app in plain English, get production-ready code
- **Multi-Agent Workflow**: Specialized agents for planning, architecture, coding, testing, and deployment
- **Intelligent Testing**: Automated static analysis, runtime testing, and integration validation
- **Self-Healing**: Debug agent automatically fixes errors and refines code
- **Full-Stack Support**: Generate both frontend (React) and backend (Node.js/Python) applications
- **Sandboxed Execution**: Safe code execution in isolated Docker containers
- **Iterative Refinement**: Learns from errors and improves output through feedback loops

### Technical Highlights

- **State Management**: LangGraph's robust state system for conversation memory
- **Context-Aware Generation**: Agents maintain architectural context across the workflow
- **Token Optimization**: Efficient prompting strategies to minimize API costs
- **Extensible Architecture**: Easy to add new agents or modify workflows
- **Comprehensive Logging**: Full observability with structured logging

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        User Prompt                               │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
                   ┌────────────────┐
                   │ Planning Agent │
                   └────────┬───────┘
                            │
                            ▼
                ┌──────────────────────┐
                │ Architecture Agent   │
                └──────────┬───────────┘
                           │
                           ▼
         ┌─────────────────────────────────────┐
         │   Code Generation Orchestrator      │
         │  ┌──────────┬──────────┬──────────┐ │
         │  │Frontend  │Backend   │Integration││
         │  │Agent     │Agent     │Agent      ││
         │  └──────────┴──────────┴──────────┘ │
         └─────────────────┬───────────────────┘
                           │
                           ▼
                   ┌───────────────┐
                   │ Testing Agent │
                   └───────┬───────┘
                           │
                    ┌──────┴──────┐
                    │             │
                    ▼             ▼
            ┌──────────┐   ┌─────────────┐
            │  Debug   │   │ Deployment  │
            │  Agent   │   │   Agent     │
            └────┬─────┘   └──────┬──────┘
                 │                │
                 └────────┬───────┘
                          │
                          ▼
                 ┌────────────────┐
                 │ Final Output   │
                 └────────────────┘
```

## 🚀 Installation

### Prerequisites

- Python 3.11 or higher
- Docker Desktop (for code execution)
- Anthropic API key
- Node.js 18+ (for generated applications)

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/agentic-ai-engineer.git
cd agentic-ai-engineer
```

### Step 2: Set Up Virtual Environment

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Configure Environment

Create a `.env` file in the root directory:

```env
ANTHROPIC_API_KEY=your_api_key_here
DOCKER_ENABLED=true
MAX_ITERATIONS=3
LOG_LEVEL=INFO
OUTPUT_DIR=./generated_apps
```

### Step 5: Verify Installation

```bash
python -m pytest tests/
```

## 🎯 Quick Start

### Basic Usage

```python
from agentic_engineer import AgenticEngineer

# Initialize the system
engineer = AgenticEngineer()

# Generate an application
result = engineer.create_app(
    prompt="Create a calculator app with basic operations and a clean UI"
)

# Access the generated code
print(f"App created at: {result.output_path}")
print(f"Status: {result.status}")
print(f"Components: {len(result.files)}")
```

### Command Line Interface

```bash
# Generate an app from command line
python -m agentic_engineer generate \
  --prompt "Build a todo list with local storage" \
  --output ./my-todo-app

# Run in interactive mode
python -m agentic_engineer interactive

# View detailed logs
python -m agentic_engineer generate \
  --prompt "Create a dashboard with charts" \
  --verbose
```

## 📝 Usage Examples

### Example 1: Simple Calculator

```python
engineer = AgenticEngineer()

result = engineer.create_app(
    prompt="""
    Create a calculator application with:
    - Basic operations (add, subtract, multiply, divide)
    - Clear and backspace buttons
    - Decimal support
    - Responsive design with a modern UI
    """
)

# Run the generated app
result.run_dev_server()
```

### Example 2: Todo List with Backend

```python
result = engineer.create_app(
    prompt="""
    Build a full-stack todo list application:
    - Add, edit, delete, and mark todos as complete
    - Filter by status (all, active, completed)
    - Persist data to a backend API
    - User authentication
    - Modern, clean interface
    """,
    config={
        "backend": "fastapi",
        "database": "sqlite",
        "auth": True
    }
)
```

### Example 3: Data Dashboard

```python
result = engineer.create_app(
    prompt="""
    Create a data visualization dashboard:
    - Display sample sales data in charts
    - Support bar, line, and pie charts
    - Interactive filters by date range
    - Responsive layout
    - Export data to CSV
    """,
    config={
        "libraries": ["recharts", "papaparse"]
    }
)
```

## ⚙️ Configuration

### System Configuration

Edit `config/system_config.yaml`:

```yaml
llm:
  model: "claude-sonnet-4-20250514"
  temperature: 0.2
  max_tokens: 4000

agents:
  max_iterations: 3
  timeout_seconds: 300
  
testing:
  static_analysis: true
  runtime_tests: true
  integration_tests: true
  
docker:
  enabled: true
  memory_limit: "2g"
  cpu_limit: "2"
  timeout: 120

output:
  format: "react-vite"
  include_tests: true
  include_docs: true
```

### Agent Configuration

Customize individual agents in `config/agents/`:

```yaml
# planning_agent.yaml
prompt_template: |
  Analyze this web app request: {user_prompt}
  
  Consider:
  1. Core functionality
  2. User experience
  3. Technical complexity
  4. Best practices
  
  Output structured JSON.

max_retries: 2
temperature: 0.3
```

## 🤖 Agent System

### Planning Agent
Analyzes user requirements and creates detailed specifications.

**Outputs:**
- Feature breakdown
- Complexity assessment
- Technology recommendations

### Architecture Agent
Designs the application structure and component hierarchy.

**Outputs:**
- File/folder structure
- Component relationships
- Data flow design
- API specifications

### Code Generation Agents

**Frontend Agent:**
- Generates React components
- Implements Tailwind CSS styling
- Sets up state management
- Creates routing logic

**Backend Agent:**
- Creates API endpoints
- Implements business logic
- Sets up data models
- Configures middleware

**Integration Agent:**
- Connects frontend to backend
- Implements API calls
- Sets up environment config

### Testing Agent
Validates code quality and functionality.

**Test Layers:**
- Static analysis (ESLint, type checking)
- Syntax validation
- Runtime testing
- Integration testing

### Debug Agent
Fixes errors and refines code iteratively.

**Capabilities:**
- Root cause analysis
- Targeted fixes
- Regression prevention

### Deployment Agent
Packages the application for delivery.

**Outputs:**
- Bundled code
- Documentation
- Setup instructions
- Deployment configuration

## 🛠️ Development

### Project Structure

```
agentic-ai-engineer/
├── src/
│   ├── agents/
│   │   ├── planning.py
│   │   ├── architecture.py
│   │   ├── code_generation.py
│   │   ├── testing.py
│   │   ├── debug.py
│   │   └── deployment.py
│   ├── orchestrator/
│   │   ├── graph.py
│   │   └── state.py
│   ├── utils/
│   │   ├── docker_runner.py
│   │   ├── file_manager.py
│   │   └── logger.py
│   └── templates/
│       ├── calculator/
│       └── todo/
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/
├── config/
│   ├── system_config.yaml
│   └── agents/
├── generated_apps/
├── requirements.txt
├── setup.py
└── README.md
```

### Adding a New Agent

```python
from src.agents.base import BaseAgent
from src.orchestrator.state import ProjectState

class CustomAgent(BaseAgent):
    def __init__(self, llm):
        super().__init__(llm, "custom_agent")
    
    def execute(self, state: ProjectState) -> ProjectState:
        # Implement agent logic
        result = self.llm.invoke(self.build_prompt(state))
        
        # Update state
        state["custom_field"] = result.content
        return state
    
    def build_prompt(self, state: ProjectState) -> str:
        return f"Process: {state['user_prompt']}"
```

### Running Tests

```bash
# Run all tests
pytest

# Run specific test suite
pytest tests/unit/test_planning_agent.py

# Run with coverage
pytest --cov=src tests/

# Run end-to-end tests
pytest tests/e2e/ -v
```

## 🧪 Testing

### Unit Tests

```python
def test_planning_agent():
    agent = PlanningAgent(mock_llm)
    state = {"user_prompt": "Create a calculator"}
    
    result = agent.execute(state)
    
    assert "requirements" in result
    assert len(result["requirements"]) > 0
```

### Integration Tests

```python
def test_full_workflow():
    engineer = AgenticEngineer()
    result = engineer.create_app(
        prompt="Simple counter app"
    )
    
    assert result.status == "success"
    assert os.path.exists(result.output_path)
```

## 🔧 Troubleshooting

### Common Issues

**Issue: Docker connection failed**
```bash
# Check Docker is running
docker ps

# Restart Docker Desktop
# On Linux: sudo systemctl restart docker
```

**Issue: API rate limits**
```python
# Adjust configuration
config = {
    "llm": {
        "max_retries": 5,
        "retry_delay": 2
    }
}
```

**Issue: Generation timeout**
```yaml
# Increase timeout in config/system_config.yaml
agents:
  timeout_seconds: 600
```

### Debug Mode

```python
engineer = AgenticEngineer(debug=True)
result = engineer.create_app(
    prompt="Your app description",
    verbose=True
)

# Check logs
engineer.export_logs("./debug_logs.json")
```

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for details.

### Development Workflow

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Add tests for new functionality
5. Run the test suite (`pytest`)
6. Commit your changes (`git commit -m 'Add amazing feature'`)
7. Push to the branch (`git push origin feature/amazing-feature`)
8. Open a Pull Request

## 🗺️ Roadmap

### Version 1.0 (Current)
- [x] Basic multi-agent workflow
- [x] Frontend-only application generation
- [x] Testing and debugging capabilities
- [x] Calculator and todo list templates

### Version 1.1 (Q2 2026)
- [ ] Full-stack application support
- [ ] Database integration
- [ ] Authentication templates
- [ ] Visual refinement interface

### Version 2.0 (Q3 2026)
- [ ] React Native support
- [ ] Custom component library learning
- [ ] Version control integration
- [ ] Collaborative editing

### Future Considerations
- [ ] AI code review
- [ ] Performance optimization suggestions
- [ ] Automated deployment to cloud platforms
- [ ] Multi-language support (Vue, Angular, Svelte)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- LangGraph team for the excellent orchestration framework
- Anthropic for Claude API
- The open-source community for inspiration and tools

## 📞 Support

- **Documentation**: [docs.yourdomain.com](https://docs.yourdomain.com)
- **Issues**: [GitHub Issues](https://github.com/yourusername/agentic-ai-engineer/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/agentic-ai-engineer/discussions)
- **Email**: support@yourdomain.com

## 📊 Stats

![GitHub stars](https://img.shields.io/github/stars/yourusername/agentic-ai-engineer?style=social)
![GitHub forks](https://img.shields.io/github/forks/yourusername/agentic-ai-engineer?style=social)
![GitHub issues](https://img.shields.io/github/issues/yourusername/agentic-ai-engineer)
![GitHub pull requests](https://img.shields.io/github/issues-pr/yourusername/agentic-ai-engineer)

---

*Transforming ideas into applications, one prompt at a time.*
