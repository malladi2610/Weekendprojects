# Weekend Projects

> A collection of automation and AI-powered mini-projects built for learning, experimentation, and productivity enhancement.

---

## Table of Contents
- [Projects](#projects)
  - [n8n Gmail AI Agent](#n8n-gmail-ai-agent)
  - [WhatsApp Automation](#whatsapp-automation)
- [Technologies Used](#technologies-used)
- [Getting Started](#getting-started)
- [Contributing](#contributing)

---

## Projects

### [n8n Gmail AI Agent](./n8n_gmail_AI_agent)

An intelligent automation workflow that streamlines the job application process by extracting, analyzing, and organizing job postings from recruitment emails.

**Overview:**  
This n8n-powered agent monitors Gmail for job postings from LinkedIn, Glassdoor, and Indeed, uses AI to match opportunities against your CVs (95% relevance threshold), and automatically populates a Notion database with qualified leads.

**Key Features:**
- Automated email parsing for job postings from multiple platforms
- AI-powered job filtering based on profile categories
- Intelligent CV-to-job description matching
- Seamless Notion integration for job tracking and management
- Scheduled daily execution for consistent workflow
- Smart categorization and priority assignment

**Security:**  
Sensitive credentials and API keys are protected. See [SETUP.md](./n8n_gmail_AI_agent/SETUP.md) for configuration instructions.

**Tech Stack:** n8n, AI/LLM APIs, Gmail API, Notion API

---

### [WhatsApp Automation](./whatsapp%20automation)

A VBA-based automation solution for WhatsApp Web, enabling bulk messaging and workflow automation through a familiar Excel interface.

**Overview:**  
This project leverages Excel VBA and Selenium to automate WhatsApp Web interactions, making it easy to send messages, manage contacts, and streamline communication workflows.

**Key Features:**
- WhatsApp Web automation via Selenium WebDriver
- Excel VBA interface for intuitive control
- Automated messaging capabilities
- Bulk operations support

**Tech Stack:** Excel VBA, Selenium WebDriver

---

## Technologies Used

- **Automation:** n8n, Selenium WebDriver
- **AI/ML:** Large Language Models (LLMs), AI APIs
- **Platforms:** Gmail API, Notion API, WhatsApp Web
- **Languages:** VBA, JSON
- **Tools:** Excel, n8n Workflow Automation

---

## Getting Started

Each project contains its own README with detailed setup instructions. Navigate to the respective project folder to get started:

1. **[n8n Gmail AI Agent](./n8n_gmail_AI_agent/readme.md)** - Follow the setup guide for Gmail filters, n8n configuration, and Notion integration
2. **[WhatsApp Automation](./whatsapp%20automation/Readme.txt)** - Review the installation steps for Selenium and Excel setup

---

## Contributing

These projects are personal learning experiments. Feel free to fork, explore, and adapt them for your own use cases!

---

**Built during weekends for learning, automation, and fun.**

