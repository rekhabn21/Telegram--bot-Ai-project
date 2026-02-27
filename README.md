**Project Overview**

This project features an AI-driven Telegram bot built with n8n, designed to automate critical marketing tasks such as email management, calendar scheduling, contact lookup, and content generation. Tailored for a marketing startup, it leverages Gemini (a large language model) for intelligent decision-making and workflow automation, showcasing my expertise as an AI Engineer with a focus on scalable, production-ready solutions.

**Key Features & Value**

**Email Automation:**
Send, reply, label, and manage emails via Telegram—streamlining communication workflows.
Calendar Management: Create, update, and delete Google Calendar events, ideal for scheduling campaigns or meetings.
Contact Lookup: Retrieve or update contact details using AI-generated SQL queries, enhancing customer relationship management.
Content Generation: Generate blog posts from web-scraped data, supporting content marketing efforts.
Voice & Text Support: Processes both voice (transcribed) and text inputs for flexible user interaction.

**Environment & Prerequisites**
The project uses the following tools:

n8n (Docker-based): Workflow automation platform.
ngrok: Exposes the local n8n instance for Telegram integration.
PostgreSQL 17 (localhost): Manages user authentication and contact data.

**Getting Started**
ngrok: Expose n8n with ngrok http 5678 to generate a public URL which will be used as a webhook for telegram.

n8n: Run via Docker with:

docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n -e WEBHOOK_URL=&lt;https://{random-string}.ngrok-free.app&gt; docker.n8n.io/n8nio/n8n
PostgreSQL 17: Install locally and setup the DB.
