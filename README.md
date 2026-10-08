# SmartClaims --- AI Insurance Claims Agent

> An AI-powered insurance claims assistant built with Microsoft Foundry
> Agent Service, Azure OpenAI, Python, and FastAPI.

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-Web%20API-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![Microsoft
Azure](https://img.shields.io/badge/Microsoft%20Azure-Cloud-0078D4?logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/)
[![Microsoft
Foundry](https://img.shields.io/badge/Microsoft%20Foundry-AI%20Agents-0078D4)](https://ai.azure.com/)

## Overview

**SmartClaims** is a multi-tool AI agent designed to support insurance
claim-processing workflows. It combines policy-document retrieval,
claims-data analysis, custom business logic, and real-time web search
through a FastAPI web application.

The project demonstrates how an AI agent can assist insurance teams
with:

- Answering questions about insurance policies
- Retrieving relevant information from policy documents using **File
  Search / RAG**
- Analyzing claims datasets with **Code Interpreter**
- Looking up claim status through custom business logic
- Calculating or evaluating fraud-risk indicators
- Retrieving current regulatory or insurance-related information
  through web search
- Providing a browser-based interface through **FastAPI**

> **Important:** SmartClaims is an AI-assisted
> demonstration/application. Its outputs should be reviewed by qualified
> insurance professionals before being used for real claims decisions.

## Video Demo

<video src="diagram/Demo-compressed.mp4" width="100%" controls></video>

## Key Capabilities

---

Capability Purpose

---

**Microsoft Foundry Agent Service** Orchestrates the AI agent and its
tools

**Azure OpenAI** Provides the language model
capability

**File Search / RAG** Retrieves relevant content from
insurance policy documents

**Code Interpreter** Performs calculations and analyzes
claims datasets

**Custom Function Tools** Executes application-specific
operations such as claim-status
lookup and fraud-risk scoring

**Web Search** Retrieves up-to-date information
relevant to insurance regulations
and related topics

**FastAPI** Provides the application backend
and web interface

**Azure Web App** Hosts the application in Azure

---

## High-Level Architecture

![SmartClaims Azure Insurance Architecture](diagram/SmartClaims%20Azure%20Insurance%20Architecture.png)

## Technology Stack

- **Python 3.10+**
- **Microsoft Foundry Agent Service**
- **Azure OpenAI**
- **GPT-4o-mini** model deployment
- **FastAPI**
- **Uvicorn**
- **Azure CLI**
- **Azure Web App / App Service**
- Retrieval-Augmented Generation (RAG)
- Python-based data analysis

## Prerequisites

Before running the project, make sure you have:

1.  An **Azure account** with access to the required Azure AI resources.
2.  **Python 3.10 or later**.
3.  **Git**.
4.  **Visual Studio Code** or another Python-capable IDE.
5.  **Azure CLI 2.50+**.
6.  A Microsoft Foundry project with the required model deployment and
    agent configuration.

Check your local versions:

```bash
python --version
az --version
git --version
```

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/k21academyuk/smart-claims-agent-project.git
cd smart-claims-agent-project
```

### 2. Create a virtual environment

Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

macOS / Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

The project uses `requirements.txt` for Python dependencies:

```bash
pip install --pre -r requirements.txt
```

### 4. Configure environment variables

Create a local `.env` file if the application code expects
environment-based configuration.

The deployment configuration documented for the project uses the
following values:

```env
PROJECT_ENDPOINT=<your-foundry-project-endpoint>
MODEL_DEPLOYMENT_NAME=gpt-4o-mini
```

Do **not** commit credentials, secrets, tokens, or private Azure
configuration values to Git.

If your local implementation uses additional environment variables, add
them according to the application's configuration code.

### 5. Authenticate with Azure

Sign in with Azure CLI:

```bash
az login
```

Verify the active subscription:

```bash
az account show
```

If you have multiple subscriptions, select the required one:

```bash
az account set --subscription "<subscription-id>"
```

## Run the Application Locally

From the repository root, start the FastAPI application with Uvicorn:

```bash
uvicorn app.main:app --reload --port 8000
```

Then open:

```text
http://localhost:8000
```

The documented application uses `app.main:app` as the FastAPI entry
point and `app/templates/index.html` for the frontend interface.

## Example Use Cases

### Policy Questions

Ask questions about the insurance policy documents available to the
agent.

```text
What coverage is available for this type of claim?
```

The File Search / RAG capability can retrieve relevant policy
information before generating the response.

### Claims Analytics

Provide or reference claims data and ask the agent to analyze it.

```text
Analyze the claims data and identify unusual patterns.
```

The Code Interpreter capability can be used for calculations, dataset
analysis, and identifying potential indicators that warrant further
review.

### Claim Status

The custom function layer can support application-specific operations
such as:

```text
What is the current status of claim CLM-1001?
```

### Fraud-Risk Analysis

The project demonstrates custom business logic for fraud-risk scoring or
related indicators.

```text
Evaluate the fraud risk for this claim and explain the factors that contributed to the score.
```

> Fraud indicators are decision-support signals, not proof of fraud.
> Final decisions should follow the organization's approved review and
> compliance processes.

### Regulatory Information

The web-search capability can retrieve current information related to
insurance regulations and updates.

```text
What recent regulatory information could affect this claims workflow?
```

## Project Structure

The following paths are explicitly referenced by the project
documentation:

```text
smart-claims-agent-project/
├── app/
│   ├── main.py
│   └── templates/
│       └── index.html
├── requirements.txt
└── .env                  # local configuration; do not commit secrets
```

> The repository may contain additional files and directories not shown
> above. Treat the actual repository tree as the source of truth when
> extending this section.

## Azure Deployment

The project documentation describes deployment to an Azure Web App.

### 1. Create an App Service Plan

The documented deployment uses a Linux App Service Plan:

```bash
az appservice plan create \
  --name smartclaims-plan \
  --resource-group <resource-group-name> \
  --is-linux \
  --sku B1
```

### 2. Configure Web App settings

The documented application settings include:

```bash
az webapp config appsettings set \
  --name smartclaims-webapp \
  --resource-group <resource-group-name> \
  --settings \
  PROJECT_ENDPOINT="<your-foundry-project-endpoint>" \
  MODEL_DEPLOYMENT_NAME="gpt-4o-mini" \
  SCM_DO_BUILD_DURING_DEPLOYMENT="true" \
  WEBSITES_PORT="8000"
```

### 3. Deploy the application

```bash
az webapp up \
  --name smartclaims-webapp \
  --resource-group <resource-group-name>
```

Use your own Azure resource names rather than copying example names from
the documentation.

## Troubleshooting

### Application does not start

Confirm that the virtual environment is active and dependencies are
installed:

```bash
python --version
pip install --pre -r requirements.txt
```

Then retry:

```bash
uvicorn app.main:app --reload --port 8000
```

### Azure connectivity / DNS errors

If Azure endpoints cannot be resolved, verify:

- Your network connection
- Azure CLI authentication
- The Azure resource and project endpoint
- DNS resolution on the local machine
- That the Azure resources have finished provisioning

The project guide specifically documents a `ServiceRequestError` /
DNS-resolution scenario involving an Azure AI service endpoint.

### Environment configuration errors

Verify that the application has access to the expected configuration
values:

```env
PROJECT_ENDPOINT=<your-foundry-project-endpoint>
MODEL_DEPLOYMENT_NAME=gpt-4o-mini
```

Do not paste secrets into source code or commit them to Git.

## Development Notes

When modifying the project:

- Keep Azure configuration outside source control.
- Use environment variables for deployment-specific settings.
- Validate agent tool behavior independently before integrating it
  into the web layer.
- Test policy retrieval with representative documents.
- Treat fraud-risk outputs as review signals rather than definitive
  findings.
- Review Azure resource permissions and managed identities before
  production deployment.
- Monitor model and tool behavior when changing prompts, tools,
  datasets, or model deployments.

## What This Project Demonstrates

This project brings together several important AI-engineering concepts
in a single application:

1.  Creating an AI agent with Microsoft Foundry Agent Service
2.  Deploying and using an Azure OpenAI model
3.  Implementing document retrieval with RAG
4.  Using an AI agent for claims-data analysis
5.  Extending an agent with custom business functions
6.  Adding web-search capabilities
7.  Exposing the agent through a FastAPI application
8.  Running the application locally
9.  Deploying the application to Azure Web App

## Roadmap

Potential areas for future enhancement include:

- [ ] Add automated tests for agent tools and API endpoints
- [ ] Add structured claim schemas and validation
- [ ] Add authentication and role-based access control
- [ ] Add persistent claim-history storage
- [ ] Add richer observability and evaluation workflows
- [ ] Add CI/CD with GitHub Actions
- [ ] Add automated evaluation datasets for policy Q&A and fraud-risk
      scenarios
- [ ] Improve production-grade security and secret management

## Disclaimer

This project is intended for educational, demonstration, and development
purposes. Insurance claims, policy interpretation, fraud assessment, and
regulatory decisions can have significant financial and legal
consequences. AI-generated outputs should be validated against
authoritative policy documents, organizational procedures, and
applicable regulations before being used in production decision-making.

## Contributing

Contributions, improvements, bug reports, and documentation updates are
welcome.

Before opening a pull request:

1.  Test your changes locally.
2.  Avoid committing secrets or `.env` files.
3.  Update the documentation when behavior or setup requirements change.
4.  Keep changes focused and clearly described.

---

**SmartClaims** --- AI-assisted insurance claims analysis with Microsoft
Foundry and Azure.
