# 🧠 Knowledge in CrewAI – A Beginner-Friendly Guide  

Knowledge in **CrewAI** is a way to provide AI agents with external information so they can make informed decisions and generate more accurate responses. Think of it as giving your AI assistant access to a **library** where it can look up details when needed.  

---

## 🏆 **What is Knowledge in CrewAI?**  

In CrewAI, **Knowledge** refers to external data sources that AI agents can use during their tasks. These knowledge sources help AI agents:  

✅ **Enhance domain expertise** – AI agents can specialize in specific fields (e.g., finance, healthcare).  
✅ **Support decision-making** – AI can refer to stored data for fact-based answers.  
✅ **Maintain context** – Information persists across conversations.  
✅ **Generate factual responses** – Reduces hallucinations by grounding responses in real data.  

**Example Use Case:**  
Imagine you're building a **customer support chatbot** for an e-commerce store. Instead of relying only on its pre-trained knowledge, the chatbot can **access stored product details, return policies, and FAQs** to provide accurate responses to customers.  

---

## 📂 **Supported Knowledge Sources in CrewAI**  

CrewAI supports various **file formats and data structures** as knowledge sources:  

### 📝 **Text-Based Knowledge**  
- **Raw Strings** (plain text stored in code)  
- **Text Files (.txt)**  
- **PDF Documents**  

### 📊 **Structured Data Sources**  
- **CSV Files** (spreadsheet data)  
- **Excel Files (.xlsx)**  
- **JSON Documents** (API responses, configurations)  

---

## ⚙️ **Knowledge Parameters in CrewAI**  

CrewAI allows configuring **knowledge storage** using specific parameters:  

| 🏷️ **Parameter** | 🛠️ **Type** | ✅ **Required?** | 📌 **Description** |
|---------------|-----------|--------------|----------------|
| `sources` | `List[BaseKnowledgeSource]` | **Yes** | List of knowledge sources (e.g., PDFs, CSV, JSON, text files). |
| `collection_name` | `str` | **No** | Name of the stored knowledge collection (default: `"knowledge"`). |
| `storage` | `Optional[KnowledgeStorage]` | **No** | Custom storage configuration for managing data retrieval. |

---

## 🚀 **Getting Started with CrewAI Knowledge**  

To use knowledge in CrewAI, follow these steps:  

1️⃣ **Define a Knowledge Source** (e.g., string, file, or structured data).  
2️⃣ **Create an AI Agent** that will use this knowledge.  
3️⃣ **Assign a Task** to the agent.  
4️⃣ **Create a Crew** with the agent, task, and knowledge source.  
5️⃣ **Execute the Task** and get results.  

---

## 📝 **Code Example: String-Based Knowledge**  

Let’s build a simple **CrewAI system** where an agent has knowledge about a user and answers questions based on that information.  

```python
from crewai import Agent, Task, Crew, Process, LLM
from crewai.knowledge.source.string_knowledge_source import StringKnowledgeSource

# 1️⃣ Create a knowledge source (text-based)
content = "User's name is John. He is 30 years old and lives in San Francisco."
string_source = StringKnowledgeSource(content=content)

# 2️⃣ Initialize a Language Model (LLM) with temperature 0 (for deterministic answers)
llm = LLM(model="gpt-4o-mini", temperature=0)

# 3️⃣ Create an Agent who will use the knowledge source
agent = Agent(
    role="User Information Expert",
    goal="Provide accurate details about the user.",
    backstory="You specialize in remembering user details and answering questions about them.",
    verbose=True,
    allow_delegation=False,
    llm=llm,
)

# 4️⃣ Define a Task that the Agent will perform
task = Task(
    description="Answer the following questions about the user: {question}",
    expected_output="A factual answer to the question.",
    agent=agent,
)

# 5️⃣ Create a Crew that manages the Agent, Task, and Knowledge
crew = Crew(
    agents=[agent],
    tasks=[task],
    verbose=True,
    process=Process.sequential,
    knowledge_sources=[string_source],  # Attach the knowledge source here
)

# 6️⃣ Ask the AI a question about the user
result = crew.kickoff(inputs={"question": "What city does John live in and how old is he?"})

# 7️⃣ Print the result
print(result)
```

---

### 🔍 **Understanding the Code**  

✅ **Step 1: Define a Knowledge Source**  
- We create a `StringKnowledgeSource` with user information.  
- This acts like **stored memory** for the AI.  

✅ **Step 2: Initialize the LLM**  
- We use `gpt-4o-mini` with `temperature=0` to **ensure deterministic (consistent) outputs**.  

✅ **Step 3: Create an Agent**  
- The agent has a **role, goal, and backstory** defining its expertise.  
- This agent **does not delegate tasks** and will always answer directly.  

✅ **Step 4: Define a Task**  
- The task tells the agent what to do:  
  - It takes a **user’s question** as input.  
  - It **returns a factual response** based on knowledge.  

✅ **Step 5: Create a Crew**  
- A Crew manages multiple **agents and tasks**.  
- We specify a **sequential process**, meaning tasks are executed **one by one**.  
- The **knowledge source is attached** to make the agent knowledgeable.  

✅ **Step 6 & 7: Execute and Retrieve Answer**  
- The Crew **executes the task** and **retrieves the answer**.  
- If asked `"Where does John live and how old is he?"`, the AI will return:  
  - **"John lives in San Francisco and he is 30 years old."**  

---

## 📌 **Real-World Example: Using Knowledge in Customer Support**  

Let’s say you are building an **AI-powered customer support assistant** for an **e-commerce store**.  

🔹 **Problem:**  
Customers ask about **product details, return policies, and shipping information**. Instead of hardcoding every response, we can **store this knowledge in CrewAI** so the bot can answer based on actual data.  

🔹 **Solution:**  
We can store:  
✅ **Product details** in JSON.  
✅ **Return & refund policies** in a text file.  
✅ **Order tracking information** in a CSV file.  

🔹 **Example Interaction:**  

**Customer:** "What is the return policy for electronics?"  
**AI Response:** "Electronics can be returned within 30 days if unopened. Please provide your order ID for further assistance."  

By **integrating CrewAI Knowledge**, the chatbot provides **instant, accurate responses** without needing predefined answers.  

---

## 🎯 **Conclusion**  

💡 **CrewAI’s Knowledge System** is a game-changer for AI-powered applications. It allows agents to:  

✅ Store and retrieve information from **multiple sources**  
✅ Generate **accurate, real-world answers**  
✅ Maintain **context across conversations**  

Whether you’re building **AI chatbots, virtual assistants, or automation tools**, **CrewAI’s knowledge feature helps AI make smarter, more informed decisions.**  

🚀 **Ready to get started? Try implementing CrewAI Knowledge in your own projects today!**

# 2. Types of Knowledge Sources in CrewAI

# 📚 Understanding Knowledge Sources in CrewAI  

CrewAI provides a powerful **knowledge management system** that allows AI agents to access and utilize external data sources, making them more informed and capable. This guide will help you understand the **concept of knowledge in CrewAI**, how to use different **knowledge sources**, and implement them in **real-world applications** with **code examples and explanations**.  

---

## 🧠 What is Knowledge in CrewAI?  

Knowledge in **CrewAI** refers to external information that AI agents can use while performing tasks. Instead of relying **only on pre-trained models**, CrewAI enables agents to **fetch and process** information from various sources like **text files, PDFs, CSVs, JSON files, and even online documents**.  

### ✅ **Why Use Knowledge in AI Agents?**  
Using knowledge sources helps AI agents:  
✔ **Enhance responses** with domain-specific data.  
✔ **Answer questions based on real-world facts.**  
✔ **Support decision-making** with structured information.  
✔ **Avoid hallucinations** by grounding responses in real documents.  
✔ **Maintain context** across different interactions.  

---

## 📂 **Types of Knowledge Sources in CrewAI**  

CrewAI supports multiple knowledge sources out of the box:  

| 📜 Source Type  | 🔍 Description |
|----------------|--------------|
| **String-Based** | Directly use a string as a knowledge source. |
| **Text Files** (.txt) | Store knowledge in plain text files. |
| **PDF Documents** (.pdf) | Extract and use text from PDFs. |
| **CSV Files** (.csv) | Use structured tabular data. |
| **Excel Files** (.xlsx) | Process spreadsheets with multiple sheets. |
| **JSON Files** (.json) | Fetch and process structured JSON data. |
| **Web Documents** (Docling) | Extract knowledge from online articles or research papers. |

---

## 🚀 **Getting Started with CrewAI Knowledge Sources**  

Before implementing knowledge sources, ensure you have **CrewAI** installed:  

```bash
pip install crewai
```

For **Docling (web document sources)**, install the required library:  

```bash
uv add docling
```

---

## 🌐 **Using Online Documents as Knowledge Sources (Docling)**  

### 🔹 **Scenario:**  
Imagine you want an AI agent to analyze research papers on **Reward Hacking** and **AI Hallucinations** from online sources.  

### ✅ **Code Implementation**  

```python
from crewai import LLM, Agent, Crew, Process, Task
from crewai.knowledge.source.crew_docling_source import CrewDoclingSource

# 🌍 Step 1: Create a Knowledge Source from Online Documents
content_source = CrewDoclingSource(
    file_paths=[
        "https://lilianweng.github.io/posts/2024-11-28-reward-hacking",
        "https://lilianweng.github.io/posts/2024-07-07-hallucination",
    ],
)

# 🧠 Step 2: Define a Language Model (LLM)
llm = LLM(model="gpt-4o-mini", temperature=0)

# 🤖 Step 3: Create an AI Agent with Access to Knowledge
agent = Agent(
    role="Research Paper Expert",
    goal="You know everything about the provided research papers.",
    backstory="""You are a highly knowledgeable AI that specializes in reading and summarizing academic research papers.""",
    verbose=True,
    allow_delegation=False,
    llm=llm,
)

# 📋 Step 4: Define a Task for the Agent
task = Task(
    description="Answer the following questions about the research papers: {question}",
    expected_output="An answer to the question with proper references.",
    agent=agent,
)

# 🚀 Step 5: Create a Crew and Assign the Knowledge Source
crew = Crew(
    agents=[agent],
    tasks=[task],
    verbose=True,
    process=Process.sequential,
    knowledge_sources=[content_source],  # Adding the knowledge source
)

# 🎯 Step 6: Run the AI Agent to Answer a Research-Related Question
result = crew.kickoff(
    inputs={
        "question": "What is the reward hacking paper about? Be sure to provide sources."
    }
)
```

---

## 🔎 **Code Explanation**  

1️⃣ **Define a Knowledge Source** (`CrewDoclingSource`)  
   - We specify **two research paper links** as sources.  
   - The AI will extract and process content from these URLs.  

2️⃣ **Create an LLM**  
   - We use `gpt-4o-mini` with `temperature=0` to ensure **deterministic outputs** (consistent responses).  

3️⃣ **Define an AI Agent**  
   - The agent is responsible for **reading, understanding, and answering questions** about the research papers.  

4️⃣ **Define a Task**  
   - The agent answers **user queries** related to the research papers.  

5️⃣ **Create a Crew**  
   - We add the agent, assign the task, and include the **knowledge source** so that the AI can use it.  

6️⃣ **Execute the AI Workflow**  
   - We provide a question, and the agent **fetches information from the research papers** before answering.  

---

## 📑 **Using Other Types of Knowledge Sources in CrewAI**  

### 📄 **1. Using Text File Knowledge Sources**  

```python
from crewai.knowledge.source.text_file_knowledge_source import TextFileKnowledgeSource

# Load knowledge from text files
text_source = TextFileKnowledgeSource(
    file_paths=["document.txt", "another.txt"]
)

agent = Agent(
    ...
    knowledge_sources=[text_source]
)

crew = Crew(
    ...
    knowledge_sources=[text_source]
)
```
🔹 **Example Use Case:** AI chatbot that reads company policies from `.txt` files.  

---

### 📝 **2. Using PDF Documents as Knowledge Sources**  

```python
from crewai.knowledge.source.pdf_knowledge_source import PDFKnowledgeSource

# Load knowledge from PDFs
pdf_source = PDFKnowledgeSource(
    file_paths=["document.pdf", "report.pdf"]
)

agent = Agent(
    ...
    knowledge_sources=[pdf_source]
)

crew = Crew(
    ...
    knowledge_sources=[pdf_source]
)
```
🔹 **Example Use Case:** AI legal assistant that reads **contract PDFs** to answer questions.  

---

### 📊 **3. Using CSV Files as Knowledge Sources**  

```python
from crewai.knowledge.source.csv_knowledge_source import CSVKnowledgeSource

# Load knowledge from CSV files
csv_source = CSVKnowledgeSource(
    file_paths=["data.csv"]
)

agent = Agent(
    ...
    knowledge_sources=[csv_source]
)

crew = Crew(
    ...
    knowledge_sources=[csv_source]
)
```
🔹 **Example Use Case:** AI sales assistant analyzing **customer data** from CSV files.  

---

### 📈 **4. Using Excel Files as Knowledge Sources**  

```python
from crewai.knowledge.source.excel_knowledge_source import ExcelKnowledgeSource

# Load knowledge from Excel files
excel_source = ExcelKnowledgeSource(
    file_paths=["spreadsheet.xlsx"]
)

agent = Agent(
    ...
    knowledge_sources=[excel_source]
)

crew = Crew(
    ...
    knowledge_sources=[excel_source]
)
```
🔹 **Example Use Case:** AI finance assistant extracting **financial reports** from Excel files.  

---

### 🌐 **5. Using JSON Files as Knowledge Sources**  

```python
from crewai.knowledge.source.json_knowledge_source import JSONKnowledgeSource

# Load knowledge from JSON files
json_source = JSONKnowledgeSource(
    file_paths=["data.json"]
)

agent = Agent(
    ...
    knowledge_sources=[json_source]
)

crew = Crew(
    ...
    knowledge_sources=[json_source]
)
```
🔹 **Example Use Case:** AI chatbot fetching **API response data** from JSON files.  

---

## 🎯 **Real-World Use Cases for Knowledge Sources in CrewAI**  

✅ **Customer Support AI** → Uses **PDF manuals** to assist customers.  
✅ **Legal Assistant AI** → Reads **contract PDFs** and gives legal advice.  
✅ **Research AI** → Reads **scientific papers** and provides summaries.  
✅ **E-commerce AI** → Analyzes **Excel/CSV sales data** to generate insights.  
✅ **Finance AI** → Uses **JSON/CSV** to analyze stock trends and forecasts.  

---

## 🚀 **Conclusion**  

Knowledge sources in **CrewAI** allow AI agents to work with **real data** instead of relying solely on pre-trained models. By integrating **files, structured data, and web documents**, AI can become more **context-aware and accurate**.  

Would you like help in implementing CrewAI for your own project? 😊

# 3. Knowledge Configuration 

Here's a detailed and beginner-friendly explanation of the **Knowledge Configuration in CrewAI**, including real-world examples, code breakdowns, and use cases.

---

# 🧠 Understanding Knowledge Configuration in CrewAI

**CrewAI** is a powerful framework that allows AI agents to work with knowledge sources efficiently. To ensure accurate information retrieval, CrewAI offers features like **chunking**, **embedding configuration**, and **knowledge resetting**. 

These features help in processing large documents, improving retrieval accuracy, and customizing how knowledge is stored and accessed.

---

## 📌 **1. Chunking Configuration in CrewAI**
### 🔍 What is Chunking?
When working with large documents, AI models may struggle to process them efficiently. **Chunking** refers to splitting a document into smaller, manageable pieces (**chunks**) for better processing.  

### 🎯 **Why is Chunking Important?**
- ✅ **Handles Large Documents**: AI models have token limits, so breaking documents into chunks ensures smooth processing.
- ✅ **Improves Retrieval Accuracy**: When answering queries, smaller chunks provide precise context.
- ✅ **Maintains Context**: Overlapping chunks help retain information continuity.

---

### 📝 **Code Example: Chunking a String Knowledge Source**
```python
from crewai.knowledge.source.string_knowledge_source import StringKnowledgeSource

# Create a knowledge source with chunking
source = StringKnowledgeSource(
    content="Your content here",
    chunk_size=4000,      # Maximum size of each chunk (default: 4000)
    chunk_overlap=200     # Overlap between chunks (default: 200)
)
```
### 🛠 **Code Explanation**
1. **Import `StringKnowledgeSource`** – This is a module that handles string-based knowledge sources.
2. **Define `content`** – This is the text or document we want to store.
3. **Set `chunk_size=4000`** – Specifies the maximum length of each chunk.
4. **Set `chunk_overlap=200`** – Ensures overlapping context between chunks to maintain continuity.

---

### 🌍 **Real-World Use Case: Where is Chunking Used?**
📖 **Example: AI-powered Legal Document Assistant**  
A law firm uploads large legal contracts. AI processes them by breaking them into chunks for accurate retrieval when answering questions about specific clauses.

---

## 📌 **2. Embeddings Configuration**
### 🔍 **What are Embeddings?**
Embeddings are numerical representations of words and sentences that help AI understand the meaning of text.

### 🎯 **Why Configure an Embedder?**
- ✅ **Improves AI’s Understanding**: Converts text into machine-readable numerical data.
- ✅ **Optimizes Search and Retrieval**: Helps AI find relevant knowledge faster.
- ✅ **Supports Various Providers**: Choose from OpenAI, Google, Cohere, AWS Bedrock, etc.

---

### 📝 **Supported Embedding Providers**
| 🔹 Provider  | 🔹 Description |
|-------------|--------------|
| **openai** | Uses OpenAI’s embedding models |
| **google** | Uses Google’s `text-embedding-004` model |
| **azure** | Azure’s OpenAI embeddings |
| **ollama** | Local embeddings with Ollama |
| **vertexai** | Google Cloud VertexAI embeddings |
| **cohere** | Cohere’s embedding models |
| **voyageai** | VoyageAI’s embedding models |
| **bedrock** | AWS Bedrock embeddings |
| **huggingface** | Open-source Hugging Face models |
| **watson** | IBM Watson embeddings |

---

### 📝 **Code Example: Configuring Google Embeddings**
```python
from crewai import Agent, Task, Crew, Process, LLM
from crewai.knowledge.source.string_knowledge_source import StringKnowledgeSource
import os

# Get the GEMINI API key
GEMINI_API_KEY = os.environ.get("GEMINI_API_KEY")

# Create a knowledge source
content = "Users name is John. He is 30 years old and lives in San Francisco."
string_source = StringKnowledgeSource(
    content=content,
)

# Create an LLM with a temperature of 0 to ensure deterministic outputs
gemini_llm = LLM(
    model="gemini/gemini-1.5-pro-002",
    api_key=GEMINI_API_KEY,
    temperature=0,
)

# Create an agent with the knowledge store and embedding
agent = Agent(
    role="About User",
    goal="You know everything about the user.",
    backstory="""You are a master at understanding people and their preferences.""",
    verbose=True,
    allow_delegation=False,
    llm=gemini_llm,
    embedder={
        "provider": "google",
        "config": {
            "model": "models/text-embedding-004",
            "api_key": GEMINI_API_KEY,
        }
    }
)

# Define a task for the agent
task = Task(
    description="Answer the following questions about the user: {question}",
    expected_output="An answer to the question.",
    agent=agent,
)

# Create a crew with the agent, task, and knowledge source
crew = Crew(
    agents=[agent],
    tasks=[task],
    verbose=True,
    process=Process.sequential,
    knowledge_sources=[string_source],
    embedder={
        "provider": "google",
        "config": {
            "model": "models/text-embedding-004",
            "api_key": GEMINI_API_KEY,
        }
    }
)

# Execute the task
result = crew.kickoff(inputs={"question": "What city does John live in and how old is he?"})
```

---

### 🛠 **Code Explanation**
1. **Import necessary modules** – Includes `Agent`, `Task`, `Crew`, `Process`, and `LLM`.
2. **Get API key from environment** – Uses `os.environ.get("GEMINI_API_KEY")` to access the Google API key.
3. **Create a string knowledge source** – Stores the user's information.
4. **Define an LLM (Language Model)** – Uses Google's `gemini-1.5-pro-002` model.
5. **Create an AI Agent** – The agent specializes in user-related queries.
6. **Embedder Configuration** – Uses `text-embedding-004` from Google.
7. **Define a Task** – The agent is assigned to answer questions about the user.
8. **Create a Crew** – The AI team is assembled with tasks and knowledge sources.
9. **Execute the Task** – `crew.kickoff()` processes a query about John.

---

### 🌍 **Real-World Use Case: Where is Embedding Used?**
🔎 **Example: AI-Powered Resume Screening**  
A hiring platform uses **text embeddings** to compare job descriptions with resumes and find the best candidates.

---

## 📌 **3. Clearing Knowledge in CrewAI**
### 🔍 **Why Reset Knowledge?**
If you update your knowledge sources, you might need to **clear previous data** to ensure agents work with the latest information.

---

### 📝 **Command to Reset Knowledge**
```bash
crewai reset-memories --knowledge
```

### 🎯 **When to Use This?**
- ✅ After updating knowledge sources.
- ✅ When AI provides outdated answers.
- ✅ If switching between different datasets.

---

### 🌍 **Real-World Use Case: Where is Knowledge Reset Used?**
🔄 **Example: AI-Powered Customer Support**  
A chatbot trained on old FAQs can reset its knowledge and learn from the latest support documents to provide up-to-date answers.

---

# 🎯 **Conclusion**
**Knowledge configuration in CrewAI** is crucial for **efficient information retrieval, accurate AI responses, and optimized processing**. The three main components—**chunking, embeddings, and knowledge resetting**—help AI agents work effectively with different data sources.

🚀 **Key Takeaways:**
- **Chunking** breaks large content into smaller pieces for better processing.
- **Embeddings** help AI understand text better using numerical representations.
- **Resetting Knowledge** ensures AI uses the latest data.

By leveraging these features, you can **enhance AI-driven applications** in various fields like customer service, legal research, resume screening, and more! 🎉

---

# 4. Agent-Specific Knowledge

# 🤖 **Understanding Agent-Specific Knowledge in CrewAI**  

In **CrewAI**, agents can have their **own specialized knowledge sources** instead of relying on shared knowledge at the crew level. This means that each agent can be an expert in its specific area, leading to **better decision-making, efficient information retrieval, and role-specific expertise**.  

Let's break this down in detail so that even a beginner can understand, with **real-world examples, code explanations, and a step-by-step breakdown** of how this concept works.

---

# 📌 **1. What is Agent-Specific Knowledge?**  

🔍 **Definition:**  
Agent-specific knowledge allows **each agent to have its own knowledge source** using the `knowledge_sources` parameter. Instead of all agents sharing the same knowledge at the crew level, **each agent can have exclusive knowledge relevant to its role.**  

💡 **Why is this important?**  
- ✅ **Specialized Expertise** – Different agents can have different areas of knowledge.  
- ✅ **Separation of Concerns** – Prevents unnecessary information sharing between agents.  
- ✅ **Better Organization** – Helps in structuring knowledge in a more modular way.  
- ✅ **Layered Information Access** – Agents can use both crew-level and agent-level knowledge.  

---

# 🌍 **2. Real-World Use Case: Where is Agent-Specific Knowledge Used?**  

📞 **Example: AI-Powered Customer Support System**  

Imagine you have a customer support system powered by AI agents.  
- **Support Agent** – Specializes in product specifications and troubleshooting.  
- **Billing Agent** – Has knowledge about payments, invoices, and refunds.  
- **Shipping Agent** – Knows about delivery times, tracking, and shipping policies.  

Each agent should have **only the knowledge relevant to its domain** to provide accurate responses. This prevents confusion and ensures **efficient task handling**.  

For example, if a customer asks about **laptop storage capacity**, only the **Support Agent** should respond, not the **Billing Agent** or **Shipping Agent**.  

---

# 📝 **3. Code Example: Implementing Agent-Specific Knowledge**  

Let's implement a **technical support agent** with **exclusive product knowledge** about a **Dell XPS 13 laptop**.

```python
from crewai import Agent, Task, Crew
from crewai.knowledge.source.string_knowledge_source import StringKnowledgeSource

# 🛠️ Step 1: Define agent-specific knowledge (Laptop Specs)
product_specs = StringKnowledgeSource(
    content="""The XPS 13 laptop features:
    - 13.4-inch 4K display
    - Intel Core i7 processor
    - 16GB RAM
    - 512GB SSD storage
    - 12-hour battery life""",
    metadata={"category": "product_specs"}  # Metadata for categorization
)

# 🏆 Step 2: Create a Technical Support Agent
support_agent = Agent(
    role="Technical Support Specialist",
    goal="Provide accurate product information and support.",
    backstory="You are an expert on our laptop products and specifications.",
    knowledge_sources=[product_specs]  # Assign agent-specific knowledge
)

# 🎯 Step 3: Define a task for the agent
support_task = Task(
    description="Answer this customer question: {question}",
    agent=support_agent  # Assigning task to the support agent
)

# 🤖 Step 4: Create and run the crew
crew = Crew(
    agents=[support_agent],  # Add the support agent to the crew
    tasks=[support_task]  # Assign tasks that require product knowledge
)

# 🏁 Step 5: Ask a question about the laptop's specifications
result = crew.kickoff(
    inputs={"question": "What is the storage capacity of the XPS 13?"}
)

# Print the result
print(result)
```

---

# 🔍 **4. Code Breakdown & Explanation**
Let's break down each section of the code to understand its purpose:

### **🛠️ Step 1: Defining Agent-Specific Knowledge**
```python
product_specs = StringKnowledgeSource(
    content="""The XPS 13 laptop features:
    - 13.4-inch 4K display
    - Intel Core i7 processor
    - 16GB RAM
    - 512GB SSD storage
    - 12-hour battery life""",
    metadata={"category": "product_specs"}
)
```
✔️ **What This Does:**  
- Creates a **knowledge source** containing **laptop specifications**.  
- Uses **metadata** to categorize this knowledge as "product_specs."  
- This knowledge is specific to the **Technical Support Agent**.

---

### **🏆 Step 2: Creating a Technical Support Agent**
```python
support_agent = Agent(
    role="Technical Support Specialist",
    goal="Provide accurate product information and support.",
    backstory="You are an expert on our laptop products and specifications.",
    knowledge_sources=[product_specs]  # Assign agent-specific knowledge
)
```
✔️ **What This Does:**  
- Defines an **AI agent** with the role of a **Technical Support Specialist**.  
- The agent's **goal** is to provide **accurate product details**.  
- Assigns the **product_specs** knowledge source to this agent.

---

### **🎯 Step 3: Defining a Task**
```python
support_task = Task(
    description="Answer this customer question: {question}",
    agent=support_agent
)
```
✔️ **What This Does:**  
- Creates a **task** where the agent answers customer queries.  
- The **{question}** placeholder allows dynamic input.  
- This task is **assigned to the support agent**.

---

### **🤖 Step 4: Creating the Crew**
```python
crew = Crew(
    agents=[support_agent],  # Add the support agent to the crew
    tasks=[support_task]  # Assign tasks that require product knowledge
)
```
✔️ **What This Does:**  
- Defines a **Crew**, which is a team of AI agents.  
- The **Support Agent** is added to the crew.  
- The crew is assigned **product-related tasks**.

---

### **🏁 Step 5: Running the Crew with a Query**
```python
result = crew.kickoff(
    inputs={"question": "What is the storage capacity of the XPS 13?"}
)

# Print the result
print(result)
```
✔️ **What This Does:**  
- Calls the `kickoff()` method to **execute the query**.  
- The agent **retrieves information from its knowledge source**.  
- The answer (e.g., **"512GB SSD"**) is returned.  

---

# 🎯 **5. Benefits of Agent-Specific Knowledge**
| ✅ Benefit | 🔍 Explanation |
|------------|--------------|
| **Specialized Information** | Each agent gets **only relevant** knowledge. |
| **Better Accuracy** | Prevents agents from using unnecessary or incorrect information. |
| **Improved Efficiency** | Reduces knowledge processing time. |
| **Scalability** | Easily add more agents with specific knowledge. |
| **Separation of Concerns** | Organizes information by agent roles. |

---

# 📌 **6. Advanced Use Case: Combining Agent & Crew-Level Knowledge**
While each agent can have **its own knowledge**, sometimes **crew-wide knowledge** is needed. You can **combine both** by assigning:  
✅ **Common knowledge at the crew level** (e.g., company policies).  
✅ **Specialized knowledge at the agent level** (e.g., product details for support agents).

🔹 **Example:**  
A **customer service crew** could have:  
- **Crew-Level Knowledge:** General company policies.  
- **Agent-Specific Knowledge:**  
  - 📦 **Support Agent:** Product details.  
  - 💰 **Billing Agent:** Payment & refund policies.  
  - 🚚 **Shipping Agent:** Delivery times & tracking.  

---

# 🎉 **Conclusion**
Agent-specific knowledge in **CrewAI** allows **agents to specialize**, leading to **more accurate responses and efficient information retrieval**.  

🚀 **Key Takeaways:**  
- **Each agent can have exclusive knowledge** relevant to its role.  
- **Prevents confusion** by restricting knowledge to the right agents.  
- **Improves efficiency** in AI-driven applications.  
- **Can be combined** with crew-level knowledge for a layered approach.  

By applying this concept, you can build **highly efficient AI-powered teams** for **customer support, technical help, sales automation, and more!** 🎯

# 5. Custom Knowledge Sources in CrewAI

Here’s a detailed, beginner-friendly explanation of **Custom Knowledge Sources in CrewAI** with real-world examples, a structured breakdown, and well-commented code to help you understand everything step by step.  

---

# 🚀 **Understanding Custom Knowledge Sources in CrewAI**
CrewAI allows us to create **custom knowledge sources** by extending the `BaseKnowledgeSource` class. This means we can fetch data from any external API, database, or document and use it to make our AI agents more intelligent and context-aware.  

---

## 🎯 **Why Use Custom Knowledge Sources?**
- 📡 Fetch **real-time data** from APIs (e.g., space news, stock prices, weather updates).  
- 🎓 Train AI agents with **specific knowledge** (e.g., medical guidelines, legal documents).  
- 🏗️ Allow **domain-specific AI agents** to answer questions based on dynamic, up-to-date information.  

### **🌍 Real-World Example**
Imagine you're building an **AI chatbot for a space news website**. Instead of using outdated information, the chatbot should fetch **real-time space news articles** and answer user queries like:  
✅ *"What are the latest updates on NASA's Mars mission?"*  
✅ *"What new space exploration technologies were announced this week?"*  

To achieve this, we create a **custom knowledge source** that pulls live data from the **Spaceflight News API** and feeds it into a CrewAI agent.  

---

# 🛠 **Code Walkthrough: Creating a Custom Knowledge Source**
Here’s a **fully explained** implementation of a space news knowledge source:  

### **📌 Step 1: Import Required Libraries**
```python
from crewai import Agent, Task, Crew, Process, LLM
from crewai.knowledge.source.base_knowledge_source import BaseKnowledgeSource
import requests  # For making API calls
from datetime import datetime  # To work with dates
from typing import Dict, Any  # For type hinting
from pydantic import BaseModel, Field  # For data validation
```
✅ `requests` → Used to fetch live news from an API.  
✅ `datetime` → Helps manage article publishing dates.  
✅ `BaseKnowledgeSource` → Allows us to define a **custom knowledge source**.  

---

### **📌 Step 2: Create a Custom Knowledge Source Class**
```python
class SpaceNewsKnowledgeSource(BaseKnowledgeSource):
    """Knowledge source that fetches data from Space News API."""

    api_endpoint: str = Field(description="API endpoint URL")
    limit: int = Field(default=10, description="Number of articles to fetch")

    def load_content(self) -> Dict[Any, str]:
        """Fetch and format space news articles."""
        try:
            response = requests.get(f"{self.api_endpoint}?limit={self.limit}")
            response.raise_for_status()  # Check if the API call was successful

            data = response.json()  # Convert response to JSON format
            articles = data.get('results', [])  # Extract articles list

            formatted_data = self._format_articles(articles)  # Format articles into readable text
            return {self.api_endpoint: formatted_data}
        except Exception as e:
            raise ValueError(f"Failed to fetch space news: {str(e)}")

    def _format_articles(self, articles: list) -> str:
        """Format articles into readable text."""
        formatted = "🚀 Space News Articles:\n\n"
        for article in articles:
            formatted += f"""
                📰 Title: {article['title']}
                📅 Published: {article['published_at']}
                📝 Summary: {article['summary']}
                🌍 News Site: {article['news_site']}
                🔗 URL: {article['url']}
                -------------------"""
        return formatted

    def add(self) -> None:
        """Process and store the articles."""
        content = self.load_content()  # Fetch latest articles
        for _, text in content.items():
            chunks = self._chunk_text(text)  # Break large text into small chunks
            self.chunks.extend(chunks)

        self._save_documents()  # Save processed articles
```
✅ **`load_content()`** → Fetches news articles from the API.  
✅ **`_format_articles()`** → Converts articles into a clean, readable format.  
✅ **`add()`** → Processes and stores the articles for AI use.  

---

### **📌 Step 3: Instantiate and Use the Custom Knowledge Source**
```python
# Create knowledge source to fetch the latest space news
recent_news = SpaceNewsKnowledgeSource(
    api_endpoint="https://api.spaceflightnewsapi.net/v4/articles",
    limit=10  # Fetch up to 10 articles
)
```
✅ Here, we create an **instance** of `SpaceNewsKnowledgeSource` that will fetch **10 recent space news articles**.  

---

### **📌 Step 4: Define the AI Agent**
```python
space_analyst = Agent(
    role="🛰️ Space News Analyst",
    goal="Answer questions about space news accurately and comprehensively",
    backstory="""You are a space industry analyst with expertise in space exploration,
    satellite technology, and space industry trends. You excel at answering questions
    about space news and providing detailed, accurate information.""",
    knowledge_sources=[recent_news],  # Attach the custom knowledge source
    llm=LLM(model="gpt-4", temperature=0.0)  # Use GPT-4 for responses
)
```
✅ The agent is specialized in space news.  
✅ It **uses** the `recent_news` knowledge source to fetch live data.  
✅ **`temperature=0.0`** → Ensures factual, non-random responses.  

---

### **📌 Step 5: Define the Task**
```python
analysis_task = Task(
    description="Answer this question about space news: {user_question}",
    expected_output="A detailed answer based on the recent space news articles",
    agent=space_analyst  # Assign task to the space analyst agent
)
```
✅ This task takes a **user question** (e.g., “What are the latest space discoveries?”) and generates a response using **real-time space news**.  

---

### **📌 Step 6: Create and Run the Crew**
```python
crew = Crew(
    agents=[space_analyst],  # Assign the space analyst agent
    tasks=[analysis_task],  # Assign the task
    verbose=True,  # Show detailed logs
    process=Process.sequential  # Execute tasks one by one
)

# Example usage
result = crew.kickoff(
    inputs={"user_question": "What are the latest developments in space exploration?"}
)
```
✅ **`Crew`** manages the workflow between agents and tasks.  
✅ **`kickoff()`** starts the process and **fetches** space news articles to answer the question.  

---

# 🎯 **Key Takeaways**
### ✅ **What We Achieved**
- **Created a custom knowledge source** (`SpaceNewsKnowledgeSource`) that fetches **real-time space news**.  
- **Integrated it into a CrewAI agent** that specializes in answering **space-related questions**.  
- **Used GPT-4 to analyze news articles** and provide **detailed, accurate answers**.  

---

# 🏗️ **How Can You Use This in the Real World?**
🔹 **📈 Stock Market Assistant** → Fetches real-time stock prices and analyzes trends.  
🔹 **🦠 Medical AI** → Retrieves the latest research on diseases and treatments.  
🔹 **📅 Event Tracker** → Monitors tech events, conferences, and product launches.  
🔹 **🌦️ Weather Bot** → Provides up-to-date weather reports.  

---

# 🔥 **Final Thoughts**
This approach **supercharges AI agents** by giving them **real-time knowledge** rather than relying on outdated training data. Whether you're building a **news bot**, a **financial advisor**, or a **legal assistant**, **custom knowledge sources** can take your AI applications to the next level! 🚀