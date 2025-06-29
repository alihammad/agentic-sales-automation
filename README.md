# Agentic Sales Automation

This project demonstrates advanced agentic AI design patterns for automating the process of generating, selecting, and sending cold sales emails using OpenAI models and the SendGrid email API. The code is organized as a Jupyter notebook, making it easy to experiment with and extend in VS Code.

---

## Project Overview

The notebook covers the following key concepts and functionalities:

### 1. **Agent Workflows**
- Multiple specialized agents (`sales_agent1`, `sales_agent2`, `sales_agent3`) are created, each with unique instructions and personalities for writing cold sales emails.
- Agents are instantiated using the `Agent` class and can be run individually or in parallel.

### 2. **Parallelism**
- The code uses `asyncio.gather` to run multiple agents in parallel, generating several email drafts at once for comparison or selection.

### 3. **Agent as Tool Pattern**
- Agents are converted into callable tools using the `.as_tool()` method. This allows other agents (like the Sales Manager) to invoke them as modular components.

### 4. **Function as Tool Pattern**
- Python functions (e.g., `send_email`, `send_html_email`) are decorated with `@function_tool`, registering them as tools that agents can use. This integrates external actions (like sending emails) into the agentic workflow.

### 5. **Planning/Manager Agent**
- The `Sales Manager` agent orchestrates the workflow: it uses the agent-tools to generate emails, selects the best one, and delegates the sending task to another agent or tool.

### 6. **Selection/Evaluation Agent**
- A dedicated agent (`sales_picker`) is used to evaluate and select the best email from multiple candidates, demonstrating agent-based judgment.

### 7. **Handoff Pattern**
- The Sales Manager agent can hand off tasks to another agent (`Email Manager`), which handles formatting and sending the email. This enables complex, multi-step workflows where agents collaborate and delegate responsibilities.

### 8. **Traceability**
- The `trace` context manager is used to track and visualize the workflow execution, which can be viewed on the OpenAI platform.

---

## SendGrid Integration

**Purpose:**  
SendGrid is used in this project to actually send the generated sales emails. By integrating SendGrid, the workflow moves beyond just generating email content and demonstrates real-world automation by delivering emails to recipients.

**How it works in this project:**  
- The `send_email` and `send_html_email` functions are decorated as tools and use the SendGrid API to send plain text or HTML emails.
- These functions are called by agents as part of the workflow, allowing for seamless automation from content generation to delivery.

**How to set up SendGrid:**
1. [Sign up for a SendGrid account](https://sendgrid.com/).
2. Create an API key in the SendGrid dashboard.
3. Add your API key to a `.env` file in your project root:
   ```
   SENDGRID_API_KEY=your_sendgrid_api_key_here
   ```
4. (Optional) Verify sender email addresses in your SendGrid account to avoid delivery issues.

---

## Setup Instructions

### 1. **Clone the Repository**
```sh
git clone <your-repo-url>
cd agentic-sales-automation
```

### 2. **Install Python Dependencies**
Make sure you have Python 3.8+ and pip installed.

```sh
pip install -r requirements.txt
```
*Typical requirements include:*
- openai
- sendgrid
- python-dotenv
- asyncio

### 3. **Set Up Environment Variables**
Create a `.env` file in the root directory and add your SendGrid API key:
```
SENDGRID_API_KEY=your_sendgrid_api_key_here
```

### 4. **Open in VS Code**
- Open the project folder in VS Code.
- Make sure the Python and Jupyter extensions are installed.

### 5. **Run the Notebook**
- Open `src/sales_automation.ipynb` in VS Code.
- Run cells step by step to see agentic workflows in action.

---

## How to Use

- **Generate Emails:** Run the cells to have different agents generate cold sales emails in parallel.
- **Select Best Email:** Use the selection agent to pick the most effective email.
- **Send Emails:** Use the function tools to send emails via SendGrid.
- **Orchestrate with Manager Agent:** Let the Sales Manager agent coordinate the entire process, including handoffs to the Email Manager for formatting and sending.

---

## Agentic AI Patterns Demonstrated

- **Agent as Tool:** Agents can be registered as tools and called by other agents.
- **Function as Tool:** Python functions are exposed as tools for agents to use.
- **Planning/Manager Agent:** An agent coordinates and manages the workflow, making decisions and delegating tasks.
- **Selection/Evaluation Agent:** Agents can be used to evaluate and select outputs from other agents.
- **Handoff Pattern:** Agents can delegate tasks to other agents, enabling complex, multi-step workflows.
- **Parallelism:** Multiple agents can work in parallel to generate diverse outputs.
- **Traceability:** Workflows are traced for debugging and visualization.

---

## Extending the Project

- Add more specialized agents for different sales styles.
- Integrate additional tools (e.g., CRM integration, analytics).
- Experiment with different agent orchestration strategies.

