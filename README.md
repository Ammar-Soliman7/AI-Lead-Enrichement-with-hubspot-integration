# AI Company Enrichment & Lead Qualification Workflow

An AI-powered lead qualification workflow built with **n8n**, **Apollo**, **Gemini**, **Google Sheets**, and **HubSpot**.

The workflow accepts a company domain through a form, enriches the company using Apollo, cleans the returned data, analyzes the company using Gemini, assigns a lead score, stores the result in Google Sheets, and sends qualified companies to HubSpot.

## Workflow

![Workflow](AI Lead Enrichement workflow.png)

## What It Does

The workflow follows this process:

```text
Company Form Submission
        ↓
Apollo Company Enrichment API
        ↓
API Error Handling
        ↓
Check Company Exists
        ↓
Clean Apollo Data
        ↓
Gemini AI Analysis
        ↓
Parse Structured JSON
        ↓
Lead Qualification
        ↓
Google Sheets / HubSpot
```

## Features

* Company enrichment using the Apollo API
* Dynamic company lookup using a submitted domain
* AI-powered company analysis using Gemini
* Lead scoring
* Identification of likely business needs
* Suggested B2B sales angle
* Structured JSON output
* Google Sheets integration
* HubSpot CRM integration
* Invalid-domain handling
* Apollo API error handling
* Company-not-found handling
* Conditional workflow routing

## Example Input

A user submits:

```text
Company Name: HubSpot
Website: hubspot.com
```

Apollo retrieves real company information such as:

```text
Company Name
Industry
Employee Count
Revenue
Location
LinkedIn
Company Description
Keywords
```

The data is cleaned before being passed to the AI model.

## AI Analysis

Gemini analyzes the enriched company data and returns structured output such as:

```json
{
  "company_name": "HubSpot",
  "industry": "Information Technology & Services",
  "company_size": "Large Enterprise",
  "lead_score": 95,
  "likely_needs": "Advanced AI infrastructure and sales automation.",
  "sales_angle": "Position the solution as a strategic integration that improves automation and platform capabilities."
}
```

## Error Handling

The workflow includes separate paths for API and data failures.

### Invalid API Request

If Apollo cannot process the submitted domain:

```json
{
  "status": "apollo_api_error",
  "message": "Apollo could not process the submitted company domain."
}
```

### Company Not Found

If the API request succeeds but no organization is returned:

```json
{
  "status": "company_not_found",
  "message": "No company was found for the submitted domain."
}
```

This prevents failed API calls from stopping the entire workflow unexpectedly.

## Technologies Used

* **n8n** — Workflow orchestration
* **Apollo API** — Company enrichment
* **Google Gemini** — AI analysis and lead qualification
* **JavaScript** — API response cleaning and JSON parsing
* **Google Sheets** — Lead storage
* **HubSpot CRM** — Qualified company management
* **Docker** — Local n8n deployment

## Key Concepts Demonstrated

This project demonstrates several practical AI automation concepts:

* REST API integration
* API authentication
* Query parameters and headers
* JSON processing
* JavaScript data transformation
* LLM integration
* Structured AI output
* Conditional routing
* Error handling
* CRM integration
* Business workflow automation

## Running the Workflow

### 1. Run n8n

The workflow was developed using a locally hosted n8n instance running with Docker.

Create the volume:

```bash
docker volume create n8n_data
```

Start n8n:

```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```

Then open:

```text
http://localhost:5678
```

### 2. Import the Workflow

Download the workflow JSON from this repository and import it into n8n.

### 3. Configure Credentials

You will need to configure your own credentials for:

* Apollo API
* Google Gemini
* Google Sheets
* HubSpot

API keys and credentials are **not included** in this repository.

### 4. Test the Workflow

Example:

```text
Company Name: Salesforce
Website: salesforce.com
```

The workflow will:

1. Retrieve company data from Apollo.
2. Clean the API response.
3. Analyze the company using Gemini.
4. Generate a lead score and sales insights.
5. Store the results.
6. Send qualified company data to HubSpot.

## Repository Structure

```text
.
├── README.md
├── ai-company-enrichment-workflow.json
└── workflow.png
```

## Security

No API keys, OAuth credentials, service keys, or other secrets are included in this repository.

When importing the workflow, configure your own credentials inside n8n.

## Future Improvements

Possible future improvements include:

* CRM duplicate detection
* Automatic company updates
* Contact enrichment
* Personalized outbound email generation
* Human approval before CRM insertion
* Lead routing based on score
* Logging and monitoring
* Retry logic and rate-limit handling

## Purpose

This project was built as a practical AI automation project focused on combining:

**AI + APIs + business logic + CRM automation**

rather than using an LLM as a standalone chatbot.

It demonstrates how AI can be integrated into a real business workflow for automated company research and lead qualification.
