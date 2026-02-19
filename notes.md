ProblemSolverAgent (LLM)
        ↓
CodeExecutorAgent (Tool Agent)
        ↓
DockerCommandLineCodeExecutor (Runtime Engine)
        ↓
Docker Container (Sandbox)
        ↓
Python Execution
        ↓
Output Returned

Your system now looks like this:

User
  ↓
ProblemSolverAgent (LLM)
  ↓ sends python code
CodeExecutorAgent (Tool Agent)
  ↓
Docker Executor
  ↓
Execution Output
  ↓
Back to ProblemSolverAgent


This is a separation of intelligence and execution.


A Tool Agent is an agent that:

Does not think.
Does not call an LLM.
Does not generate language.
It performs deterministic actions.

It is basically:

LLM Brain  →  Tool Agent  →  Real-world action

## autogen architecture
In AutoGen Architecture

There are generally two categories:

1️⃣ LLM Agents (Cognitive)

Use model_client

Generate text

Plan, reason, decide

Example: AssistantAgent

2️⃣ Tool Agents (Execution / Action)

No model_client

Execute something

Perform structured tasks

Example: CodeExecutorAgent



🔁 So The Flow Is:
Step 1 — LLM Agent generates code
```python
print("Hello")
```

Step 2 — Tool Agent detects code block

It extracts:

print("Hello")

Step 3 — Tool Agent sends code to Docker executor

Docker runs:

python temp_script.py

Step 4 — Docker returns:
Hello

Step 5 — Tool Agent wraps result into message

It sends back:

Execution Result:
Hello


Still no LLM involved.


LLM → writes instructions
Tool Agent → forwards instructions
Docker → executes instructions
Tool Agent → forwards output
LLM → interprets output
