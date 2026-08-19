# CampusOps AI

## Autonomous College Operations Manager

CampusOps AI is an **autonomous multi-agent AI system** designed to automate and optimize college operational activities such as classroom allocation, faculty scheduling, examination planning, resource management, and operational decision-making.

Unlike a traditional chatbot, CampusOps AI works as an **agentic system**. It understands a high-level goal, breaks it into smaller tasks, creates an execution plan, selects appropriate tools, executes operations, observes the results, verifies them, detects failures or conflicts, and automatically re-plans when required.

---

## Problem Statement

Managing college operations manually involves multiple interconnected activities:

* Classroom allocation
* Faculty scheduling
* Examination planning
* Resource management
* Timetable coordination
* Conflict resolution
* Operational decision-making

Manual processes can result in:

* Scheduling conflicts
* Room allocation errors
* Faculty clashes
* Resource underutilization
* Repeated manual work
* Delayed decision-making

CampusOps AI addresses these challenges using **Multi-Agent AI + Workflow Orchestration + Automated Verification + Replanning**.

---

## Objective

The primary objective of CampusOps AI is to build an autonomous system that can:

1. Understand a user's high-level operational goal.
2. Analyze the requirements.
3. Break the goal into smaller tasks.
4. Create an execution plan.
5. Assign tasks to specialized agents.
6. Select and use appropriate tools.
7. Execute operations automatically.
8. Observe execution results.
9. Verify the generated results.
10. Detect conflicts, errors, or missing information.
11. Re-plan failed tasks when necessary.
12. Provide a final verified result.

---

## Key Features

### Autonomous Task Planning

The system converts a high-level request into an actionable sequence of tasks.

Example:

> "Arrange classrooms for tomorrow's examinations."

The system can determine that it needs to:

* Identify examinations.
* Determine student counts.
* Check available classrooms.
* Check room capacities.
* Detect occupied rooms.
* Allocate suitable rooms.
* Verify the allocation.
* Resolve conflicts if required.

---

### Multi-Agent Architecture

CampusOps AI uses specialized agents instead of relying on a single AI component.

Main agents include:

* **Supervisor Agent**
* **Planner Agent**
* **Operations Agent**
* **Verifier Agent**
* **Replanner Agent**

Each agent has a specific responsibility within the workflow.

---

### Automatic Verification

Generated results are not directly accepted.

The Verifier Agent checks the output for:

* Conflicts
* Missing information
* Invalid assignments
* Resource constraints
* Scheduling problems
* Operational inconsistencies

---

### Automatic Replanning

If verification fails, the system does not simply return an error.

Instead:

```text
Execution
    ↓
Observation
    ↓
Verification
    ↓
Failure?
    ↓
Replanner Agent
    ↓
Updated Plan
    ↓
Re-execution
```

This enables the system to recover from operational failures.

---

## Agentic Workflow

```text
                USER GOAL
                    │
                    ▼
          ┌──────────────────┐
          │ Supervisor Agent │
          └────────┬─────────┘
                   │
                   ▼
          ┌──────────────────┐
          │  Planner Agent   │
          └────────┬─────────┘
                   │
                   ▼
              TASK QUEUE
                   │
          ┌────────┼─────────┐
          ▼        ▼         ▼
       Task 1    Task 2    Task 3
          │        │         │
          ▼        ▼         ▼
      Operations / Specialized Agents
                   │
                   ▼
                TOOLS
                   │
                   ▼
              OBSERVATION
                   │
                   ▼
          ┌──────────────────┐
          │  Verifier Agent  │
          └────────┬─────────┘
                   │
             ┌─────┴─────┐
             │           │
           PASS         FAIL
             │           │
             ▼           ▼
          RESULT     Replanner
                         │
                         ▼
                   Updated Plan
```

---

## How the System Works

### Step 1 — User Provides a Goal

The user provides a natural-language operational request.

Example:

```text
Allocate classrooms for tomorrow's exams.
```

### Step 2 — Supervisor Agent

The Supervisor Agent analyzes the request and determines what type of operation is required.

### Step 3 — Planner Agent

The Planner Agent decomposes the goal into smaller executable tasks.

Example:

```text
1. Retrieve examination schedule
2. Retrieve classroom information
3. Calculate required capacity
4. Allocate classrooms
5. Check conflicts
6. Verify allocation
```

### Step 4 — Task Execution

The appropriate operational agents execute the generated tasks using available tools and database operations.

### Step 5 — Observation

The system collects the results of each operation.

### Step 6 — Verification

The Verifier Agent checks whether the result satisfies the required constraints.

### Step 7 — Replanning

If a conflict or failure is detected, the Replanner Agent modifies the plan and the workflow continues.

### Step 8 — Final Result

Once the result passes verification, the system provides the final operational output.

---

## Technology Stack

| Technology   | Purpose                      |
| ------------ | ---------------------------- |
| Python       | Core application development |
| FastAPI      | Backend API                  |
| Streamlit    | Frontend / user interface    |
| LangGraph    | Agent workflow orchestration |
| LangChain    | LLM and agent integration    |
| SQLite       | Local database               |
| Pydantic     | Data validation              |
| Uvicorn      | FastAPI server               |
| Pandas       | Data processing              |
| LLM          | Natural-language reasoning   |
| Git & GitHub | Version control              |

---

## Project Architecture

```text
CampusOps-AI/
│
├── backend/
│   └── app/
│       ├── agents/
│       │   ├── supervisor/
│       │   ├── planner/
│       │   ├── operations/
│       │   ├── verifier/
│       │   └── replanner/
│       │
│       ├── state/
│       │   └── workflow_state.py
│       │
│       ├── workflow/
│       │   └── graph.py
│       │
│       ├── database/
│       │   └── database.py
│       │
│       ├── classrooms/
│       ├── registry/
│       ├── main.py
│       └── campusops.db
│
├── frontend/
│   └── streamlit_app.py
│
├── requirements.txt
├── README.md
└── .gitignore
```

> The exact folder structure may vary depending on the current implementation.

---

## Core Components

### Supervisor Agent

Responsible for understanding the user's request and coordinating the overall workflow.

**Responsibilities:**

* Understand user intent
* Identify required operation
* Coordinate agents
* Control workflow execution

---

### Planner Agent

Responsible for converting the high-level objective into executable tasks.

**Responsibilities:**

* Task decomposition
* Dependency identification
* Execution planning
* Task ordering

---

### Operations Agent

Responsible for performing actual college operational tasks.

Examples:

* Classroom allocation
* Schedule operations
* Faculty assignment
* Resource lookup
* Database operations

---

### Verifier Agent

Responsible for validating the result generated by other agents.

It checks:

```text
Is the task completed?
        ↓
Are constraints satisfied?
        ↓
Are there conflicts?
        ↓
Is information missing?
        ↓
Is the result valid?
```

---

### Replanner Agent

Responsible for recovery when the original plan fails.

It can:

* Identify the failure
* Analyze the cause
* Modify the plan
* Generate alternative tasks
* Restart execution

---

## Workflow State

The agents communicate through a shared workflow state.

A simplified state contains information such as:

```text
User Goal
    ↓
Current Plan
    ↓
Task Queue
    ↓
Completed Tasks
    ↓
Observations
    ↓
Verification Results
    ↓
Errors / Conflicts
    ↓
Final Result
```

This shared state allows different agents to coordinate during execution.

---

## Example Use Case

### User Request

```text
Allocate classrooms for the upcoming examination.
```

### Autonomous Processing

```text
Supervisor
    ↓
Understands examination allocation
    ↓
Planner
    ↓
Creates execution plan
    ↓
Operations Agent
    ↓
Retrieves exam + classroom data
    ↓
Allocates rooms
    ↓
Verifier
    ↓
Detects classroom conflict
    ↓
Replanner
    ↓
Creates alternative allocation
    ↓
Verifier
    ↓
PASS
    ↓
Final Allocation
```

---

## Installation

### 1. Clone the Repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd CampusOps-AI
```

### 2. Create a Virtual Environment

Windows:

```bash
python -m venv .venv
```

Activate it:

```bash
.venv\Scripts\activate
```

If PowerShell blocks activation, use:

```bash
.venv\Scripts\activate.bat
```

or activate the environment through the VS Code Python interpreter.

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Environment Variables

Create a `.env` file in the project root.

Example:

```env
OPENAI_API_KEY=your_api_key_here
```

Do not upload your real API key to GitHub.

Add `.env` to `.gitignore`:

```text
.env
.venv/
__pycache__/
*.pyc
```

---

## Running the Backend

Navigate to the backend application directory:

```bash
cd backend/app
```

Run FastAPI:

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

Backend API:

```text
http://localhost:8000
```

For another device on the same network, use the host computer's local IP address:

```text
http://YOUR_IP_ADDRESS:8000
```

---

## Running the Frontend

Open a second terminal.

Navigate to the frontend directory:

```bash
cd frontend
```

Run Streamlit:

```bash
streamlit run streamlit_app.py --server.address 0.0.0.0
```

The application will normally be available at:

```text
http://localhost:8501
```

For network access:

```text
http://YOUR_IP_ADDRESS:8501
```

---

## API Documentation

When the FastAPI backend is running, API documentation can be accessed through:

```text
http://localhost:8000/docs
```

FastAPI automatically provides interactive API documentation.

---

## Security

The following information should never be committed to GitHub:

* API keys
* Passwords
* Authentication tokens
* Private credentials
* Secret configuration files
* Sensitive database information

Use environment variables for secrets.

---

## Advantages

CampusOps AI provides several advantages over traditional rule-based systems:

* Autonomous task planning
* Multi-agent collaboration
* Natural-language interaction
* Automated verification
* Failure detection
* Automatic replanning
* Modular architecture
* Extensible workflows
* Reduced manual effort
* Improved operational consistency

---

## Agentic AI Characteristics

CampusOps AI demonstrates important characteristics of an Agentic AI system:

| Capability           | Implementation      |
| -------------------- | ------------------- |
| Goal Understanding   | Supervisor Agent    |
| Planning             | Planner Agent       |
| Task Decomposition   | Planner             |
| Tool Selection       | Operations Workflow |
| Execution            | Operations Agent    |
| Observation          | Workflow State      |
| Verification         | Verifier Agent      |
| Error Detection      | Verifier            |
| Recovery             | Replanner Agent     |
| Autonomous Iteration | LangGraph Workflow  |

---

## Future Enhancements

Possible future improvements include:

* PostgreSQL integration
* Authentication and role-based access
* Advanced timetable optimization
* Real-time notifications
* Email integration
* Calendar integration
* Faculty workload optimization
* AI-powered resource forecasting
* Multi-campus support
* Analytics dashboard
* Docker deployment
* Cloud deployment
* Human-in-the-loop approval
* Audit logging
* Advanced conflict-resolution algorithms

---

## Research Potential

CampusOps AI can be extended into research areas such as:

* Multi-Agent Systems
* Autonomous Planning
* Agentic AI
* AI-based Scheduling
* Constraint Optimization
* Human-Agent Collaboration
* Autonomous Decision-Making
* AI Workflow Orchestration
* Self-Correcting AI Systems

---

## Project Team

**CampusOps AI — Autonomous College Operations Manager**

Developed as an AI/ML project focusing on **Multi-Agent Systems, Agentic AI, and Autonomous Workflow Orchestration**.

---

## License

This project is intended for educational and research purposes.

You may modify and extend the project according to your requirements.

---

## Conclusion

CampusOps AI demonstrates how **Agentic AI can be applied to real-world college operations**.

Instead of simply responding to a user's question, the system follows an autonomous cycle:

```text
UNDERSTAND
    ↓
PLAN
    ↓
EXECUTE
    ↓
OBSERVE
    ↓
VERIFY
    ↓
REPLAN
    ↓
EXECUTE AGAIN
    ↓
FINAL VERIFIED RESULT
```

The project therefore moves beyond a traditional chatbot toward an **autonomous, multi-agent operational management system**.
## Demo Video

[▶️ Watch CampusOps AI Demo](assets/campusops-demo.

mp4)
