# 1. crews attributes.

Here’s a detailed beginner-friendly explanation of **Crews in CrewAI**, covering all aspects with examples, real-world applications, code snippets, and step-by-step explanations.  

---

# 🚀 Understanding Crews in CrewAI  
A **Crew** in CrewAI is a team of AI agents working together to complete a set of tasks efficiently. It defines how agents collaborate, the order of task execution, and the strategy for achieving a goal.  

🔹 Imagine a **crew** like a team of employees in a company, where each member (agent) has a specific role and contributes to achieving a shared objective.  

---

## 🏗️ **What is a Crew?**  
A **Crew** in CrewAI represents a structured **group of agents** working together to complete assigned tasks. It is responsible for **task delegation, execution strategy, and workflow management**.

### 📌 **Real-World Example:**  
🔹 **Customer Support System**  
A **Crew** can manage a **customer support system**, where different AI agents handle:  
✔️ Basic inquiries (FAQ bot)  
✔️ Escalations (Support agent)  
✔️ Follow-ups (Feedback collector)  

---

# 🔧 **Crew Attributes and Their Purpose**  

A **Crew** consists of several attributes that define how it functions. Let's go through them in detail.

| **Attribute** | **Parameters** | **Description** |
|--------------|--------------|----------------|
| **Tasks** | `tasks` | List of tasks assigned to the crew. |
| **Agents** | `agents` | List of agents in the crew. |
| **Process** | `process` (optional) | Execution strategy: Sequential, Hierarchical, etc. Default is **Sequential**. |
| **Verbose** | `verbose` (optional) | Enables logging during execution. Default is **False**. |
| **Manager LLM** | `manager_llm` (optional) | Language model used by the **manager agent** in a hierarchical process. |
| **Function Calling LLM** | `function_calling_llm` (optional) | LLM responsible for function calling for agents. |
| **Config** | `config` (optional) | JSON or dictionary containing additional settings. |
| **Max RPM** | `max_rpm` (optional) | Maximum requests per minute (rate limit). |
| **Language** | `language` (optional) | Default language (English by default). |
| **Memory** | `memory` (optional) | Stores execution data for short-term, long-term, or entity memory. |
| **Cache** | `cache` (optional) | Stores execution results to avoid redundant processing. Default is **True**. |
| **Embedder** | `embedder` (optional) | Defines the embedding provider (e.g., OpenAI). |
| **Full Output** | `full_output` (optional) | Returns either the final result or all intermediate outputs. Default is **False**. |
| **Step Callback** | `step_callback` (optional) | A function triggered after each agent's step. |
| **Task Callback** | `task_callback` (optional) | A function executed after task completion. |
| **Manager Agent** | `manager_agent` (optional) | Defines a **custom manager agent** to oversee the crew. |
| **Planning** | `planning` (optional) | Enables **AgentPlanner** for pre-planning task execution. |
| **Output Log File** | `output_log_file` (optional) | Saves execution logs in a `.txt` or `.json` file. |

---

# 💻 **Code Example: Implementing a Crew in CrewAI**  

Let’s create a simple **Crew** that consists of agents performing a document review process.

### **📝 Scenario: Automating Document Review Process**  
Imagine a **legal firm** where:  
✅ One agent **extracts key information** from documents.  
✅ Another agent **verifies and validates** the extracted information.  
✅ A final agent **summarizes the document** for human review.

---

## **1️⃣ Define Agents**  
We first create individual **agents** with different roles.

```python
from crewai import Agent  

# Agent 1: Extractor
extractor_agent = Agent(
    name="Document Extractor",
    role="Extracts key information from documents",
    tools=["Text Extraction Tool"],
    verbose=True
)

# Agent 2: Validator
validator_agent = Agent(
    name="Information Validator",
    role="Validates the extracted information",
    tools=["Verification Tool"],
    verbose=True
)

# Agent 3: Summarizer
summarizer_agent = Agent(
    name="Document Summarizer",
    role="Summarizes the validated information",
    tools=["Summarization Tool"],
    verbose=True
)
```

### **🔍 Explanation:**
1. **`Agent()`**: Creates an AI agent with specific capabilities.
2. **`name`**: Defines the agent’s identity.
3. **`role`**: Describes what the agent does.
4. **`tools`**: Assigns specific tools the agent will use.
5. **`verbose=True`**: Enables detailed logging of agent actions.

---

## **2️⃣ Define Tasks**  
Now, let's create **tasks** and assign them to agents.

```python
from crewai import Task  

# Task 1: Extract key information
extract_task = Task(
    description="Extract key information from legal documents",
    agent=extractor_agent
)

# Task 2: Validate extracted information
validate_task = Task(
    description="Verify and validate extracted legal information",
    agent=validator_agent
)

# Task 3: Summarize document
summarize_task = Task(
    description="Generate a summary of validated legal information",
    agent=summarizer_agent
)
```

### **🔍 Explanation:**
1. **`Task()`**: Creates a task that an agent will perform.
2. **`description`**: Defines what needs to be done.
3. **`agent`**: Assigns an agent to execute the task.

---

## **3️⃣ Create and Run the Crew**  
Now, we organize agents and tasks into a **Crew**.

```python
from crewai import Crew  

# Creating the Crew
document_review_crew = Crew(
    tasks=[extract_task, validate_task, summarize_task],
    agents=[extractor_agent, validator_agent, summarizer_agent],
    process="sequential",
    verbose=True
)

# Running the Crew
document_review_crew.kickoff()
```

### **🔍 Explanation:**
1. **`Crew()`**: Creates a group of agents and tasks.
2. **`tasks`**: List of tasks the Crew will execute.
3. **`agents`**: List of agents forming the Crew.
4. **`process="sequential"`**: Ensures tasks execute in a step-by-step manner.
5. **`verbose=True`**: Logs execution details.
6. **`kickoff()`**: Starts the execution of the crew.

---

# 🎯 **Real-World Applications of Crews in CrewAI**  

| **Industry** | **Use Case** |
|-------------|-------------|
| 🏦 **Finance** | Automating **fraud detection** by having different agents analyze transactions, validate anomalies, and generate alerts. |
| 🏥 **Healthcare** | AI agents in a **medical crew** can assist in diagnosing symptoms, verifying patient data, and generating reports. |
| 📞 **Customer Support** | Multi-agent system handling **FAQ queries, issue escalation, and ticket resolution**. |
| 📄 **Legal Industry** | Document processing system for **contract analysis, legal validation, and summarization**. |
| 🔍 **SEO & Content Marketing** | A crew of agents optimizing SEO, analyzing trends, and generating reports for content marketing. |

---

# ✅ **Key Takeaways**  
✔ **Crews** in CrewAI allow multiple AI agents to collaborate and complete tasks efficiently.  
✔ Crews follow **sequential, hierarchical, or custom execution strategies**.  
✔ Attributes like **memory, caching, and logging** enhance performance.  
✔ **Real-world applications** range from **customer support** to **finance, legal, and healthcare**.  
✔ Implementing a crew involves **defining agents, tasks, and execution flow**.  

---

# 🎯 **Next Steps**  
🚀 **Start experimenting with CrewAI!**  
Try modifying the code to create your own AI-powered workflows. Need help? Let’s discuss how you can implement Crews in your projects! 🚀

# 🚀 Understanding CrewAI Task Execution in Detail  

CrewAI allows multiple **agents** to work together to complete **tasks** efficiently. In this guide, we'll break down the key attributes of **Tasks, Agents, Process, Verbose, Manager LLM, and Function Calling LLM** with real-world applications and detailed code explanations.  

---

# 📌 **1. What are Tasks in CrewAI?**  

### ✅ **Definition:**  
A **task** in CrewAI is a specific job that an **agent** is responsible for executing. It contains instructions that guide the agent in performing an action.  

### 📌 **Real-World Example:**  
🔹 **Customer Support System**  
In an **AI-powered customer service team**, tasks could include:  
✔️ **Greeting users** and identifying their issue.  
✔️ **Providing solutions** or escalating complaints.  
✔️ **Collecting feedback** after issue resolution.  

### 💻 **Code Example: Creating a Task in CrewAI**  

```python
from crewai import Task  

# Creating a simple task
greet_task = Task(
    description="Greet the user and ask how we can assist them.",
    agent=None  # We will assign an agent later
)
```

### **🔍 Explanation:**  
1. **`Task()`**: Creates a new task.  
2. **`description`**: Describes the action the agent must perform.  
3. **`agent=None`**: Placeholder for an agent that will execute the task.  

---

# 🧑‍💻 **2. What are Agents in CrewAI?**  

### ✅ **Definition:**  
An **agent** in CrewAI is an AI-powered assistant that executes tasks. Each agent has a specific **role, responsibilities, and tools**.  

### 📌 **Real-World Example:**  
🔹 **AI-powered Document Processing**  
✔️ One agent **extracts key information** from a document.  
✔️ Another agent **validates the extracted information**.  
✔️ A final agent **summarizes the document** for human review.  

### 💻 **Code Example: Creating an Agent**  

```python
from crewai import Agent  

# Creating an AI agent
assistant_agent = Agent(
    name="Customer Assistant",
    role="Handles basic customer inquiries and greets users.",
    tools=["FAQ Tool"],  # AI tool used by the agent
    verbose=True  # Enables logging for debugging
)
```

### **🔍 Explanation:**  
1. **`Agent()`**: Creates an AI agent.  
2. **`name`**: Gives the agent a unique identity.  
3. **`role`**: Defines the agent’s job description.  
4. **`tools`**: Specifies the tools the agent will use.  
5. **`verbose=True`**: Enables detailed logs of agent actions.  

---

# 🔄 **3. Process: Defining Execution Strategy**  

### ✅ **Definition:**  
The **process** defines how the Crew executes tasks. There are two main types:  
✔️ **Sequential**: Tasks run one after another.  
✔️ **Hierarchical**: A **manager agent** supervises execution and assigns tasks dynamically.  

### 📌 **Real-World Example:**  
🔹 **Hiring Process Automation**  
✔️ **Step 1**: HR Assistant agent collects resumes.  
✔️ **Step 2**: Screening agent filters candidates.  
✔️ **Step 3**: Interview agent conducts AI-based interviews.  

### 💻 **Code Example: Setting Execution Strategy**  

```python
from crewai import Crew  

# Creating a Crew with a sequential execution strategy
customer_support_crew = Crew(
    tasks=[greet_task],  # List of tasks
    agents=[assistant_agent],  # List of agents
    process="sequential",  # Tasks run one after another
    verbose=True
)
```

### **🔍 Explanation:**  
1. **`Crew()`**: Defines a team of agents and their tasks.  
2. **`process="sequential"`**: Tasks run in order (first greet, then assist).  
3. **`verbose=True`**: Enables logging for better debugging.  

---

# 📢 **4. Verbose: Enabling Execution Logs**  

### ✅ **Definition:**  
The **verbose** setting determines whether CrewAI logs execution details.  

✔ **True**: Enables logs (useful for debugging).  
✔ **False**: Disables logs (saves processing power).  

### 📌 **Real-World Example:**  
🔹 **AI Chatbot Development**  
While building a chatbot, developers may **enable verbose mode** to track errors in real-time.  

### 💻 **Code Example: Using Verbose Mode**  

```python
customer_support_crew = Crew(
    tasks=[greet_task],  
    agents=[assistant_agent],  
    process="sequential",
    verbose=True  # Logs execution steps
)
```

### **🔍 Explanation:**  
1. **`verbose=True`**: Prints logs for debugging and monitoring.  

---

# 🤖 **5. Manager LLM: Using AI for Task Management**  

### ✅ **Definition:**  
A **Manager LLM (Large Language Model)** supervises agents in a **hierarchical** process. It helps assign and manage tasks dynamically.  

### 📌 **Real-World Example:**  
🔹 **AI-Powered Content Creation**  
✔ **AI Manager** assigns research, writing, and editing tasks to different AI agents.  

### 💻 **Code Example: Using Manager LLM**  

```python
customer_support_crew = Crew(
    tasks=[greet_task],
    agents=[assistant_agent],
    process="hierarchical",  # Uses a manager agent
    manager_llm="gpt-4-turbo",  # Assigns an LLM to manage tasks
    verbose=True
)
```

### **🔍 Explanation:**  
1. **`process="hierarchical"`**: Uses a manager agent to control execution.  
2. **`manager_llm="gpt-4-turbo"`**: Assigns an AI model to manage tasks.  

---

# 🛠️ **6. Function Calling LLM: Automating Tool Execution**  

### ✅ **Definition:**  
A **Function Calling LLM** allows agents to call external tools and APIs dynamically.  

### 📌 **Real-World Example:**  
🔹 **Stock Market Analysis System**  
✔ AI agents **fetch stock prices**, analyze trends, and make predictions using APIs.  

### 💻 **Code Example: Using Function Calling LLM**  

```python
customer_support_crew = Crew(
    tasks=[greet_task],
    agents=[assistant_agent],
    function_calling_llm="gpt-4-1106-preview",  # Enables function calling
    verbose=True
)
```

### **🔍 Explanation:**  
1. **`function_calling_llm="gpt-4-1106-preview"`**: Allows agents to interact with external APIs.  

---

# 🎯 **Key Takeaways**  

| **Concept** | **Definition** | **Example Use Case** |
|------------|--------------|------------------|
| **Tasks** | Specific jobs assigned to agents. | AI handling customer inquiries. |
| **Agents** | AI-powered assistants executing tasks. | Chatbot responding to user queries. |
| **Process** | Defines task execution order. | Sequential or hierarchical workflows. |
| **Verbose** | Enables execution logging. | Debugging AI models. |
| **Manager LLM** | AI supervisor managing tasks. | Content generation manager. |
| **Function Calling LLM** | AI executing external functions. | Fetching stock market data. |

---

# 🚀 **Next Steps**  
🎯 Try modifying the code to create your own AI-powered workflows! Need help? Let’s discuss how you can implement CrewAI in your projects! 🚀


# 🚀 **Deep Dive into CrewAI Advanced Configurations**  

CrewAI provides **powerful configuration options** that allow us to fine-tune how agents and tasks operate. In this guide, we will explore **Config, Max RPM, Language, Memory, Cache, and Embedder**, their real-world use cases, and **detailed code explanations** for better understanding.  

---

# 🔧 **1. Config: Additional Settings for CrewAI**  

### ✅ **Definition:**  
The **Config** attribute allows developers to pass additional settings as a **JSON object or a dictionary** to customize how the crew operates.  

### 📌 **Real-World Example:**  
🔹 **AI-Powered Customer Support**  
Imagine an AI-powered **customer service system** where different agents handle **support tickets, complaints, and queries**. The **config** can define:  
✔️ **Response time thresholds**  
✔️ **Priority levels for queries**  
✔️ **Custom logging options**  

### 💻 **Code Example: Using Config in CrewAI**  

```python
from crewai import Crew

# Defining a custom configuration dictionary
custom_config = {
    "logging": "detailed",  # Enables detailed logging
    "retry_attempts": 3,    # Retries failed tasks up to 3 times
    "timeout": 10           # Maximum execution time per task in seconds
}

# Creating a Crew with custom configurations
customer_support_crew = Crew(
    tasks=[],
    agents=[],
    config=custom_config  # Passing custom settings
)
```

### **🔍 Explanation:**  
1. **`custom_config`**: Defines custom settings like logging, retries, and timeouts.  
2. **`config=custom_config`**: Passes the configuration to the crew.  

---

# 🚀 **2. Max RPM: Rate Limiting Requests**  

### ✅ **Definition:**  
The **Max RPM (Requests Per Minute)** attribute controls the maximum number of requests the crew can make **to avoid exceeding API limits**.  

### 📌 **Real-World Example:**  
🔹 **AI-Powered Stock Market Analysis**  
✔ AI agents fetch stock prices from an API.  
✔ API limits requests to **100 per minute**.  
✔ **Max RPM ensures agents stay within limits**.  

### 💻 **Code Example: Setting Max RPM**  

```python
customer_support_crew = Crew(
    tasks=[],
    agents=[],
    max_rpm=50  # Limit requests to 50 per minute
)
```

### **🔍 Explanation:**  
1. **`max_rpm=50`**: Limits the crew to 50 requests per minute to prevent exceeding API limits.  

---

# 🌍 **3. Language: Setting the Default Language**  

### ✅ **Definition:**  
The **Language** attribute defines the default language for the crew. By default, it's **English**, but it can be changed for multilingual support.  

### 📌 **Real-World Example:**  
🔹 **Multilingual AI Chatbot**  
✔ AI **customer support chatbot** in multiple languages.  
✔ Automatically sets the **default language** based on user location.  

### 💻 **Code Example: Setting the Default Language**  

```python
customer_support_crew = Crew(
    tasks=[],
    agents=[],
    language="fr"  # Sets French as the default language
)
```

### **🔍 Explanation:**  
1. **`language="fr"`**: Changes the crew’s default language to French.  

---

# 💾 **4. Memory: Storing Execution Data**  

### ✅ **Definition:**  
The **Memory** attribute allows the crew to **store and recall past interactions** using **short-term, long-term, or entity memory**.  

### 📌 **Real-World Example:**  
🔹 **AI Personal Assistant**  
✔ Remembers previous conversations.  
✔ Recalls **user preferences** and past requests.  

### 💻 **Code Example: Enabling Memory**  

```python
customer_support_crew = Crew(
    tasks=[],
    agents=[],
    memory="long-term"  # Stores previous interactions for future use
)
```

### **🔍 Explanation:**  
1. **`memory="long-term"`**: Stores user interactions over time for a better experience.  

---

# ⚡ **5. Cache: Storing Execution Results**  

### ✅ **Definition:**  
The **Cache** attribute enables result storage to **avoid redundant processing**. By default, it is **enabled (`True`)**.  

### 📌 **Real-World Example:**  
🔹 **AI Search Engine**  
✔ If a user searches **"latest tech trends,"** the AI can **cache the response** to serve it faster next time.  

### 💻 **Code Example: Disabling Cache**  

```python
customer_support_crew = Crew(
    tasks=[],
    agents=[],
    cache=False  # Disables caching
)
```

### **🔍 Explanation:**  
1. **`cache=False`**: Forces the crew to generate fresh responses every time.  

---

# 🔍 **6. Embedder: Configuring AI Embeddings**  

### ✅ **Definition:**  
The **Embedder** attribute sets the embedding model, which is mainly used for **memory storage and vector-based search**.  

### 📌 **Real-World Example:**  
🔹 **AI-Powered Document Search**  
✔ AI **embeds** legal documents for **quick retrieval** using OpenAI’s embeddings.  

### 💻 **Code Example: Using OpenAI for Embeddings**  

```python
customer_support_crew = Crew(
    tasks=[],
    agents=[],
    embedder={"provider": "openai"}  # Uses OpenAI's embedding model
)
```

### **🔍 Explanation:**  
1. **`embedder={"provider": "openai"}`**: Specifies OpenAI as the embedding provider.  

---

# 🎯 **Key Takeaways**  

| **Feature** | **Purpose** | **Example Use Case** |
|------------|------------|------------------|
| **Config** | Custom settings for the crew. | AI chatbot logging, retry attempts. |
| **Max RPM** | Controls API request rate. | Stock market API with request limits. |
| **Language** | Defines default language. | Multilingual AI chatbots. |
| **Memory** | Stores past interactions. | AI personal assistants remembering users. |
| **Cache** | Stores previous execution results. | AI-powered search engines. |
| **Embedder** | Defines embedding provider. | AI document retrieval systems. |

---

# 🚀 **Next Steps**  
Try modifying these attributes to **customize your AI-powered workflow**! Need help? Let's discuss how you can apply these features in real-world projects. 🚀

# 🚀 **Deep Dive into CrewAI Advanced Features**  

CrewAI provides **powerful functionalities** to **enhance control, logging, and execution flow**. In this guide, we will explore:  

- **Full Output** 📝  
- **Step Callback** 🔄  
- **Task Callback** ✅  
- **Manager Agent** 🏗️  
- **Planning** 📋  
- **Output Log File** 🗂️  

Each section includes **real-world use cases, code examples, and a detailed explanation of every line of code** to help beginners understand these concepts easily.  

---

# 📝 **1. Full Output: Controlling What Results Are Returned**  

### ✅ **Definition:**  
The `full_output` attribute determines whether the crew returns **only the final result** or **all intermediate outputs** from each task.  

- **Default (`False`)**: Only the **final output** is returned.  
- **Set to `True`**: Returns **all outputs** from every step.  

### 📌 **Real-World Example:**  
🔹 **AI Research Assistant**  
✔ An AI assistant **summarizes multiple articles**.  
✔ `full_output=True` stores **each step's summary**, allowing deeper insights.  

### 💻 **Code Example: Enabling Full Output**  

```python
from crewai import Crew

# Creating a Crew with full output enabled
research_crew = Crew(
    tasks=[],  # Tasks assigned to the crew
    agents=[],  # Agents working on the tasks
    full_output=True  # Returns all intermediate outputs, not just final result
)

# Running the crew
output = research_crew.run()
print(output)  # Prints all task outputs
```

### **🔍 Explanation:**  
1. **`full_output=True`**: Collects and returns results from all tasks instead of just the final one.  
2. **`research_crew.run()`**: Executes the crew and returns all step-wise outputs.  

---

# 🔄 **2. Step Callback: Executing a Function After Each Step**  

### ✅ **Definition:**  
A **step callback** is a function that runs **after every agent's step**. It allows us to **log progress, track actions, or modify execution dynamically**.  

### 📌 **Real-World Example:**  
🔹 **AI Content Writer**  
✔ AI generates content **step by step**.  
✔ **Logs each step** to track progress.  

### 💻 **Code Example: Implementing a Step Callback**  

```python
def log_step(agent, step_output):
    print(f"Agent {agent.name} completed a step with output: {step_output}")

content_writer_crew = Crew(
    tasks=[],  
    agents=[],  
    step_callback=log_step  # Calls log_step() after each step
)
```

### **🔍 Explanation:**  
1. **`log_step(agent, step_output)`**: A function to log each step’s result.  
2. **`step_callback=log_step`**: Calls `log_step` after every agent step.  

---

# ✅ **3. Task Callback: Executing a Function After Task Completion**  

### ✅ **Definition:**  
A **task callback** is triggered **after a task is fully completed**, useful for **logging, reporting, or triggering new workflows**.  

### 📌 **Real-World Example:**  
🔹 **AI-Powered Job Application Screener**  
✔ AI scans resumes.  
✔ **Triggers email notifications** after processing each resume.  

### 💻 **Code Example: Implementing a Task Callback**  

```python
def notify_completion(task, result):
    print(f"Task '{task.name}' completed. Final result: {result}")

job_screener_crew = Crew(
    tasks=[],  
    agents=[],  
    task_callback=notify_completion  # Calls notify_completion() after task completion
)
```

### **🔍 Explanation:**  
1. **`notify_completion(task, result)`**: Logs the final task result.  
2. **`task_callback=notify_completion`**: Calls this function when a task is completed.  

---

# 🏗️ **4. Manager Agent: Overseeing the Crew**  

### ✅ **Definition:**  
The **Manager Agent** is a special agent responsible for **supervising other agents and assigning tasks**.  

### 📌 **Real-World Example:**  
🔹 **AI Software Development Team**  
✔ The **Manager AI** assigns coding, testing, and deployment tasks to other agents.  

### 💻 **Code Example: Defining a Manager Agent**  

```python
from crewai import Agent, Crew

# Creating a manager agent
manager = Agent(name="Project Manager")

# Creating a crew with a manager agent
dev_team_crew = Crew(
    tasks=[],  
    agents=[],  
    manager_agent=manager  # Assigning a manager agent
)
```

### **🔍 Explanation:**  
1. **`manager = Agent(name="Project Manager")`**: Creates a manager agent.  
2. **`manager_agent=manager`**: Assigns the manager agent to the crew.  

---

# 📋 **5. Planning: Enabling Pre-Planned Execution**  

### ✅ **Definition:**  
Planning allows CrewAI to **pre-organize task execution** using **AgentPlanner**, optimizing efficiency.  

### 📌 **Real-World Example:**  
🔹 **AI Task Scheduler**  
✔ AI schedules **meetings, emails, and deadlines** efficiently.  

### 💻 **Code Example: Enabling Planning**  

```python
dev_team_crew = Crew(
    tasks=[],  
    agents=[],  
    planning=True  # Enables pre-planned task execution
)
```

### **🔍 Explanation:**  
1. **`planning=True`**: Enables structured pre-planning of tasks.  

---

# 🗂️ **6. Output Log File: Storing Execution Logs**  

### ✅ **Definition:**  
This feature allows CrewAI to **store execution logs** in a `.txt` or `.json` file for debugging or record-keeping.  

### 📌 **Real-World Example:**  
🔹 **AI Legal Assistant**  
✔ AI analyzes legal documents and stores execution logs for auditing.  

### 💻 **Code Example: Saving Execution Logs**  

```python
legal_ai_crew = Crew(
    tasks=[],  
    agents=[],  
    output_log_file="execution_logs.json"  # Saves logs in JSON format
)
```

### **🔍 Explanation:**  
1. **`output_log_file="execution_logs.json"`**: Stores logs in a JSON file.  

---

# 🎯 **Key Takeaways**  

| **Feature**        | **Purpose** | **Example Use Case** |
|------------------|------------|------------------|
| **Full Output** | Returns all outputs, not just the final result. | AI research assistant summarizing multiple sources. |
| **Step Callback** | Triggers after each step for logging. | AI content writer tracking progress. |
| **Task Callback** | Runs after task completion for reporting. | AI job screener sending email notifications. |
| **Manager Agent** | Supervises other agents and assigns tasks. | AI project manager handling a development team. |
| **Planning** | Pre-organizes task execution for efficiency. | AI scheduling tasks in a business workflow. |
| **Output Log File** | Saves logs in `.txt` or `.json` format. | AI legal assistant storing document analysis logs. |

---

# 🚀 **Next Steps**  
Try implementing these features in your **CrewAI projects** to enhance **logging, tracking, and structured execution**! Need help? Let’s discuss how you can optimize your AI workflows! 🚀

---

# 2. Creating crews Using YAML Configuration


# 🚀 **Understanding Crews in CrewAI: A Complete Beginner's Guide**  

In this guide, we'll dive deep into how to **create crews in CrewAI** using **YAML configuration** and **decorators** in Python.  
We'll break down complex concepts, explain each line of code, and provide **real-world examples** to make it simple and beginner-friendly.  

---

## 🔍 **What is a Crew in CrewAI?**  
A **crew** in CrewAI is a group of **agents** working together to complete defined **tasks**.  
Think of a crew like a **team of employees in a company**, where each person (agent) has specific responsibilities (tasks).  

---

## 🌟 **Why Use YAML Configuration to Create Crews?**  
✅ Cleaner and more organized code  
✅ Easier to maintain and update  
✅ Consistency across CrewAI projects  

---

## 🌍 **Real-World Example: Content Creation Team**  
Imagine you are running a **content creation agency**. You have:  
- 🖋️ **Writer** (Agent 1) - Creates content  
- 🧹 **Editor** (Agent 2) - Reviews and edits the content  
- 💻 **SEO Specialist** (Agent 3) - Optimizes the content for search engines  

These agents need to perform tasks like writing, editing, and optimizing articles. A **crew** would manage this entire workflow in sequence.  

---

## 📝 **How to Create Crews Using YAML Configuration**  
### ✨ **1. Install and Set Up Your CrewAI Project**  
```bash
pip install crewai
```
*This installs CrewAI so we can start building our project.*  

---

### 🗂️ **2. Define Agents and Tasks in YAML Files**  

#### **agents.yaml**  
```yaml
agent_one:
  name: "Content Writer"
  role: "Generates high-quality blog articles"
  goal: "Produce engaging and SEO-friendly content"

agent_two:
  name: "Content Editor"
  role: "Edits and improves written articles"
  goal: "Ensure content is clear, accurate, and well-structured"
```

#### **tasks.yaml**  
```yaml
task_one:
  name: "Write Article"
  description: "Create a 1500-word article on AI advancements."

task_two:
  name: "Edit Article"
  description: "Review and enhance the article for clarity and SEO."
```

---

### ⚡ **3. Create Your Crew Class with Decorators**  
Let's break down the code **line by line** and understand what's happening:

```python
# Importing necessary classes and decorators from CrewAI
from crewai import Agent, Crew, Task, Process
from crewai.project import CrewBase, agent, task, crew, before_kickoff, after_kickoff
```
🔹 *These imports bring in the tools needed to define agents, tasks, and the crew structure.*  

---

### 🛠️ **4. Define the Crew Class**  

```python
@CrewBase
class ContentCreationCrew:
    """This crew handles the content creation workflow from writing to editing."""
```
✅ `@CrewBase`: Marks this class as a crew structure.  
✅ The `"""docstring"""` explains the purpose of this crew.

---

### 📄 **5. Link YAML Configurations**  
```python
    agents_config = 'config/agents.yaml' 
    tasks_config = 'config/tasks.yaml' 
```
🔹 *These variables tell the class where to find agent and task configurations.*  

---

### 🎬 **6. Pre-Processing Inputs (Before Kickoff)**  
```python
    @before_kickoff
    def prepare_inputs(self, inputs):
        # Adding extra info before starting tasks
        inputs['additional_data'] = "Keyword: AI Trends"
        return inputs
```
✅ `@before_kickoff`: Runs this method **before** the crew starts working.  
📌 **Purpose:** Modify inputs like adding extra information needed for the tasks.

---

### 🎬 **7. Post-Processing Outputs (After Kickoff)**  
```python
    @after_kickoff
    def process_output(self, output):
        # Adding extra processing after all tasks finish
        output.raw += "\n[Edited and SEO Optimized!]"
        return output
```
✅ `@after_kickoff`: Runs **after** all tasks are completed.  
📌 **Purpose:** Final touches like adding notes or formatting the output.

---

### 🧑‍💻 **8. Define Agents with @agent Decorator**  
```python
    @agent
    def agent_one(self) -> Agent:
        return Agent(
            config=self.agents_config['agent_one'],
            verbose=True
        )
```
✅ `@agent`: Marks this method as defining an **agent**.  
📌 **Purpose:** Fetches the "Content Writer" configuration from the YAML file.  
🗣️ `verbose=True`: Shows detailed logs of what the agent is doing.

---

### 🎯 **9. Define Tasks with @task Decorator**  
```python
    @task
    def task_one(self) -> Task:
        return Task(
            config=self.tasks_config['task_one']
        )
```
✅ `@task`: Marks this method as defining a **task**.  
📌 **Purpose:** Fetches the "Write Article" task from the YAML file.

---

### 🚀 **10. Assemble the Crew with @crew Decorator**  
```python
    @crew
    def crew(self) -> Crew:
        return Crew(
            agents=self.agents,  # Automatically gathered from @agent methods
            tasks=self.tasks,    # Automatically gathered from @task methods
            process=Process.sequential,  # Execute tasks one after another
            verbose=True,
        )
```
✅ `@crew`: Defines the **final crew** combining agents and tasks.  
📌 **Purpose:** Specifies that tasks should be performed **sequentially** (one after another).  
🗣️ `verbose=True`: Shows the workflow step-by-step in logs.

---

## ⚒️ **How Everything Works Together**  
When you run this crew:  
1️⃣ The **writer** generates an article.  
2️⃣ The **editor** reviews and improves it.  
3️⃣ Extra processing happens after all tasks (like adding SEO notes).  

---

## 💡 **Real-World Use Cases for CrewAI Crews**  
1️⃣ **E-commerce Automation:** Managing product uploads, descriptions, and promotions.  
2️⃣ **Customer Support:** Chatbots for answering FAQs and escalating complex issues.  
3️⃣ **AI Research:** Automating data collection, analysis, and report generation.  

---

## 💬 **Summary of Key Decorators**  
| 🚀 **Decorator**        | 🎯 **Purpose**                                     |
|-------------------------|----------------------------------------------------|
| `@CrewBase`             | Marks the class as the main crew structure.        |
| `@agent`                | Defines a method that returns an Agent object.     |
| `@task`                 | Defines a method that returns a Task object.       |
| `@crew`                 | Assembles agents and tasks into a Crew object.     |
| `@before_kickoff`       | Executes logic **before** tasks start.             |
| `@after_kickoff`        | Executes logic **after** tasks finish.             |

---

## 🎉 **Conclusion**  
By now, you should understand:  
✅ How to define agents and tasks using YAML.  
✅ How decorators simplify the process of creating crews.  
✅ Real-world scenarios where CrewAI can automate workflows.  

💬 **Got questions or need more examples? Feel free to ask!** 🚀

# 3. creating crews using Direct Code Definition

# 🚀 **Defining Crews in CrewAI Using Direct Code Definition**  

CrewAI allows us to create **intelligent multi-agent workflows** for handling complex tasks. Instead of using **YAML files** to configure agents and tasks, we can define everything **directly in Python code**.  

This guide will **explain this concept in detail**, covering:  
✅ **How to create agents and tasks directly in Python**  
✅ **Real-world applications**  
✅ **Step-by-step code explanation**  
✅ **How to access Crew Output efficiently**  

---

# 🎯 **1. What is Direct Code Definition?**  

Instead of defining agents and tasks in separate **YAML configuration files**, we can write everything inside a **Python class**. This approach gives us **more control** but may be harder to maintain for **larger projects**.  

---

# 🌍 **2. Real-World Example: AI-Powered Market Analysis**  

### ✅ **Use Case: AI Market Research Team**  
Imagine a company wants to **analyze market trends and competition**. We can create an **AI-powered team** consisting of:  
🔹 **A Data Analyst** → Extracts and analyzes market trends 📊  
🔹 **A Market Researcher** → Gathers insights on competitors and industry changes 🔎  

---

# 💻 **3. Step-by-Step Code Explanation**  

Below is a Python implementation of **Direct Code Definition** for CrewAI.  

```python
from crewai import Agent, Crew, Task, Process
from crewai_tools import YourCustomTool  # Custom AI tool (optional)

class MarketResearchCrew:
    """A CrewAI team for market research and trend analysis"""

    def agent_one(self) -> Agent:
        """Defines a Data Analyst Agent"""
        return Agent(
            role="Data Analyst",
            goal="Analyze data trends in the market",
            backstory="An experienced data analyst with a background in economics",
            verbose=True,
            tools=[YourCustomTool()]  # AI-powered tool for data analysis
        )

    def agent_two(self) -> Agent:
        """Defines a Market Researcher Agent"""
        return Agent(
            role="Market Researcher",
            goal="Gather information on market dynamics",
            backstory="A diligent researcher with a keen eye for detail",
            verbose=True
        )

    def task_one(self) -> Task:
        """Defines Task 1: Collecting Market Data"""
        return Task(
            description="Collect recent market data and identify trends.",
            expected_output="A report summarizing key trends in the market.",
            agent=self.agent_one()  # Assigns the task to the Data Analyst
        )

    def task_two(self) -> Task:
        """Defines Task 2: Researching Market Factors"""
        return Task(
            description="Research factors affecting market dynamics.",
            expected_output="An analysis of factors influencing the market.",
            agent=self.agent_two()  # Assigns the task to the Market Researcher
        )

    def crew(self) -> Crew:
        """Defines the CrewAI workflow"""
        return Crew(
            agents=[self.agent_one(), self.agent_two()],  # List of agents
            tasks=[self.task_one(), self.task_two()],  # List of tasks
            process=Process.sequential,  # Executes tasks one after another
            verbose=True
        )

# Create a crew instance and execute
market_research_crew = MarketResearchCrew().crew()
result = market_research_crew.kickoff()
print(result)
```

---

# 🔍 **4. Breaking Down the Code**  

### 📌 **Step 1: Import Required Libraries**  
```python
from crewai import Agent, Crew, Task, Process
from crewai_tools import YourCustomTool  # Custom AI tool (optional)
```
🔹 `crewai` → Provides core classes like `Agent`, `Crew`, `Task`, and `Process`.  
🔹 `crewai_tools` → Allows integration of AI-powered tools for enhanced performance.  

---

### 📌 **Step 2: Define a Class for the Crew**  
```python
class MarketResearchCrew:
    """A CrewAI team for market research and trend analysis"""
```
🔹 Defines a **class** named `MarketResearchCrew` that organizes agents and tasks.  

---

### 📌 **Step 3: Create Agent 1 - Data Analyst**  
```python
def agent_one(self) -> Agent:
    """Defines a Data Analyst Agent"""
    return Agent(
        role="Data Analyst",
        goal="Analyze data trends in the market",
        backstory="An experienced data analyst with a background in economics",
        verbose=True,
        tools=[YourCustomTool()]  # AI-powered tool for data analysis
    )
```
🔹 **Role:** Data Analyst  
🔹 **Goal:** Analyzes market data and trends  
🔹 **Backstory:** Has experience in economics  
🔹 **Tools:** Uses `YourCustomTool()` for data analysis  
🔹 **Verbose:** Enables detailed output logging  

---

### 📌 **Step 4: Create Agent 2 - Market Researcher**  
```python
def agent_two(self) -> Agent:
    """Defines a Market Researcher Agent"""
    return Agent(
        role="Market Researcher",
        goal="Gather information on market dynamics",
        backstory="A diligent researcher with a keen eye for detail",
        verbose=True
    )
```
🔹 **Role:** Market Researcher  
🔹 **Goal:** Gathers market intelligence  
🔹 **Backstory:** Skilled in competitive research  

---

### 📌 **Step 5: Define Task 1 - Collect Market Data**  
```python
def task_one(self) -> Task:
    """Defines Task 1: Collecting Market Data"""
    return Task(
        description="Collect recent market data and identify trends.",
        expected_output="A report summarizing key trends in the market.",
        agent=self.agent_one()  # Assigns the task to the Data Analyst
    )
```
🔹 **Description:** Gathers latest market data  
🔹 **Expected Output:** Generates a report summarizing key trends  
🔹 **Assigned To:** `agent_one()` (Data Analyst)  

---

### 📌 **Step 6: Define Task 2 - Research Market Factors**  
```python
def task_two(self) -> Task:
    """Defines Task 2: Researching Market Factors"""
    return Task(
        description="Research factors affecting market dynamics.",
        expected_output="An analysis of factors influencing the market.",
        agent=self.agent_two()  # Assigns the task to the Market Researcher
    )
```
🔹 **Description:** Studies market dynamics  
🔹 **Expected Output:** Analysis of market influences  
🔹 **Assigned To:** `agent_two()` (Market Researcher)  

---

### 📌 **Step 7: Create the Crew Workflow**  
```python
def crew(self) -> Crew:
    """Defines the CrewAI workflow"""
    return Crew(
        agents=[self.agent_one(), self.agent_two()],  # List of agents
        tasks=[self.task_one(), self.task_two()],  # List of tasks
        process=Process.sequential,  # Executes tasks one after another
        verbose=True
    )
```
🔹 **Defines a Crew** with:  
✔ Two **agents** (`Data Analyst`, `Market Researcher`)  
✔ Two **tasks** (`task_one()`, `task_two()`)  
✔ **Sequential execution** (one task after another)  

---

# 📊 **5. Understanding Crew Output**  

When a **Crew** executes, its results are stored in the **CrewOutput class**, which contains:  

| **Attribute**  | **Type** | **Description** |
|--------------|--------|--------------|
| `raw` | `str` | Raw output of the crew |
| `pydantic` | `Optional[BaseModel]` | Structured Pydantic model output |
| `json_dict` | `Optional[Dict]` | JSON-formatted output |
| `tasks_output` | `List[TaskOutput]` | Individual task results |
| `token_usage` | `Dict` | AI model token usage |

### ✅ **Example: Convert Output to JSON**  
```python
crew_output = market_research_crew.kickoff()
print(crew_output.json())  # Returns output as JSON
```

---

# 🚀 **6. Summary & Next Steps**  

✅ **Direct Code Definition** gives more control but is harder to maintain in large projects.  
✅ **Ideal for AI-driven automation** (e.g., Market Research, Financial Analysis, etc.).  
✅ **Easier debugging since everything is in Python (no YAML required).**  

Now, try modifying the **roles** or **tasks** and see how your CrewAI agents interact! 🚀

# 4. Accessing Crew Outputs

Here's a detailed, beginner-friendly explanation of **Accessing Crew Outputs in CrewAI**, with real-world applications, code examples, and step-by-step explanations.  

---

# 🚀 **Accessing Crew Outputs in CrewAI**  

## 📌 **What is Crew Output?**  
When a **Crew** (a set of AI agents working together) executes tasks, it generates an **output**. This output can be accessed through the `output` attribute of the **Crew** object.  

The output can take different forms, including:  
✔️ **Raw Output** – Plain text output from the execution.  
✔️ **JSON Output** – Structured JSON data.  
✔️ **Pydantic Model** – A structured representation using Pydantic.  
✔️ **Tasks Output** – Results from individual tasks.  
✔️ **Token Usage** – Insights into the language model’s performance.  

---

## 🏭 **Real-World Example**  
Imagine an AI-powered **news article generator**:  
- **Research Agent** gathers recent news.  
- **Writer Agent** creates a structured article.  
- The **Crew Output** contains the final news article, logs, and performance metrics.  

---

## 🖥️ **Code Example: Accessing Crew Outputs**  

### **🔹 Step 1: Define the Crew**
```python
from crewai import Crew, Agent, Task
import json

# Define agents
research_agent = Agent(
    role="Researcher",
    goal="Find recent tech news articles",
    backstory="An AI-powered research assistant skilled in analyzing news trends",
    verbose=True
)

writer_agent = Agent(
    role="Content Writer",
    goal="Write a structured news article based on research",
    backstory="An AI writer specializing in technology news",
    verbose=True
)

# Define tasks
research_task = Task(
    description="Search the internet for the latest technology trends",
    expected_output="A summary of recent tech news",
    agent=research_agent
)

write_article_task = Task(
    description="Write a news article based on research findings",
    expected_output="A well-structured article",
    agent=writer_agent
)

# Create a crew with agents and tasks
crew = Crew(
    agents=[research_agent, writer_agent],
    tasks=[research_task, write_article_task],
    verbose=True
)
```

### **🔹 Step 2: Execute the Crew and Access Output**
```python
# Execute the crew
crew_output = crew.kickoff()

# Access the different formats of crew output
print(f"📄 Raw Output: {crew_output.raw}")

# If output is available in JSON format, print it
if crew_output.json_dict:
    print(f"📊 JSON Output: {json.dumps(crew_output.json_dict, indent=2)}")

# If output is available as a Pydantic model, print it
if crew_output.pydantic:
    print(f"🛠️ Pydantic Output: {crew_output.pydantic}")

# Display individual task outputs
print(f"✅ Tasks Output: {crew_output.tasks_output}")

# Show token usage for performance insights
print(f"🔢 Token Usage: {crew_output.token_usage}")
```

---

## 📜 **Explanation of Code**
1️⃣ **Define Agents**:  
   - `research_agent` gathers news.  
   - `writer_agent` writes the article.  

2️⃣ **Create Tasks**:  
   - `research_task` searches for news.  
   - `write_article_task` writes the article.  

3️⃣ **Define the Crew**:  
   - The crew consists of the agents and their tasks.  

4️⃣ **Execute the Crew**:  
   - `.kickoff()` runs the crew.  

5️⃣ **Access Output**:  
   - `.raw` → Displays plain text output.  
   - `.json_dict` → Shows structured JSON output.  
   - `.pydantic` → Provides a structured model.  
   - `.tasks_output` → Shows individual task results.  
   - `.token_usage` → Displays LLM performance metrics.  

---

# 📂 **Accessing Crew Logs**
### **🔹 Why Logs Are Important?**
Crew logs track execution steps in real time. This is useful for:  
✔️ Debugging errors  
✔️ Tracking AI decision-making  
✔️ Analyzing execution patterns  

### **🔹 Code Example: Saving Logs**
```python
# Save logs as logs.txt
crew = Crew(output_log_file=True)  

# Save logs with a specific file name
crew = Crew(output_log_file="crew_execution_log")  

# Save logs as JSON
crew = Crew(output_log_file="crew_log.json")  
```

---

# 🧠 **Memory Utilization in CrewAI**
### **🔹 What is Memory Utilization?**
Memory allows AI agents to remember previous executions.  
Types of memory:  
✔️ **Short-term Memory** – Stores recent execution data.  
✔️ **Long-term Memory** – Stores knowledge across sessions.  
✔️ **Entity Memory** – Stores details about entities (e.g., customer info).  

🔸 **Example Usage:**  
- A chatbot remembers past conversations.  
- A research agent recalls previous findings.  

---

# ⚡ **Cache Utilization in CrewAI**
### **🔹 What is Cache Utilization?**
Caching stores previously computed results to avoid repeating identical tasks, making the process more efficient.  

🔸 **Example Usage:**  
- A market research tool caches past reports.  
- A stock analysis bot stores past stock trend calculations.  

---

# 📊 **Crew Usage Metrics**
### **🔹 What are Usage Metrics?**
After execution, `usage_metrics` provides insights into:  
✔️ **Tokens Used** – Measures AI model efficiency.  
✔️ **Execution Time** – Tracks task duration.  
✔️ **Resource Consumption** – Monitors system usage.  

### **🔹 Code Example: Viewing Metrics**
```python
# Execute the crew
crew.kickoff()

# Print crew execution metrics
print(f"📈 Usage Metrics: {crew.usage_metrics}")
```

---

# 🔄 **Crew Execution Process**
### **1️⃣ Sequential Process**  
- Tasks are executed **one after another**.  
- Example: A **blog writing crew** first researches, then writes.  

### **2️⃣ Hierarchical Process**  
- A **Manager Agent** oversees task execution.  
- Example: A **customer service AI** first categorizes queries before responding.  

🔹 **Code Example: Hierarchical Execution**
```python
crew = Crew(
    agents=[manager_agent, research_agent, writer_agent],
    tasks=[task1, task2, task3],
    process=Process.hierarchical
)
```

---

# 🎯 **Conclusion**
✔️ CrewAI outputs provide structured data from AI-powered workflows.  
✔️ Logs help track execution steps for debugging.  
✔️ Memory and cache enhance efficiency.  
✔️ Metrics measure performance.  
✔️ Execution processes can be **sequential** or **hierarchical**.  

🚀 **Now you can build and optimize AI-powered crews like a pro!**

# 5. Different Ways to Kick Off a Crew

# 🚀 **Kicking Off a Crew in CrewAI**  

Once your **Crew** (a group of AI agents working together) is set up, you need to start the execution process. This is done using the `kickoff()` method, which begins the workflow based on the defined **process flow**.  

CrewAI provides **four** different ways to kick off a crew, allowing for both **synchronous** and **asynchronous** execution.  

Let’s dive deep into each method, **real-world applications**, **code examples**, and step-by-step explanations.  

---

# 📌 **1. What is Crew Kickoff?**  

The **kickoff process** is how we start our CrewAI agents to perform their assigned tasks. It can be:  
✔️ **Synchronous (Normal Execution)** – Tasks execute one after another.  
✔️ **Asynchronous (Parallel Execution)** – Tasks execute in parallel for efficiency.  

🛠️ **Real-World Example:**  
Imagine an AI-powered **Content Creation Team** 🚀:  
- **Research Agent** gathers news.  
- **Writing Agent** writes an article.  
- **Review Agent** proofreads it.  
Each step can be executed **synchronously (one after another)** or **asynchronously (simultaneously)**.  

---

# 🔹 **2. Basic Kickoff – Synchronous Execution**  
### 📌 **What is `kickoff()`?**  
`kickoff()` starts the execution process in a linear, **step-by-step manner**. Each task **waits** for the previous one to complete before moving forward.  

### 🖥 **Code Example: Basic Kickoff**
```python
from crewai import Crew, Agent, Task

# Define Agents
research_agent = Agent(
    role="Researcher",
    goal="Find recent AI trends",
    backstory="AI-powered assistant for research",
    verbose=True
)

writer_agent = Agent(
    role="Writer",
    goal="Write an article based on research",
    backstory="AI-driven content writer",
    verbose=True
)

# Define Tasks
research_task = Task(
    description="Research the latest AI trends",
    expected_output="A summary of AI advancements",
    agent=research_agent
)

write_task = Task(
    description="Write an article based on the research",
    expected_output="A structured AI article",
    agent=writer_agent
)

# Create Crew
my_crew = Crew(
    agents=[research_agent, writer_agent],
    tasks=[research_task, write_task],
    verbose=True
)

# 🚀 Kickoff Execution
result = my_crew.kickoff()

# Display Results
print(f"📄 Final Output: {result}")
```

---

# 🔹 **3. Handling Multiple Inputs – `kickoff_for_each()`**  
### 📌 **What is `kickoff_for_each()`?**  
- Executes the **same task multiple times**, each with different input.  
- **Useful for batch processing** (e.g., writing multiple articles on different topics).  

### 🖥 **Code Example: Processing Multiple Inputs**
```python
# Define multiple inputs
inputs_array = [
    {'topic': 'AI in Healthcare'},
    {'topic': 'AI in Finance'}
]

# 🚀 Execute for each input separately
results = my_crew.kickoff_for_each(inputs=inputs_array)

# Display Results
for result in results:
    print(f"📝 Processed Output: {result}")
```
**🛠 Real-World Example:**  
An AI-driven **news agency** can generate **multiple** articles for different industries in one go.  

---

# 🔹 **4. Asynchronous Execution – `kickoff_async()`**  
### 📌 **What is `kickoff_async()`?**  
- Runs tasks **without waiting** for them to complete.  
- Ideal for **speed and efficiency** when working with large data.  

### 🖥 **Code Example: Asynchronous Execution**
```python
# Define input
inputs = {'topic': 'AI in Healthcare'}

# 🚀 Execute asynchronously
async_result = my_crew.kickoff_async(inputs=inputs)

# Display Result
print(f"🔄 Async Output: {async_result}")
```
**🛠 Real-World Example:**  
An AI **data scraper** can **gather news** from different websites **simultaneously**, rather than waiting for each request to complete.  

---

# 🔹 **5. Parallel Execution – `kickoff_for_each_async()`**  
### 📌 **What is `kickoff_for_each_async()`?**  
- Executes **multiple inputs asynchronously**, leveraging **parallel processing**.  
- **Best for large-scale automation** where multiple AI agents need to work simultaneously.  

### 🖥 **Code Example: Asynchronous Processing for Multiple Inputs**
```python
# Define multiple inputs
inputs_array = [
    {'topic': 'AI in Healthcare'},
    {'topic': 'AI in Finance'}
]

# 🚀 Execute asynchronously for each input
async_results = my_crew.kickoff_for_each_async(inputs=inputs_array)

# Display Results
for async_result in async_results:
    print(f"⚡ Async Processed Output: {async_result}")
```
**🛠 Real-World Example:**  
A **market research tool** can collect **real-time data** for **multiple industries** in parallel, rather than one at a time.  

---

# 🎯 **6. Choosing the Right Kickoff Method**
| Kickoff Method               | Execution Type | Best For |
|------------------------------|---------------|----------|
| `kickoff()`                   | Synchronous   | Normal sequential execution |
| `kickoff_for_each()`          | Synchronous   | Batch processing (one-by-one) |
| `kickoff_async()`             | Asynchronous  | Running single tasks faster |
| `kickoff_for_each_async()`    | Asynchronous  | High-speed parallel execution |

---

# 📌 **7. Summary**
✔️ **`kickoff()`** – Runs tasks **step by step** (synchronous).  
✔️ **`kickoff_for_each()`** – Runs the same task **multiple times** for different inputs.  
✔️ **`kickoff_async()`** – Runs tasks **in parallel** without waiting.  
✔️ **`kickoff_for_each_async()`** – **Best for large-scale parallel processing**.  

🚀 **Now you know how to efficiently execute AI-powered workflows using CrewAI!**

---
# 6. Replaying from a Specific Task 
# 🔄 **Replaying from a Specific Task in CrewAI**  

When working with **CrewAI**, sometimes you may want to **replay** a specific task instead of running the entire process from the beginning. This is useful when debugging, optimizing, or **retrying a failed task** without re-executing the whole workflow.  

The **replay feature** allows you to **restart from a specific task** using the **CLI (Command Line Interface)**.  

---

# 📌 **1. Why Use the Replay Feature?**  

🔹 **Avoid redundant execution** – No need to restart the entire workflow.  
🔹 **Debug efficiently** – Easily fix issues in a specific task.  
🔹 **Optimize workflows** – Quickly test improvements in a single step.  
🔹 **Retain previous context** – CrewAI keeps track of past executions, ensuring continuity.  

🛠 **Real-World Example:**  
Imagine you're using CrewAI to automate **blog writing** with these tasks:  
1️⃣ **Research topic**  
2️⃣ **Write draft**  
3️⃣ **Proofread draft**  
4️⃣ **Generate final article**  

If the **proofreading step fails** due to a formatting issue, you don't want to restart **from research**—you want to **fix and replay from proofreading**.  

---

# 🔹 **2. How Replay Works in CrewAI**  
CrewAI **automatically saves** the latest kickoff task outputs **locally**, so you can **restart from any task** using its unique **Task ID**.  

🎯 **Key Concepts:**  
✔️ Each task in CrewAI has a **Task ID**.  
✔️ You can **replay a specific task** using this Task ID.  
✔️ The replay maintains context, meaning **previous completed tasks remain unchanged**.  

---

# 🔹 **3. Finding Task IDs Before Replaying**  
Before replaying a task, you need to find the **Task ID** of the latest execution.  

🖥 **Command to List Task IDs:**  
```bash
crewai log-tasks-outputs
```
✅ **What this does:**  
- Shows **all previous task executions**.  
- Displays **Task IDs** you can replay.  

---

# 🔹 **4. Replaying a Specific Task**  
Once you have the **Task ID**, use the `replay` command to restart from that task.  

🖥 **Command to Replay a Task:**  
```bash
crewai replay -t <task_id>
```
🔹 Replace `<task_id>` with the actual **Task ID** from the log.  

---

# 🔹 **5. Step-by-Step Guide to Replay a Task**  
### ✅ **Step 1: Open Terminal**  
Open your **command prompt** or **terminal**.  

### ✅ **Step 2: Navigate to Project Directory**  
Move to the folder where your CrewAI project is located.  
```bash
cd /path/to/your/crewai/project
```

### ✅ **Step 3: View Previous Task Outputs**  
Get the **Task IDs** of previously executed tasks.  
```bash
crewai log-tasks-outputs
```
💡 **Example Output:**  
```
Task ID: task_123 - Research completed
Task ID: task_456 - Writing completed
Task ID: task_789 - Proofreading failed
```

### ✅ **Step 4: Replay from a Specific Task**  
Let’s say **proofreading failed**, and its Task ID is `task_789`.  
To restart from **proofreading**, run:  
```bash
crewai replay -t task_789
```

---

# 🎯 **6. Real-World Use Cases for Replaying Tasks**
| **Scenario** | **How Replay Helps** |
|-------------|------------------|
| 📝 **Blog Writing Workflow** | Replay the **proofreading step** instead of starting from research. |
| 📊 **Data Processing Pipeline** | Rerun the **data analysis step** without fetching data again. |
| 🤖 **Chatbot Development** | Fix and replay **intent detection** without restarting conversation logs. |
| 🚀 **AI-Powered Marketing Automation** | Adjust and replay the **email generation** task only. |

---

# 📌 **7. Summary**
✅ **Replay allows restarting a failed or modified task** without redoing everything.  
✅ **Task outputs are saved automatically**, so you can reference them.  
✅ **Use `crewai log-tasks-outputs`** to find Task IDs.  
✅ **Use `crewai replay -t <task_id>`** to restart from a specific step.  
✅ **Maintains execution context**, ensuring previously completed tasks remain unchanged.  

🚀 **Now you can efficiently debug and optimize your AI workflows using CrewAI’s replay feature!** 🎯