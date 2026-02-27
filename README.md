# Telegram Bot with n8n Workflow for AI-Driven Automation

**Author:** Rekha B N
**Contact:** rekha.nag@outlook.com

[Portfolio](https://pushpak-portfolio.web.app) | [LinkedIn](http://linkedin.com/in/pushpakruhil/) | [GitHub](http://github.com/ruhil-ds)

# Table of Contents

- [Project Overview](#TelegramBotwithn8nWorkflowforAI-DrivenA)
  - [Key Features & Value](#TelegramBotwithn8nWorkflowforAI-DrivenA)
- [Video Demonstration](#TelegramBotwithn8nWorkflowforAI-DrivenA)
- [Environment & Prerequisites](#TelegramBotwithn8nWorkflowforAI-DrivenA)
  - [Getting Started](#TelegramBotwithn8nWorkflowforAI-DrivenA)
- [Parent Workflow](#TelegramBotwithn8nWorkflowforAI-DrivenA)
  - [Workflow Steps](#TelegramBotwithn8nWorkflowforAI-DrivenA)
- [Sub-Workflows](#TelegramBotwithn8nWorkflowforAI-DrivenA)
  - [Email Agent Workflow](#TelegramBotwithn8nWorkflowforAI-DrivenA)
  - [Calendar Agent Workflow](#TelegramBotwithn8nWorkflowforAI-DrivenA)
  - [Contact Agent Workflow](#TelegramBotwithn8nWorkflowforAI-DrivenA)
  - [Content Creator Agent Workflow](#TelegramBotwithn8nWorkflowforAI-DrivenA)
- [Database Schema](#TelegramBotwithn8nWorkflowforAI-DrivenA)
  - [contacts Table Schema](#TelegramBotwithn8nWorkflowforAI-DrivenA)
- [Security Considerations](#TelegramBotwithn8nWorkflowforAI-DrivenA)
- [Conclusion](#TelegramBotwithn8nWorkflowforAI-DrivenA)

# Project Overview

This project features an AI-driven Telegram bot built with **n8n**, designed to automate critical marketing tasks such as email management, calendar scheduling, contact lookup, and content generation. Tailored for a marketing startup, it leverages **Gemini** (a large language model) for intelligent decision-making and workflow automation, showcasing my expertise as an AI Engineer with a focus on scalable, production-ready solutions.

## Key Features & Value

- **Email Automation:** Send, reply, label, and manage emails via Telegram—streamlining communication workflows.
- **Calendar Management:** Create, update, and delete Google Calendar events, ideal for scheduling campaigns or meetings.
- **Contact Lookup:** Retrieve or update contact details using AI-generated SQL queries, enhancing customer relationship management.
- **Content Generation:** Generate blog posts from web-scraped data, supporting content marketing efforts.
- **Voice & Text Support:** Processes both voice (transcribed) and text inputs for flexible user interaction.


# Environment & Prerequisites

The project uses the following tools:

- **n8n (Docker-based):** Workflow automation platform.
- **ngrok:** Exposes the local n8n instance for Telegram integration.
- **PostgreSQL 17 (localhost):** Manages user authentication and contact data.

## Getting Started

1. **ngrok:** Expose n8n with `ngrok http 5678` to generate a public URL which will be used as a webhook for telegram.
2. **n8n:** Run via Docker with:

    `docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n -e WEBHOOK_URL=&lt;https://{random-string}.ngrok-free.app&gt; docker.n8n.io/n8nio/n8n`

3. **PostgreSQL 17:** Install locally and setup the DB.

# Parent Workflow

The parent workflow serves as the entry point, triggered by Telegram messages. It authenticates users, processes inputs, and routes requests to sub-workflows using Gemini.

## Workflow Steps

1. **Telegram Trigger:** Captures text or voice messages from Telegram.
2. **Username Check:** Queries the members table in PostgreSQL to verify the user.
    - Registered users proceed; unregistered users are logged in not_registered and receive a default reply.
3. **Input Processing:**
    - Voice messages are transcribed into text.
    - Text inputs are passed directly to the LLM.
4. **LLM Node (Gemini):** Analyzes the query and routes it to the appropriate sub-workflow (Email, Calendar, Contact, or Content).


# Sub-Workflows

Each sub-workflow is modular, handling a specific task independently for scalability and maintainability.

## Email Agent Workflow

**Purpose:** Automates Gmail tasks.

**Capabilities:**

- Send, reply, draft, label, retrieve, and mark emails as unread.

**Nodes Used:**

- **Gemini:** Interprets user intent and selects the email action.
- **Gmail API Nodes:** Execute the email operations.
## Calendar Agent Workflow

**Purpose:** Manages Google Calendar events.

**Capabilities:**

- Create, update, delete, and retrieve events (single or multi-attendee).

**Nodes Used:**

- **Gemini:** Decides the calendar action based on the query.
- **Google Calendar API Nodes:** Perform the calendar operations.

## Contact Agent Workflow

**Purpose:** Manages contact data in the contacts table.

**Capabilities:**

- Retrieve contact details (e.g., email ID from name).
- Add new contacts.
- Update existing contacts.

**Nodes Used:**

- **Gemini:** Generates valid SQL queries based on user requests and the schema.
- **PostgreSQL Node:** Executes the queries.

**Tool Calling (System Message Summary):**  
Gemini generates SELECT, INSERT, or UPDATE SQL queries (no DELETE) for the contacts table, adhering to constraints (e.g., allowed departments: 'IT', 'Marketing').



## Content Creator Agent Workflow

**Purpose:** Generates blog posts using web data.

**Capabilities:**

- Searches the web via Tavily and generates content based on the results.

**Nodes Used:**

- **Gemini:** Interprets the topic and drives the content generation process.
- **Tavily Node:** Provides web-scraped context.
- **Gemini (again):** Crafts the blog post.



# Database Schema

The project uses three PostgreSQL tables:

- members: Stores registered users for authentication.
- not_registered: Logs unregistered users.
- contacts: Holds contact data for the Contact Agent.

### contacts Table Schema

| **Column Name** | **Data Type** | **Max Length** | **Nullable** | **Constraint** |
| --- | --- | --- | --- | --- |
| custid | integer | —   | No  | Primary Key, auto-increments |
| firstname | varchar | 255 | Yes | —   |
| lastname | varchar | 255 | Yes | —   |
| emailid | varchar | 255 | No  | —   |
| mobilenum | varchar | 15  | Yes | —   |
| department | varchar | 255 | Yes | —   |




# Security Considerations

- **Username Authentication:** The parent workflow checks the Telegram username against the members table before processing requests. This prevents unauthorized access to sensitive operations like sending emails from your email ID. In a production setup for an organization, this restricts access to specific users, safeguarding credential-sensitive steps.
- **SQL Safety:** The Contact Agent only generates SELECT, INSERT, and UPDATE queries, avoiding destructive actions like DELETE.

# Conclusion

This Telegram bot demonstrates a robust, AI-driven automation system tailored for marketing tasks, built with n8n, Gemini, and PostgreSQL. Its modular design, authentication, and practical applications (e.g., email campaigns, event scheduling, content creation) make it a valuable asset for any organization.

The project reflects my AI engineering expertise — from LLM integration and workflow automation to secure, scalable system design.
