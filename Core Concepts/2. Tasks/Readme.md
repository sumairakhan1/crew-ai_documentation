Here's a **detailed guide** on managing and creating **Tasks** in **CrewAI** with a **beginner-friendly** explanation, **real-world use cases**, and **code examples** with explanations.  

---

# 🚀 **Managing and Creating Tasks in CrewAI**  

## 📌 **What is a Task in CrewAI?**  
In the **CrewAI framework**, a **Task** is a specific assignment completed by an **Agent**. It contains all the necessary information needed for execution, such as:  
- **Task description**: What needs to be done?  
- **Assigned Agent**: Who will do the task?  
- **Required tools**: What tools are needed to complete the task?  

### 💡 **Key Features of Tasks in CrewAI**  
✅ Tasks can be **simple or complex** depending on the requirements.  
✅ Tasks can be **collaborative**, meaning multiple agents can work together.  
✅ The execution of tasks is managed by the **Crew’s process** to ensure efficiency.  

---

## 🌎 **Real-World Example of CrewAI Tasks**  
### Example: **Customer Support Automation**  
Imagine you are building an **AI-powered customer support system** where:  
- **Agent 1** handles **basic queries**.  
- **Agent 2** manages **technical support**.  
- **Agent 3** is responsible for **escalating unresolved issues**.  

Each **task** in this system represents a specific customer request. The CrewAI framework can ensure that tasks are assigned to the right agents based on their expertise.  

---

# ⚡ **Task Execution Flow in CrewAI**  
Tasks can be executed in **two ways** depending on the workflow requirement:  

## 📌 **1. Sequential Execution**  
- Tasks are executed **one after another**, in the order they are defined.  
- Example:  
  - Step 1: Collect customer data  
  - Step 2: Validate the request  
  - Step 3: Process the request  
  - Step 4: Send response  

## 📌 **2. Hierarchical Execution**  
- Tasks are assigned **based on the agent’s role and expertise**.  
- Example:  
  - A **junior agent** handles basic questions.  
  - A **senior agent** manages advanced queries.  
  - If a query is unresolved, it is escalated to a **manager**.  

---

# 🛠 **Code Example: Creating and Managing Tasks in CrewAI**  

### **Step 1: Install CrewAI**
Make sure you have **CrewAI** installed:  
```bash
pip install crewai
```

### **Step 2: Define Agents**
Agents are AI-powered entities that complete tasks.  
```python
from crewai import Agent

# Create Agents
agent1 = Agent(name="Alice", role="Customer Support Agent", expertise="Basic Queries")
agent2 = Agent(name="Bob", role="Technical Support Agent", expertise="Advanced Issues")
```
**🔍 Explanation:**  
- We create **two agents**:  
  - **Alice** → Handles basic queries.  
  - **Bob** → Handles technical issues.  

---

### **Step 3: Define Tasks**
Tasks define what each agent needs to do.  
```python
from crewai import Task

# Define Tasks
task1 = Task(description="Answer basic customer queries", agent=agent1)
task2 = Task(description="Handle advanced technical support requests", agent=agent2)
```
**🔍 Explanation:**  
- **task1** is assigned to **Alice** (basic queries).  
- **task2** is assigned to **Bob** (technical issues).  

---

### **Step 4: Define the Crew and Execution Process**
We define how tasks should be executed.  
```python
from crewai import Crew, Process

# Define Crew with Agents and Tasks
crew = Crew(
    agents=[agent1, agent2],
    tasks=[task1, task2],
    process=Process.sequential  # or Process.hierarchical
)

# Start the Execution
crew.kickoff()
```
**🔍 Explanation:**  
- We create a **Crew** that consists of the two agents.  
- We assign **tasks** to them.  
- We specify the **execution type** (`Process.sequential` or `Process.hierarchical`).  
- We call `crew.kickoff()` to **start** the execution.  

---

# 🎯 **Final Thoughts**
✅ **CrewAI** makes it easy to create and manage tasks for AI agents.  
✅ Tasks can be executed **sequentially** or **hierarchically** based on the workflow.  
✅ This framework is useful for **customer support, data analysis, automation, and more!**  

Would you like me to expand on any specific part? 🚀

---

# 🚀 **Understanding Task Attributes in CrewAI**  

When creating tasks in **CrewAI**, you can specify various **attributes** to control execution behavior, agent responsibilities, tools, and outputs. This guide explains **each attribute in detail**, with **real-world examples** and **code snippets** for better understanding.  

---

# 📌 **1. Task Attributes Explained**  

Each **Task** in CrewAI has multiple attributes. Let's break them down:  

| **Attribute** | **Type** | **Description** |
|--------------|---------|----------------|
| **description** | `str` | A clear statement of what the task entails. |
| **expected_output** | `str` | Defines the desired outcome of the task. |
| **name** (optional) | `Optional[str]` | A unique identifier for the task. |
| **agent** (optional) | `Optional[BaseAgent]` | The agent responsible for executing the task. |
| **tools** (optional) | `List[BaseTool]` | Tools the agent is allowed to use. |
| **context** (optional) | `Optional[List["Task"]]` | Other tasks whose outputs will be used in this task. |
| **async_execution** (optional) | `Optional[bool]` | Whether the task should run asynchronously (default: `False`). |
| **human_input** (optional) | `Optional[bool]` | Whether a human review is required before completing the task (default: `False`). |
| **config** (optional) | `Optional[Dict[str, Any]]` | Additional configuration parameters. |
| **output_file** (optional) | `Optional[str]` | The file path to save the task output. |
| **output_json** (optional) | `Optional[Type[BaseModel]]` | A Pydantic model for structured JSON output. |
| **output_pydantic** (optional) | `Optional[Type[BaseModel]]` | A Pydantic model for task output. |
| **callback** (optional) | `Optional[Any]` | A function or object to execute after task completion. |

---

# 🚀 **Deep Dive into Task Attributes in CrewAI**  

## 🛠 **What are Task Attributes in CrewAI?**  
In the **CrewAI framework**, a **Task** is not just a simple action—it has multiple attributes that define:  
- **What needs to be done**  
- **Who will perform it**  
- **How the result should be structured**  
- **Whether it needs human intervention**  

By defining these attributes, CrewAI allows for a **structured and efficient** execution of tasks.  

---

# 📌 **Real-World Example of Task Attributes in CrewAI**  
Imagine you're building a **Content Generation AI System** where:  
- **Agent 1 (Writer AI)** generates blog content.  
- **Agent 2 (Editor AI)** proofreads the content.  
- **Agent 3 (Publisher AI)** publishes the article.  

Each step can be structured as a **task** with the right attributes to ensure smooth execution.  

---

# 📜 **Understanding Task Attributes in Detail**  

Below is a breakdown of **each attribute** with an example and explanation.

## 📝 **1. Description (Required)**
Defines what the task is about.  
```python
description="Generate a 1000-word blog post on AI advancements"
```
✅ **Why is it important?**  
- Provides **clarity** to the agent.  
- Ensures the task is executed correctly.  

---

## 🎯 **2. Expected Output (Required)**
Defines what the final result should look like.  
```python
expected_output="A well-structured blog with an introduction, body, and conclusion."
```
✅ **Why is it important?**  
- Helps agents **understand** what a successful output looks like.  
- Ensures quality and consistency.  

---

## 🏷 **3. Name (Optional)**
A unique identifier for the task.  
```python
name="AI Blog Writing Task"
```
✅ **Why is it important?**  
- Useful for **logging and debugging**.  
- Helps identify tasks when multiple tasks are running.  

---

## 🤖 **4. Agent (Optional)**
Assigns a specific **AI agent** to the task.  
```python
agent=content_writer_ai
```
✅ **Why is it important?**  
- Ensures the **right agent** handles the task.  
- Useful when tasks require **different expertise**.  

---

## 🛠 **5. Tools (Optional)**
Defines which **tools or APIs** the agent can use.  
```python
tools=[grammar_checker, plagiarism_checker]
```
✅ **Why is it important?**  
- Restricts agents to using only **approved resources**.  
- Enhances control over **task execution**.  

---

## 🔗 **6. Context (Optional)**
Uses the output of other tasks as **input** for this task.  
```python
context=[previous_research_task]
```
✅ **Why is it important?**  
- Enables **task chaining** for better workflow automation.  
- Allows agents to **build on previous results**.  

---

## ⚡ **7. Async Execution (Optional)**
Determines if the task runs **asynchronously** (non-blocking).  
```python
async_execution=True
```
✅ **Why is it important?**  
- Improves efficiency by allowing multiple tasks to run in **parallel**.  

---

## 👨‍💻 **8. Human Input (Optional)**
Requires human approval before the task is finalized.  
```python
human_input=True
```
✅ **Why is it important?**  
- Ensures human review for **critical** tasks.  
- Useful for content moderation, sensitive information, or **quality control**.  

---

## ⚙ **9. Config (Optional)**
Stores **additional task-specific settings**.  
```python
config={"word_limit": 1000, "tone": "professional"}
```
✅ **Why is it important?**  
- Provides **fine-tuned control** over task execution.  

---

## 📝 **10. Output File (Optional)**
Defines where the task’s output should be stored.  
```python
output_file="generated_blog.txt"
```
✅ **Why is it important?**  
- Saves results for **future reference or analysis**.  

---

## 📂 **11. Output JSON (Optional)**
Formats the task output as a **structured JSON**.  
```python
output_json=BlogPostModel
```
✅ **Why is it important?**  
- Ensures data consistency in **machine-readable format**.  

---

## 📦 **12. Output Pydantic (Optional)**
Defines a **Pydantic model** to validate the output.  
```python
output_pydantic=BlogPostModel
```
✅ **Why is it important?**  
- Helps enforce **data validation and schema consistency**.  

---

## 🔄 **13. Callback (Optional)**
Executes a **custom function** after the task is completed.  
```python
callback=notify_team
```
✅ **Why is it important?**  
- Automates **next steps** after task completion.  
- Useful for **notifications, reporting, or triggering other workflows**.  

---

# 🚀 **Full Code Example: Defining a Task with Attributes in CrewAI**  
Here’s how you can define a task with attributes in **CrewAI**.

```python
from crewai import Task, Agent
from pydantic import BaseModel

# Step 1: Define a Pydantic Model for JSON Output
class BlogPostModel(BaseModel):
    title: str
    content: str
    word_count: int

# Step 2: Create an AI Agent
content_writer_ai = Agent(name="AI Writer", role="Content Creator", expertise="Blog Writing")

# Step 3: Define a Task with Attributes
blog_writing_task = Task(
    description="Generate a 1000-word blog post on AI advancements",
    expected_output="A well-structured blog with an introduction, body, and conclusion.",
    name="AI Blog Writing Task",
    agent=content_writer_ai,
    tools=[],  # No external tools used
    context=[],
    async_execution=False,  # Task runs synchronously
    human_input=True,  # Requires human review
    config={"word_limit": 1000, "tone": "professional"},
    output_file="generated_blog.txt",
    output_json=BlogPostModel,  # Output stored in JSON format
    callback=lambda: print("Task completed!")  # Function executed after task completion
)

# Step 4: Print Task Details
print(f"Task Name: {blog_writing_task.name}")
print(f"Description: {blog_writing_task.description}")
print(f"Expected Output: {blog_writing_task.expected_output}")
print(f"Agent Assigned: {blog_writing_task.agent.name}")
print(f"Output File: {blog_writing_task.output_file}")
```

---

# 🔥 **Explanation of the Code**  

✅ **Step 1: Define a Pydantic Model**  
- `BlogPostModel` ensures that the output follows a specific structure (title, content, word_count).  

✅ **Step 2: Create an AI Agent**  
- `content_writer_ai` is an AI agent specializing in blog writing.  

✅ **Step 3: Define a Task with Attributes**  
- The task is about generating a **1000-word blog post**.  
- The task requires **human approval** before finalizing the result.  
- The output will be stored in **generated_blog.txt** and as a **structured JSON**.  
- A **callback function** (`lambda: print("Task completed!")`) is executed when the task finishes.  

✅ **Step 4: Print Task Details**  
- Displays key task information for debugging and tracking.  

---

# 🎯 **Final Thoughts**  
✅ **Task attributes in CrewAI** provide flexibility and control over AI task execution.  
✅ Attributes like **async_execution, human_input, and output formatting** enhance automation.  
✅ **Real-world use cases** include **content generation, automation, customer support, and data analysis.**  

Would you like a specific **real-world example** implemented in code? 🚀

# 📞 **Automating Customer Support with CrewAI Tasks**  

## 🚀 **Introduction**  
In this guide, we'll explore how to **create and manage tasks in CrewAI** using **YAML configuration** and **Python code**. We'll focus on a **real-world customer support example**, where AI agents handle different customer service tasks.

---

# 🎯 **Real-World Use Case: AI-Powered Customer Support System**  
Imagine an **AI-driven customer support system** where:  
✅ **Agent 1 (FAQ Bot)** answers common questions.  
✅ **Agent 2 (Issue Classifier)** identifies and categorizes customer issues.  
✅ **Agent 3 (Support Representative)** handles complex queries and reports them.  

This setup ensures **efficient, automated** customer interactions with human support only when necessary.

---

# 📌 **1. Creating Tasks in CrewAI**  
CrewAI allows tasks to be **defined in two ways**:  

1️⃣ **Using YAML Configuration (Recommended)** ✅  
2️⃣ **Defining Tasks Directly in Code**  

We'll explore both methods and implement a **customer support AI** that can:  
- **Respond to FAQs**  
- **Classify Customer Issues**  
- **Escalate Issues to Human Support**  

---

# 📝 **2. YAML-Based Task Configuration (Recommended)**  
Using **YAML** keeps task definitions **clean** and **easy to manage**.

### 🛠 **Step 1: Define Tasks in a `tasks.yaml` File**
Create a **tasks.yaml** file inside your project (`src/customer_support/config/tasks.yaml`).

```yaml
faq_task:
  description: >
    Answer frequently asked customer questions about products, delivery,
    and refunds based on pre-defined knowledge.
  expected_output: >
    A concise response to the customer's question, ensuring clarity and accuracy.
  agent: faq_bot

issue_classification_task:
  description: >
    Analyze the customer's query and classify it into categories:
    "Billing", "Technical Issue", "Order Status", or "General Inquiry".
  expected_output: >
    A single category label that best represents the customer's issue.
  agent: issue_classifier

support_task:
  description: >
    If the issue is too complex or requires human involvement, 
    generate a summary report for the human support team.
  expected_output: >
    A structured report including customer details, issue summary, 
    and recommended action.
  agent: support_representative
  output_file: customer_support_report.md
```
### 🔥 **How This Works?**
1. **`faq_task`**: AI bot answers common questions.
2. **`issue_classification_task`**: Categorizes customer issues.
3. **`support_task`**: If required, escalates issues to human support.

---

# 🏗 **3. Implementing CrewAI with Python**  
Now, let’s define **AI agents** and link them to these tasks.

### 📂 **Step 2: Create `crew.py` File**
This file will **register AI agents and tasks**.

```python
# src/customer_support/crew.py

from crewai import Agent, Crew, Process, Task
from crewai.project import CrewBase, agent, crew, task
from crewai_tools import SerperDevTool  # Example tool for web search

@CrewBase
class CustomerSupportCrew():
  """AI-powered Customer Support Crew"""

  @agent
  def faq_bot(self) -> Agent:
    return Agent(
      config=self.agents_config['faq_bot'],  
      verbose=True
    )

  @agent
  def issue_classifier(self) -> Agent:
    return Agent(
      config=self.agents_config['issue_classifier'],
      verbose=True
    )

  @agent
  def support_representative(self) -> Agent:
    return Agent(
      config=self.agents_config['support_representative'],
      verbose=True
    )

  @task
  def faq_task(self) -> Task:
    return Task(
      config=self.tasks_config['faq_task']
    )

  @task
  def issue_classification_task(self) -> Task:
    return Task(
      config=self.tasks_config['issue_classification_task']
    )

  @task
  def support_task(self) -> Task:
    return Task(
      config=self.tasks_config['support_task']
    )

  @crew
  def crew(self) -> Crew:
    return Crew(
      agents=[
        self.faq_bot(),
        self.issue_classifier(),
        self.support_representative()
      ],
      tasks=[
        self.faq_task(),
        self.issue_classification_task(),
        self.support_task()
      ],
      process=Process.sequential  # Executes tasks in order
    )
```

---

# 🔍 **4. Breaking Down the Code**  

### ✅ **Step 1: Define AI Agents**
```python
@agent
def faq_bot(self) -> Agent:
    return Agent(
      config=self.agents_config['faq_bot'],  
      verbose=True
    )
```
🎯 **What This Does:**  
- Registers an **AI FAQ bot** to handle common customer queries.
- Uses **self.agents_config['faq_bot']** to retrieve bot settings.

---

### ✅ **Step 2: Define Tasks**
```python
@task
def faq_task(self) -> Task:
    return Task(
      config=self.tasks_config['faq_task']
    )
```
🎯 **What This Does:**  
- Creates a **FAQ task** that the FAQ bot will handle.
- Retrieves task settings from `tasks.yaml`.

---

### ✅ **Step 3: Register the Crew**
```python
@crew
def crew(self) -> Crew:
    return Crew(
      agents=[
        self.faq_bot(),
        self.issue_classifier(),
        self.support_representative()
      ],
      tasks=[
        self.faq_task(),
        self.issue_classification_task(),
        self.support_task()
      ],
      process=Process.sequential  # Executes tasks in order
    )
```
🎯 **What This Does:**  
- Groups all **agents and tasks** together.
- Uses a **sequential process** (each task runs one after another).

---

# 🚀 **5. Running the Customer Support AI**
### ✅ **Step 1: Start the Crew**
Run the **CrewAI** system by calling:

```python
from src.customer_support.crew import CustomerSupportCrew

crew = CustomerSupportCrew()
crew.crew().kickoff(inputs={'topic': 'Refund Policy'})
```

### ✅ **Step 2: What Happens?**
1️⃣ **FAQ Bot answers common questions** (e.g., "How long do refunds take?").  
2️⃣ **Issue Classifier categorizes customer complaints** (e.g., "Billing Issue").  
3️⃣ **Support Representative escalates complex issues** to human support.  

---

# 🎯 **Final Thoughts**  
✅ **CrewAI simplifies customer support automation.**  
✅ **YAML makes task management easy and scalable.**  
✅ **AI agents work together efficiently.**  

Would you like to add **more advanced features** like **chat history storage** or **sentiment analysis**? 🚀

# 🚀 **Understanding Task Creation in CrewAI**  

CrewAI allows us to define **tasks** in two ways:  
1️⃣ **Using YAML Configuration (Recommended)** 📝  
2️⃣ **Direct Code Definition (Alternative)** 🖥  

This guide will explain the **Direct Code Definition** method in depth, with **real-world examples** and **detailed code breakdowns**.  

---

# 🎯 **Real-World Use Case: AI-Powered Research & Reporting System**  

Imagine a **company** that needs AI to:  
✅ **Research AI topics** for blog posts 📚  
✅ **Generate detailed reports** based on findings 📊  

Using CrewAI, we can automate:  
- **Researching the latest AI trends** 📡  
- **Generating a well-structured report** 📝  
- **Saving the report in Markdown format** 📄  

This saves **time, effort**, and ensures **high-quality outputs**.  

---

# 🏗 **1. Defining Tasks Directly in Code**  

Instead of using a **YAML file**, we can define tasks **directly in Python** using the `Task` class.  

### ✅ **Step 1: Create a `task.py` File**  
Define **two tasks**:  
🔹 **`research_task`** – Gathers AI-related research.  
🔹 **`reporting_task`** – Creates a detailed report.  

```python
from crewai import Task  # Import the Task class

# Define a research task
research_task = Task(
    description="""
        Conduct a thorough research about AI Agents.
        Make sure you find any interesting and relevant information given
        the current year is 2025.
    """,
    expected_output="""
        A list with 10 bullet points of the most relevant information about AI Agents
    """,
    agent=researcher  # Assign to the researcher agent
)

# Define a reporting task
reporting_task = Task(
    description="""
        Review the context you got and expand each topic into a full section for a report.
        Make sure the report is detailed and contains any and all relevant information.
    """,
    expected_output="""
        A fully-fledged report with the main topics, each with a full section of information.
        Formatted as markdown without '```'
    """,
    agent=reporting_analyst,  # Assign to the reporting analyst agent
    output_file="report.md"  # Save the output as a Markdown file
)
```

---

# 🔍 **2. Breaking Down the Code**  

### 🛠 **Defining a Task**  
```python
from crewai import Task  # Import the Task class
```
📌 **What This Does?**  
- Imports the **Task** class from **CrewAI**, allowing us to create structured tasks.  

---

### 📌 **Creating the `research_task`**  
```python
research_task = Task(
    description="""
        Conduct a thorough research about AI Agents.
        Make sure you find any interesting and relevant information given
        the current year is 2025.
    """,
    expected_output="""
        A list with 10 bullet points of the most relevant information about AI Agents
    """,
    agent=researcher  # Assign to the researcher agent
)
```
📌 **What This Does?**  
1️⃣ Defines **`research_task`**, which collects information about **AI Agents**.  
2️⃣ **Description** – Clearly states what needs to be done.  
3️⃣ **Expected Output** – Specifies the required format (10 bullet points).  
4️⃣ **Agent** – Assigns the **task to the researcher agent** (AI that handles research).  

---

### 📌 **Creating the `reporting_task`**  
```python
reporting_task = Task(
    description="""
        Review the context you got and expand each topic into a full section for a report.
        Make sure the report is detailed and contains any and all relevant information.
    """,
    expected_output="""
        A fully-fledged report with the main topics, each with a full section of information.
        Formatted as markdown without '```'
    """,
    agent=reporting_analyst,  # Assign to the reporting analyst agent
    output_file="report.md"  # Save the output as a Markdown file
)
```
📌 **What This Does?**  
1️⃣ Defines **`reporting_task`**, which creates a detailed AI report.  
2️⃣ **Description** – The AI should review the research and write an in-depth report.  
3️⃣ **Expected Output** – The report should contain **detailed sections** with Markdown formatting.  
4️⃣ **Agent** – Assigns the task to the **reporting analyst agent** (AI specialized in writing reports).  
5️⃣ **Output File** – Saves the generated report as a **Markdown file (`report.md`)**.  

---

# ⚡ **3. Connecting Tasks to a CrewAI Workflow**  

We now need to **connect tasks and agents** to run the research-reporting pipeline.

### 📂 **Step 2: Create `crew.py`**
This file **registers the AI agents and tasks**.

```python
# src/ai_research/crew.py

from crewai import Agent, Crew, Process
from crewai_tools import SerperDevTool  # Example research tool
from task import research_task, reporting_task  # Import tasks

# Define AI Agents
researcher = Agent(
    name="AI Researcher",
    role="Research Specialist",
    verbose=True,
    tools=[SerperDevTool()]
)

reporting_analyst = Agent(
    name="AI Reporting Analyst",
    role="Content Creator",
    verbose=True
)

# Register the Crew
crew = Crew(
    agents=[researcher, reporting_analyst],  # Assign agents
    tasks=[research_task, reporting_task],  # Assign tasks
    process=Process.sequential  # Execute tasks in order
)
```

---

# 🔍 **4. Breaking Down the Crew Code**  

### ✅ **Defining AI Agents**  
```python
researcher = Agent(
    name="AI Researcher",
    role="Research Specialist",
    verbose=True,
    tools=[SerperDevTool()]
)
```
📌 **What This Does?**  
- Defines an AI agent **"AI Researcher"** specialized in research.  
- Uses a **SerperDevTool()** for AI-powered web research.  
- `verbose=True` – Enables detailed logs for debugging.  

---

### ✅ **Defining the Crew**  
```python
crew = Crew(
    agents=[researcher, reporting_analyst],  # Assign agents
    tasks=[research_task, reporting_task],  # Assign tasks
    process=Process.sequential  # Execute tasks in order
)
```
📌 **What This Does?**  
1️⃣ **Assigns the AI agents** to handle different tasks.  
2️⃣ **Links tasks to agents** (researcher → research, analyst → reporting).  
3️⃣ **Uses a sequential process** (tasks are executed **one after another**).  

---

# 🚀 **5. Running the Research-Reporting AI System**  

### ✅ **Step 1: Run the Crew**
To start the AI workflow, call:

```python
from src.ai_research.crew import crew

crew.kickoff()
```

### ✅ **Step 2: What Happens?**  
1️⃣ **AI Researcher** gathers AI-related information.  
2️⃣ **AI Reporting Analyst** converts research into a structured Markdown report.  
3️⃣ The report is **saved as `report.md`**.  

---

# 🎯 **Final Thoughts**  

✅ **Direct Code Definition** provides more control.  
✅ **Useful for AI-powered research, customer support, automation, and more.**  
✅ **Easier debugging and flexibility compared to YAML.**  

Would you like to **expand this AI system** with **live web scraping** or **automated email reports**? 🚀

# 🚀 **Understanding Task Outputs in CrewAI**  

Task outputs play a crucial role in **AI workflows**, ensuring that results are well-structured, easy to access, and useful for further processing. CrewAI provides the **`TaskOutput` class**, which helps manage **task results** in various formats, including **raw text, JSON, and structured Pydantic models**.

This guide will **explain `TaskOutput` in-depth**, with **real-world examples, code breakdowns, and step-by-step explanations**.  

---

# 🎯 **Real-World Use Case: AI-Powered News Aggregator**  

Imagine you want to build an **AI news summarizer** that:  
✅ **Searches for the latest AI news** 📰  
✅ **Extracts the top 5 headlines** 📌  
✅ **Formats the output in JSON & Markdown**  

CrewAI’s **`TaskOutput` class** helps **structure** and **store** this data, making it easy to process later.  

---

# 🏗 **1. What is `TaskOutput`?**  

The `TaskOutput` class **stores the result of a completed task**. It supports multiple output formats:  

| 🏷 **Attribute** | 🔍 **Description** |
|---------------|-----------------|
| **`description`** | The **task description** (what the AI was asked to do). |
| **`summary`** | The **first 10 words** of the description (auto-generated). |
| **`raw`** | The **default raw output** (plain text). |
| **`pydantic`** | A **structured model** (if specified in the task). |
| **`json_dict`** | A **JSON object** of the output (if configured). |
| **`agent`** | The **AI agent** that executed the task. |
| **`output_format`** | The **format** (RAW, JSON, or Pydantic). |

---

# 🔍 **2. Accessing Task Outputs**  

Once a task is executed, its output is stored in the `output` attribute.  

### ✅ **Methods to Access Task Outputs**  

| 🏷 **Method/Property** | 🔍 **Description** |
|-----------------|----------------------|
| **`.json()`** | Returns the output as a **JSON string** (if format is JSON). |
| **`.to_dict()`** | Converts **JSON/Pydantic output** to a **dictionary**. |
| **`str()`** | Returns the **output as a string**, prioritizing **Pydantic → JSON → Raw**. |

---

# 🖥 **3. Example: AI News Summarization**  

### ✅ **Step 1: Define the Task**  
This task **searches for AI news** and **summarizes the top 5 headlines**.

```python
from crewai import Task, Crew
import json

# Define the AI research agent
research_agent = Agent(
    name="AI News Researcher",
    role="Finds and summarizes the latest AI news",
    verbose=True
)

# Define a search tool (hypothetical)
search_tool = SomeSearchAPI()

# Create a task to fetch AI news
task = Task(
    description='Find and summarize the latest AI news',
    expected_output='A bullet list summary of the top 5 most important AI news',
    agent=research_agent,
    tools=[search_tool],
    output_format="JSON"  # Store results in JSON format
)
```

📌 **What This Does?**  
1️⃣ **Defines an AI agent** (`research_agent`) to perform the news search.  
2️⃣ **Uses a tool (`search_tool`)** to fetch the latest AI news.  
3️⃣ **Creates a task** with:  
   - **Description**: Find & summarize news.  
   - **Expected Output**: A **bullet-point summary**.  
   - **Output Format**: **JSON** (for structured results).  

---

### ✅ **Step 2: Execute the Crew**  
Now, we **run the task** and store the result.

```python
# Create a Crew with the agent and task
crew = Crew(
    agents=[research_agent],
    tasks=[task],
    verbose=True
)

# Execute the task
result = crew.kickoff()
```

📌 **What This Does?**  
- Registers **the agent and task** inside the Crew.  
- Calls `.kickoff()` to **start the process**.  

---

### ✅ **Step 3: Retrieve & Print Task Output**  

```python
# Accessing the task output
task_output = task.output

print(f"🔍 Task Description: {task_output.description}")
print(f"📝 Task Summary: {task_output.summary}")
print(f"📄 Raw Output: {task_output.raw}")

# If JSON output exists, print it
if task_output.json_dict:
    print(f"📦 JSON Output:\n{json.dumps(task_output.json_dict, indent=2)}")

# If Pydantic output exists, print it
if task_output.pydantic:
    print(f"📊 Pydantic Output:\n{task_output.pydantic}")
```

---

# 🔍 **4. Code Breakdown**  

### 📌 **Retrieving Task Output**  
```python
task_output = task.output
```
- The **output** of the task is **stored** in `task.output`.  

### 📌 **Printing the Raw Output**  
```python
print(f"📄 Raw Output: {task_output.raw}")
```
- Displays the **default text output**.  

### 📌 **Printing the JSON Output (If Available)**  
```python
if task_output.json_dict:
    print(f"📦 JSON Output:\n{json.dumps(task_output.json_dict, indent=2)}")
```
- Converts the JSON **into a formatted string** and prints it.  

### 📌 **Printing the Pydantic Output (If Available)**  
```python
if task_output.pydantic:
    print(f"📊 Pydantic Output:\n{task_output.pydantic}")
```
- If the task was configured with a **Pydantic model**, prints the structured output.  

---

# 🚀 **5. Output Example (Terminal Output)**  

```
🔍 Task Description: Find and summarize the latest AI news
📝 Task Summary: Find and summarize the
📄 Raw Output: 
- AI Breakthrough in 2025: New Model Beats GPT-4  
- AI Detects Cancer with 98% Accuracy  
- Tesla Launches AI-Powered Self-Driving Chip  
- OpenAI Introduces AI-Powered Coding Assistant  
- AI Outperforms Humans in Complex Problem-Solving  

📦 JSON Output:
{
  "top_news": [
    "AI Breakthrough in 2025: New Model Beats GPT-4",
    "AI Detects Cancer with 98% Accuracy",
    "Tesla Launches AI-Powered Self-Driving Chip",
    "OpenAI Introduces AI-Powered Coding Assistant",
    "AI Outperforms Humans in Complex Problem-Solving"
  ]
}
```

---

# 🎯 **6. Key Takeaways**  

✅ **TaskOutput** helps structure task results for easier processing.  
✅ It supports **multiple formats**: **RAW, JSON, Pydantic**.  
✅ **JSON & Pydantic** formats make **data transfer & integration easy**.  
✅ **Useful for real-world applications**, like **news summarization, reporting, and research**.  

Would you like to **extend this project** by **storing results in a database** or **sending summaries via email?** 🚀

# 🚀 **Understanding Task Dependencies and Guardrails in CrewAI**  

When working with **AI workflows**, tasks often rely on **previous task outputs** to function properly. CrewAI allows you to manage **task dependencies** using the **`context`** attribute, ensuring a **smooth workflow** between multiple tasks.  

Additionally, **task guardrails** act as **validation checks** to ensure the **quality** and **integrity** of task outputs before they are passed to the next step.  

This guide will **break down these concepts in detail**, with **real-world use cases, code explanations, and step-by-step breakdowns**.  

---

# 🎯 **Real-World Use Case: AI-Powered Blog Generator**  

Imagine you are building an **AI-powered blogging system** where:  

✅ **Task 1**: An AI **researcher** gathers the latest AI news. 📰  
✅ **Task 2**: An AI **analyst** analyzes trends from the research. 📊  
✅ **Task 3**: An AI **writer** generates a blog post from the analysis. ✍️  
✅ **Task 4**: A **quality guardrail** ensures the blog follows word limits. ✅  

This workflow ensures **structured AI-generated content**, improving **automation** and **quality**.

---

# 🏗 **1. Task Dependencies: Passing Context Between Tasks**  

### ✅ **What Are Task Dependencies?**  
Tasks can **depend on the output of other tasks** using the **`context` attribute**.  
- The **second task** will **wait** until the **first task is completed**.  
- The **third task** can use the **second task’s output** as its input.  

### 🖥 **Code Example: AI Research & Analysis Workflow**  

```python
from crewai import Task, Crew

# Define the AI research agent
researcher = Agent(
    name="AI Researcher",
    role="Finds the latest developments in AI",
    verbose=True
)

# Define the AI analyst agent
analyst = Agent(
    name="AI Analyst",
    role="Analyzes research findings to identify trends",
    verbose=True
)

# Define the first task: Research AI developments
research_task = Task(
    description="Research the latest developments in AI",
    expected_output="A list of recent AI developments",
    agent=researcher
)

# Define the second task: Analyze research findings
analysis_task = Task(
    description="Analyze the research findings and identify key trends",
    expected_output="Analysis report of AI trends",
    agent=analyst,
    context=[research_task]  # Waits for research_task to complete
)
```

---

### 📌 **Breaking Down the Code**  

#### 📍 **Step 1: Define AI Agents**  
```python
researcher = Agent(
    name="AI Researcher",
    role="Finds the latest developments in AI",
    verbose=True
)
```
- **Creates an AI agent** (`researcher`) that **fetches AI news**.  

```python
analyst = Agent(
    name="AI Analyst",
    role="Analyzes research findings to identify trends",
    verbose=True
)
```
- **Creates another AI agent** (`analyst`) to **analyze AI trends**.  

---

#### 📍 **Step 2: Define the First Task (Research AI News)**  
```python
research_task = Task(
    description="Research the latest developments in AI",
    expected_output="A list of recent AI developments",
    agent=researcher
)
```
- This **research task** fetches **the latest AI news**.  

---

#### 📍 **Step 3: Define the Dependent Task (Analyze AI Trends)**  
```python
analysis_task = Task(
    description="Analyze the research findings and identify key trends",
    expected_output="Analysis report of AI trends",
    agent=analyst,
    context=[research_task]  # Waits for research_task to complete
)
```
- **Context `[research_task]`** ensures that `analysis_task` **only starts** after `research_task` **is completed**.  

---

# 🛡 **2. Task Guardrails: Ensuring Output Quality**  

### ✅ **What Are Task Guardrails?**  
Guardrails **validate and transform** task outputs **before passing them to the next step**.  
- Ensures **data accuracy** ✅  
- Prevents **invalid outputs** ❌  
- **Returns feedback** if the output **doesn’t meet criteria**  

---

### 🖥 **Code Example: Blog Content Validation**  

```python
from typing import Tuple, Union, Dict, Any

def validate_blog_content(result: str) -> Tuple[bool, Union[Dict[str, Any], str]]:
    """Validate blog content meets requirements."""
    try:
        # Check word count
        word_count = len(result.split())
        if word_count > 200:
            return (False, {
                "error": "Blog content exceeds 200 words",
                "code": "WORD_COUNT_ERROR",
                "context": {"word_count": word_count}
            })

        # Additional validation logic here
        return (True, result.strip())
    except Exception as e:
        return (False, {
            "error": "Unexpected error during validation",
            "code": "SYSTEM_ERROR"
        })

# Define the blog writing task
blog_task = Task(
    description="Write a blog post about AI",
    expected_output="A blog post under 200 words",
    agent=blog_agent,
    guardrail=validate_blog_content  # Add the guardrail function
)
```

---

### 📌 **Breaking Down the Code**  

#### 📍 **Step 1: Define a Guardrail Function**  
```python
def validate_blog_content(result: str) -> Tuple[bool, Union[Dict[str, Any], str]]:
```
- The function **validates** AI-generated blog content.  
- It **returns a tuple**:  
  - **`True, result`** if valid ✅  
  - **`False, error message`** if invalid ❌  

---

#### 📍 **Step 2: Check Word Count**  
```python
word_count = len(result.split())
if word_count > 200:
    return (False, {
        "error": "Blog content exceeds 200 words",
        "code": "WORD_COUNT_ERROR",
        "context": {"word_count": word_count}
    })
```
- Counts words in the **AI-generated blog**.  
- **If it exceeds 200 words**, the **guardrail rejects** the content.  

---

#### 📍 **Step 3: Return Valid Content**  
```python
return (True, result.strip())
```
- If the content **meets criteria**, it **passes through** ✅.  

---

#### 📍 **Step 4: Attach the Guardrail to the Task**  
```python
blog_task = Task(
    description="Write a blog post about AI",
    expected_output="A blog post under 200 words",
    agent=blog_agent,
    guardrail=validate_blog_content  # Add the guardrail function
)
```
- The `guardrail` function **validates the AI-generated blog** before it moves to the next step.  

---

# 📌 **3. Full Workflow: Research → Analysis → Blog Writing with Validation**  

```python
crew = Crew(
    agents=[researcher, analyst, blog_agent],
    tasks=[research_task, analysis_task, blog_task],
    verbose=True
)

result = crew.kickoff()
```
- **Runs all tasks in order** 🚀  
- **Ensures dependencies are met** ✅  
- **Validates final blog output** ✍️  

---

# 🔍 **4. Output Example (Terminal Output)**  

```
🔍 Research Task: Found 5 latest AI developments.
📊 Analysis Task: Identified top 3 AI trends.
📝 Blog Task: Generated AI blog (Word Count: 250)
❌ ERROR: Blog content exceeds 200 words (Task Rejected)
```

---

# 🎯 **5. Key Takeaways**  

✅ **Task Dependencies** ensure tasks **execute in the correct order**.  
✅ The **`context` attribute** passes **data between tasks**.  
✅ **Task Guardrails** validate outputs **before moving forward**.  
✅ **Real-world uses**: News analysis, content moderation, data validation.  

Would you like to **extend this project** by adding **AI-generated summaries** or **email notifications**? 🚀

# 🛡 **Understanding Guardrail Functions in CrewAI**  

When working with **AI-generated content**, it’s important to **validate and filter** the outputs before using them. **Guardrail functions** help enforce **quality control** by:  
✅ **Validating the AI-generated output** before passing it forward.  
✅ **Ensuring structured responses** that meet requirements.  
✅ **Providing clear error handling** for debugging.  

In this guide, we’ll break down:  
✔ **Guardrail function requirements**  
✔ **Best practices for error handling**  
✔ **Chaining multiple validation steps**  

---  

# 🎯 **Real-World Use Case: AI-Powered Customer Support Chatbot**  

Imagine you have an **AI chatbot** that answers customer queries. The chatbot's response must:  
✅ Be **non-empty** (to prevent blank replies).  
✅ **Avoid inappropriate content** (filter toxic or offensive responses).  
✅ **Follow formatting rules** (structured as a professional response).  

To achieve this, we use **guardrail functions** to validate and filter responses **before sending them to customers**.  

---

# 🏗 **1. Guardrail Function Requirements**  

### ✅ **What is a Guardrail Function?**  
A **guardrail function** is a function that validates AI-generated outputs. It:  
- **Accepts one parameter** (the task output).  
- **Returns a tuple** of **(boolean, response)**.  
  - **`(True, validated_result)`** → If the response is valid ✅  
  - **`(False, error_details)`** → If the response is invalid ❌  
- **Uses type hints** (recommended for readability).  

---

### 🖥 **Code Example: Basic Guardrail Function**  

```python
from typing import Tuple, Union, Dict, Any

def validate_response(result: str) -> Tuple[bool, Union[str, Dict[str, Any]]]:
    """Validate AI chatbot response before sending to user."""
    
    # Check if response is empty
    if not result.strip():
        return (False, {
            "error": "Response is empty",
            "code": "EMPTY_RESPONSE"
        })

    # Check if response is too long (e.g., max 200 words)
    word_count = len(result.split())
    if word_count > 200:
        return (False, {
            "error": "Response exceeds 200 words",
            "code": "WORD_LIMIT_EXCEEDED",
            "context": {"word_count": word_count}
        })

    # If all checks pass, return valid response
    return (True, result.strip())
```

---

### 📌 **Breaking Down the Code**  

#### 📍 **Step 1: Function Definition**  
```python
def validate_response(result: str) -> Tuple[bool, Union[str, Dict[str, Any]]]:
```
- **Defines a function** `validate_response` that **takes one parameter** (`result` - the chatbot's response).  
- **Returns a tuple**:  
  - `True, validated_result` → If valid ✅  
  - `False, error_details` → If invalid ❌  

---

#### 📍 **Step 2: Check for Empty Responses**  
```python
if not result.strip():
    return (False, {
        "error": "Response is empty",
        "code": "EMPTY_RESPONSE"
    })
```
- If the **response is empty or contains only spaces**, it’s **invalid** ❌.  
- **Returns an error** `"EMPTY_RESPONSE"` with details.  

---

#### 📍 **Step 3: Check for Word Count Limit**  
```python
word_count = len(result.split())
if word_count > 200:
    return (False, {
        "error": "Response exceeds 200 words",
        "code": "WORD_LIMIT_EXCEEDED",
        "context": {"word_count": word_count}
    })
```
- **Splits the response** into words and **counts them**.  
- If the **word count exceeds 200**, it **returns an error** `"WORD_LIMIT_EXCEEDED"`.  
- The `"context"` field includes the **actual word count** for debugging.  

---

#### 📍 **Step 4: Return Valid Response**  
```python
return (True, result.strip())
```
- If the response passes **all checks**, it **returns as valid** ✅.  

---

# ⚠ **2. Best Practices for Error Handling**  

### ✅ **1. Use Structured Error Responses**  
Errors should:  
✔ Include **error codes** for easy debugging.  
✔ Provide **context** (e.g., word count, invalid content).  
✔ Give **clear feedback** on what went wrong.  

---

### 🖥 **Code Example: Handling Multiple Error Types**  

```python
def validate_with_context(result: str) -> Tuple[bool, Union[Dict[str, Any], str]]:
    try:
        # Main validation logic
        validated_data = perform_validation(result)
        return (True, validated_data)
    
    except ValidationError as e:
        return (False, {
            "error": str(e),
            "code": "VALIDATION_ERROR",
            "context": {"input": result}
        })
    
    except Exception as e:
        return (False, {
            "error": "Unexpected error",
            "code": "SYSTEM_ERROR"
        })
```

---

### 📌 **Breaking Down the Code**  

#### 📍 **Try Block: Main Validation Logic**  
```python
validated_data = perform_validation(result)
return (True, validated_data)
```
- Tries to **validate** the AI output using `perform_validation()`.  
- If **successful**, it returns the **validated response** ✅.  

---

#### 📍 **Handling Validation Errors**  
```python
except ValidationError as e:
    return (False, {
        "error": str(e),
        "code": "VALIDATION_ERROR",
        "context": {"input": result}
    })
```
- If the **validation fails**, it returns:  
  - **Error message** (`error`).  
  - **Error code** (`VALIDATION_ERROR`).  
  - **Context** (original input for debugging).  

---

#### 📍 **Handling Unexpected Errors**  
```python
except Exception as e:
    return (False, {
        "error": "Unexpected error",
        "code": "SYSTEM_ERROR"
    })
```
- If **any unknown error occurs**, it returns a `"SYSTEM_ERROR"`.  

---

# 🔗 **3. Chaining Multiple Validation Steps**  

### ✅ **Why Use a Validation Chain?**  
✔ Allows **multiple validation steps** to **process outputs** step by step.  
✔ If one step **fails**, the process **stops immediately**.  
✔ Ensures **data is fully validated** before being used.  

---

### 🖥 **Code Example: Multi-Step Validation Chain**  

```python
from typing import Any, Dict, Tuple, Union

def complex_validation(result: str) -> Tuple[bool, Union[str, Dict[str, Any]]]:
    """Chain multiple validation steps."""
    
    # Step 1: Check if input is empty
    if not result:
        return (False, {"error": "Empty result", "code": "EMPTY_INPUT"})

    # Step 2: Validate content
    try:
        validated = validate_content(result)
        if not validated:
            return (False, {"error": "Invalid content", "code": "CONTENT_ERROR"})

        # Step 3: Format validation
        formatted = format_output(validated)
        return (True, formatted)

    except Exception as e:
        return (False, {
            "error": str(e),
            "code": "VALIDATION_ERROR",
            "context": {"step": "content_validation"}
        })
```

---

### 📌 **Breaking Down the Code**  

#### 📍 **Step 1: Check for Empty Input**  
```python
if not result:
    return (False, {"error": "Empty result", "code": "EMPTY_INPUT"})
```
- Ensures **input isn’t empty** before processing.  

---

#### 📍 **Step 2: Validate Content**  
```python
validated = validate_content(result)
if not validated:
    return (False, {"error": "Invalid content", "code": "CONTENT_ERROR"})
```
- Uses `validate_content()` to **check if the content is appropriate**.  

---

#### 📍 **Step 3: Format Validation**  
```python
formatted = format_output(validated)
return (True, formatted)
```
- **Formats** the validated response **before passing it forward**.  

---

# 🎯 **Key Takeaways**  

✅ **Guardrail functions** ensure AI-generated outputs are **valid and high-quality**.  
✅ **Error handling best practices** include **structured responses and debugging context**.  
✅ **Validation chains** allow multiple **steps** to check **different aspects** of the output.  

Would you like to **extend this with real-time monitoring** or **add logging for debugging**? 🚀

---

# 10. # 🛡️ **Handling Guardrail Results in AI and Automation**  

When working with **AI models** or **automated systems**, **guardrails** act as **filters** to ensure the generated output is **valid and correct**.  

For example, if you're using **AI to generate JSON reports**, a guardrail can:  
✔ Check if the JSON is **well-formed**.  
✔ Return **errors** if it’s **incorrect**.  
✔ **Retry** fixing the issue until it's **correct**.  

---

# 🎯 **Why Do We Need Guardrails?**  

🚀 **Ensures AI-generated output is reliable**  
🔄 **Automatically retries fixing errors**  
🔍 **Improves data quality and system performance**  
🛑 **Prevents incorrect or harmful outputs**  

---

# 📌 **Real-World Use Case: AI-Generated Reports**  

Imagine you’re building an **AI-powered financial dashboard** that generates daily reports in **JSON format**.  

### Problem:  
❌ Sometimes, the AI **fails to generate valid JSON** due to missing or malformed data.  

### Solution:  
✅ We use a **guardrail function** to **validate the JSON output** and **retry until it’s correct**.  

---

# 🔄 **How the Guardrail Works**  

1️⃣ The **guardrail function** checks if the output is **valid**.  
2️⃣ If **invalid**, it returns `(False, error)` and sends it back to the agent.  
3️⃣ The **agent** tries to **fix the issue** and retries.  
4️⃣ This process **repeats until**:  
   ✔ The **output is valid** `(True, result)`.  
   ❌ The **maximum retries** are reached.  

---

# 🖥 **Example Code: Guardrail with Retry Handling**  

```python
import json
from typing import Any, Dict, Tuple, Union

def validate_json_output(result: str) -> Tuple[bool, Union[Dict[str, Any], str]]:
    """Validate and parse JSON output."""
    try:
        # 🛠 Attempt to parse the string as JSON
        data = json.loads(result)
        return (True, data)  # ✅ Success: Return parsed JSON
    except json.JSONDecodeError as e:
        return (False, {
            "error": "Invalid JSON format",  # ❌ Error message
            "code": "JSON_ERROR",  # 🔢 Error code
            "context": {"line": e.lineno, "column": e.colno}  # 🔍 Error location
        })

class Task:
    def __init__(self, description, expected_output, agent, guardrail, max_retries=3):
        self.description = description
        self.expected_output = expected_output
        self.agent = agent
        self.guardrail = guardrail
        self.max_retries = max_retries

    def execute(self):
        retries = 0
        while retries < self.max_retries:
            output = self.agent.generate_output()  # 🔄 AI generates output
            is_valid, result = self.guardrail(output)  # 🛡️ Validate output

            if is_valid:
                return result  # ✅ Return valid output
            
            print(f"Retry {retries + 1}: {result}")  # ⚠️ Log the error
            
            retries += 1
        
        return {"error": "Max retries reached", "code": "MAX_RETRIES"}

# Example agent class (simulated AI system)
class Agent:
    def generate_output(self):
        # Simulating an AI response (sometimes incorrect JSON)
        return '{"name": "John Doe", "age": 30'  # ❌ Missing closing bracket

# Initialize agent and task
analyst = Agent()
task = Task(
    description="Generate a JSON report",
    expected_output="A valid JSON object",
    agent=analyst,
    guardrail=validate_json_output,
    max_retries=3
)

# Execute the task with guardrails
result = task.execute()
print(result)
```

---

# 📌 **Breaking Down the Code**  

### 📍 **Step 1: JSON Validation Function**  
```python
def validate_json_output(result: str) -> Tuple[bool, Union[Dict[str, Any], str]]:
```
- Takes **one input** (`result`) → a JSON **string**.  
- Returns **(True, JSON object)** if valid.  
- Returns **(False, error details)** if invalid.  

---

### 📍 **Step 2: Attempt to Parse JSON**  
```python
data = json.loads(result)
return (True, data)
```
- Uses `json.loads(result)` to **convert a string into a JSON object**.  
- If **successful**, returns the parsed **JSON data**.  

---

### 📍 **Step 3: Handling JSON Errors**  
```python
except json.JSONDecodeError as e:
    return (False, {
        "error": "Invalid JSON format",
        "code": "JSON_ERROR",
        "context": {"line": e.lineno, "column": e.colno}
    })
```
- If JSON is **malformed**, it:  
  ✔ Returns an **error message** `"Invalid JSON format"`.  
  ✔ Includes an **error code** `"JSON_ERROR"`.  
  ✔ Provides **context** (`line` and `column` where the error occurred).  

---

### 📍 **Step 4: Task Class (Handles Retries)**  
```python
class Task:
    def __init__(self, description, expected_output, agent, guardrail, max_retries=3):
```
- Stores **task details**, the **agent**, and the **guardrail function**.  
- Sets **maximum retry attempts** (`max_retries`).  

---

### 📍 **Step 5: Executing the Task with Guardrails**  
```python
while retries < self.max_retries:
    output = self.agent.generate_output()  # 🔄 AI generates output
    is_valid, result = self.guardrail(output)  # 🛡️ Validate output

    if is_valid:
        return result  # ✅ Return valid output

    print(f"Retry {retries + 1}: {result}")  # ⚠️ Log the error
    
    retries += 1

return {"error": "Max retries reached", "code": "MAX_RETRIES"}
```
- **Loops through retries** (max **3 attempts**).  
- If **valid output**, returns it.  
- If **invalid**, retries **until it’s correct or reaches max retries**.  

---

# 🎯 **Key Takeaways**  

✅ **Guardrails ensure AI-generated output is valid**  
✅ **If errors occur, the system retries fixing them**  
✅ **Provides structured error responses** for debugging  
✅ **Improves automation reliability**  

Would you like me to **add logging or improve retry logic?** 🚀

---

# 11. Getting Structured & Consistent Outputs from Tasks

# 📌 **Getting Structured & Consistent Outputs from Tasks**  

In **AI-powered automation**, ensuring that **task outputs are structured and validated** is crucial. This prevents errors, ensures data consistency, and allows smooth integration with other systems.  

🚀 **CrewAI** provides a feature called `output_pydantic`, which allows us to define **structured outputs** using **Pydantic models**.  

✔ **Why use structured outputs?**  
- ✅ **Consistency** – Ensures that all outputs follow a predefined format.  
- ✅ **Validation** – Prevents missing or incorrect data.  
- ✅ **Reliability** – Helps in seamless integration with other applications.  

---

# 🏗️ **How Task Output Works in CrewAI**  

- In **CrewAI**, the **final task's output** becomes the **final output of the crew**.  
- By using **Pydantic models**, we ensure that this output follows a strict format.  

---

# 📌 **Real-World Example: AI-Generated Blog Content**  

Imagine you're building an **AI-powered blogging assistant** that generates blog titles and content.  

### Problem:  
❌ AI sometimes returns **unstructured, inconsistent outputs**.  
❌ Some outputs **miss important fields** (e.g., no title).  
❌ It’s hard to **process AI-generated content programmatically**.  

### Solution:  
✅ We use **Pydantic models** to ensure a **structured response**.  
✅ This guarantees that **every blog has a title and content**.  
✅ It makes it easy to **store, analyze, and integrate the output**.  

---

# 🖥 **Example Code: Structured AI Task Output Using CrewAI & Pydantic**  

```python
import json
from crewai import Agent, Crew, Process, Task
from pydantic import BaseModel

# 🏗 Define a Pydantic model for the expected output
class Blog(BaseModel):
    title: str  # ✅ Title of the blog
    content: str  # ✅ Content of the blog

# 🎭 Define the AI agent responsible for content generation
blog_agent = Agent(
    role="Blog Content Generator Agent",
    goal="Generate a blog title and content",
    backstory="You are an expert content creator, skilled in crafting engaging and informative blog posts.",
    verbose=False,
    allow_delegation=False,
    llm="gpt-4o",
)

# 📝 Define a task for the agent
task1 = Task(
    description="Create a blog title and content on a given topic. Make sure the content is under 200 words.",
    expected_output="A compelling blog title and well-written content.",
    agent=blog_agent,
    output_pydantic=Blog,  # 🔄 Ensure the output follows the Blog Pydantic model
)

# 🏢 Create a Crew and assign tasks to the agent
crew = Crew(
    agents=[blog_agent],
    tasks=[task1],
    verbose=True,
    process=Process.sequential,  # 🔄 Tasks are executed sequentially
)

# 🚀 Execute the CrewAI workflow
result = crew.kickoff()

# 📌 Accessing the output in multiple ways:

# ✅ Option 1: Dictionary-style indexing
print("Accessing Properties - Option 1")
title = result["title"]
content = result["content"]
print("Title:", title)
print("Content:", content)

# ✅ Option 2: Accessing from Pydantic model
print("Accessing Properties - Option 2")
title = result.pydantic.title
content = result.pydantic.content
print("Title:", title)
print("Content:", content)

# ✅ Option 3: Converting to dictionary
print("Accessing Properties - Option 3")
output_dict = result.to_dict()
title = output_dict["title"]
content = output_dict["content"]
print("Title:", title)
print("Content:", content)

# ✅ Option 4: Printing the entire blog object
print("Accessing Properties - Option 4")
print("Blog:", result)
```

---

# 📌 **Breaking Down the Code**  

### 🎯 **Step 1: Define a Pydantic Model**  
```python
class Blog(BaseModel):
    title: str
    content: str
```
- `BaseModel`: Inherits from Pydantic's base class.  
- `title: str`: Ensures that every blog **must have a title**.  
- `content: str`: Ensures that the blog **must have content**.  
- If AI **fails to generate** a title or content, it will throw a **validation error**.  

---

### 🎯 **Step 2: Create an AI Agent**  
```python
blog_agent = Agent(
    role="Blog Content Generator Agent",
    goal="Generate a blog title and content",
    backstory="You are an expert content creator, skilled in crafting engaging and informative blog posts.",
    verbose=False,
    allow_delegation=False,
    llm="gpt-4o",
)
```
- **Defines an AI agent** specialized in writing blogs.  
- **Goal:** Generates blog titles and content.  
- **Uses GPT-4o** as its language model.  

---

### 🎯 **Step 3: Define the AI Task**  
```python
task1 = Task(
    description="Create a blog title and content on a given topic. Make sure the content is under 200 words.",
    expected_output="A compelling blog title and well-written content.",
    agent=blog_agent,
    output_pydantic=Blog,  # ✅ Enforces structured output
)
```
- The **task** asks AI to generate a **blog title and content**.  
- The `output_pydantic=Blog` ensures that the output **matches the Blog model**.  

---

### 🎯 **Step 4: Create a Crew and Assign the Task**  
```python
crew = Crew(
    agents=[blog_agent],
    tasks=[task1],
    verbose=True,
    process=Process.sequential,  # 🔄 Ensures tasks run one after another
)
```
- Creates a **CrewAI workflow** with **one agent and one task**.  
- **Sequential processing** ensures tasks execute in order.  

---

### 🎯 **Step 5: Run the AI Task and Get Results**  
```python
result = crew.kickoff()
```
- This **runs the task**, and AI generates a **blog title and content**.  

---

# 📌 **How to Access the Output?**  

Once the task is executed, the **result is stored in a structured format**. You can access it in **multiple ways**:  

✅ **Option 1: Dictionary-style indexing**  
```python
title = result["title"]
content = result["content"]
```
- Allows **direct access** like a dictionary.  

✅ **Option 2: Accessing from Pydantic model**  
```python
title = result.pydantic.title
content = result.pydantic.content
```
- Uses **Pydantic’s model** for cleaner attribute access.  

✅ **Option 3: Converting to dictionary**  
```python
output_dict = result.to_dict()
title = output_dict["title"]
content = output_dict["content"]
```
- Converts the **Pydantic object** into a dictionary.  

✅ **Option 4: Printing the entire object**  
```python
print("Blog:", result)
```
- Prints the **structured blog object**.  

---

# 🎯 **Key Takeaways**  

✅ **Ensures structured, validated AI output** using `output_pydantic`  
✅ **Prevents missing or malformed data**  
✅ **Easier integration** into other applications  
✅ **Multiple ways to access results**  

Would you like to extend this with **error handling or dynamic topics**? 🚀

---

# 12. Using Output Json
# 📌 **Using `output_json` in CrewAI**  

In **AI-powered workflows**, ensuring **structured output** is crucial for consistency and reliability.  

**🚀 `output_json`** helps define the expected **output format as JSON**, making the data **easy to parse and use** in applications.  

✔ **Why use JSON output?**  
- ✅ **Standard format** – JSON is widely used in APIs and databases.  
- ✅ **Easy to parse** – Programming languages have built-in JSON support.  
- ✅ **Reliable structure** – Ensures AI-generated output is consistent.  

---

# 🏗️ **How `output_json` Works in CrewAI**  

- When defining a task, you can specify `output_json`, which ensures the output **follows a valid JSON structure**.  
- The **final output of the task** becomes the **final output of the CrewAI workflow**.  
- This structured output **eliminates inconsistencies** and makes AI-generated data easy to process.  

---

# 📌 **Real-World Example: AI Blog Generator**  

### 🌍 **Scenario**  
Imagine you're building an **AI-powered blog generator** that produces **titles and content** for blog posts.  

### ❌ **Problems Without JSON Output**  
- AI might return **unstructured text**, making it hard to extract a **title** and **content**.  
- If integrated with an API, missing or incorrect fields could cause **errors**.  
- The output might **not be valid JSON**, leading to **parsing issues**.  

### ✅ **Solution Using `output_json`**  
- Ensures AI-generated output **follows a proper JSON structure**.  
- Guarantees **title and content fields** are always present.  
- Makes it easy to **integrate with APIs, databases, and frontend applications**.  

---

# 🖥 **Example Code: Using `output_json` in CrewAI**  

```python
import json
from crewai import Agent, Crew, Process, Task
from pydantic import BaseModel

# 🏗 Define a Pydantic model for structured output
class Blog(BaseModel):
    title: str  # ✅ Blog title
    content: str  # ✅ Blog content

# 🎭 Define the AI agent responsible for content generation
blog_agent = Agent(
    role="Blog Content Generator Agent",
    goal="Generate a blog title and content",
    backstory="You are an expert content creator, skilled in crafting engaging and informative blog posts.",
    verbose=False,
    allow_delegation=False,
    llm="gpt-4o",
)

# 📝 Define a task with JSON output
task1 = Task(
    description="Create a blog title and content on a given topic. Make sure the content is under 200 words.",
    expected_output="A JSON object with 'title' and 'content' fields.",
    agent=blog_agent,
    output_json=Blog,  # 🔄 Ensures AI output follows JSON format
)

# 🏢 Create a Crew and assign the task
crew = Crew(
    agents=[blog_agent],
    tasks=[task1],
    verbose=True,
    process=Process.sequential,  # 🔄 Tasks run one after another
)

# 🚀 Execute the CrewAI workflow
result = crew.kickoff()

# 📌 Accessing the output in multiple ways:

# ✅ Option 1: Dictionary-style indexing
print("Accessing Properties - Option 1")
title = result["title"]
content = result["content"]
print("Title:", title)
print("Content:", content)

# ✅ Option 2: Printing the entire JSON object
print("Accessing Properties - Option 2")
print("Blog JSON:", result)
```

---

# 📌 **Breaking Down the Code**  

### 🎯 **Step 1: Define a Pydantic Model for JSON Output**  
```python
class Blog(BaseModel):
    title: str
    content: str
```
- **Ensures AI output follows this structure**.  
- AI **must return** `title` and `content`, or else **validation fails**.  

---

### 🎯 **Step 2: Create an AI Agent**  
```python
blog_agent = Agent(
    role="Blog Content Generator Agent",
    goal="Generate a blog title and content",
    backstory="You are an expert content creator, skilled in crafting engaging and informative blog posts.",
    verbose=False,
    allow_delegation=False,
    llm="gpt-4o",
)
```
- Defines an **AI agent** specialized in writing blogs.  
- Uses **GPT-4o** as its language model.  

---

### 🎯 **Step 3: Define a Task with `output_json`**  
```python
task1 = Task(
    description="Create a blog title and content on a given topic. Make sure the content is under 200 words.",
    expected_output="A JSON object with 'title' and 'content' fields.",
    agent=blog_agent,
    output_json=Blog,  # ✅ Ensures output is a valid JSON object
)
```
- This **task** asks AI to generate a **blog title and content**.  
- The `output_json=Blog` ensures the output is **formatted as JSON**.  

---

### 🎯 **Step 4: Create a Crew and Assign the Task**  
```python
crew = Crew(
    agents=[blog_agent],
    tasks=[task1],
    verbose=True,
    process=Process.sequential,  # 🔄 Ensures tasks run in order
)
```
- Creates a **CrewAI workflow** with **one agent and one task**.  
- Uses **sequential processing** to run tasks **one after another**.  

---

### 🎯 **Step 5: Run the AI Task and Get Results**  
```python
result = crew.kickoff()
```
- This **executes the task**, and AI generates a **JSON object with title and content**.  

---

# 📌 **How to Access the JSON Output?**  

Once the task is executed, the **result is stored as JSON**. You can access it in **multiple ways**:  

✅ **Option 1: Dictionary-style indexing**  
```python
title = result["title"]
content = result["content"]
```
- Retrieves the **title and content** from the JSON response.  

✅ **Option 2: Printing the entire JSON object**  
```python
print("Blog JSON:", result)
```
- Prints the entire **JSON-formatted blog object**.  

---

# 📌 **Why Use `output_json` Instead of `output_pydantic`?**  

| Feature | `output_pydantic` | `output_json` |
|---------|-----------------|-----------------|
| **Ensures structured output** | ✅ Yes | ✅ Yes |
| **Uses Pydantic validation** | ✅ Yes | ❌ No |
| **Returns a JSON object** | ❌ No | ✅ Yes |
| **Best for APIs & frontend apps** | ❌ No | ✅ Yes |

**👉 Use `output_json` when:**  
✔ You need a **pure JSON response**.  
✔ You want to integrate with **APIs, databases, or JavaScript apps**.  

**👉 Use `output_pydantic` when:**  
✔ You need **strict validation** with Pydantic.  
✔ You're working **inside Python** and need structured objects.  

---

# 🎯 **Key Takeaways**  

✅ **Ensures AI-generated output is valid JSON**  
✅ **Prevents missing or malformed data**  
✅ **Ideal for APIs, frontend integration, and databases**  
✅ **Easier to parse and process in other applications**  

Would you like to see **error handling examples** or **dynamic topic generation**? 🚀