Automated Threat Intelligence & Incident Response Pipeline (SOAR)

📌 Project Overview
This project is an automated Security Orchestration, Automation, and Response (SOAR) pipeline. It acts as a lightweight SOC analyst, designed to automatically ingest suspicious URLs, query global threat intelligence databases, mathematically evaluate risk, and route high-fidelity alerts to incident response channels. 

This architecture serves as a foundational micro-service for a broader Security Information and Event Management (SIEM) strategy, reducing alert fatigue and automating initial triage.

Architecture & Tech Stack
* **Orchestration Engine:** n8n (Self-hosted)
* **Threat Intelligence API:** VirusTotal API v3
* **Alerting & Notification:** Discord Webhooks & Automated SMTP (Gmail)
* **Logic/Parsing:** JSON parsing, conditional risk scoring

 How It Works
1.  **Ingestion:** A webhook acts as the listener, accepting `POST`/`GET` requests containing a target URL.
2.  **Enrichment:** The workflow automatically queries the VirusTotal API, passing the target URL to check against 70+ security vendors.
3.  **Parsing & Decision Engine:** The pipeline parses the complex JSON response, extracting the specific `malicious` hit count.
4.  **Automated Response:** * *Clean (Score = 0):* The workflow terminates silently, keeping analyst dashboards clean.
    * *Threat (Score > 0):* The system instantly formats the threat data and pushes a critical alert to a dedicated Discord incident channel, alongside a formal email log.

## 🔮 Future Expansions
* **AI Integration:** Integrating an AI/ML model to evaluate the context and syntax of the URL before triggering the API, acting as a predictive filter.
* **Custom Dashboarding:** Connecting the n8n backend webhooks to a custom Django frontend application to create a centralized interface for SOC analysts.
* **SIEM Integration:** Pushing the JSON logs directly into a robust SIEM platform like Wazuh for long-term threat hunting.

## 🛠️ How to Deploy Locally
1. Install [n8n](https://n8n.io/) (`npm install n8n -g`).
2. Import the `threat_intel_pipeline.json` file into your n8n workspace.
3. Add your VirusTotal API key to the HTTP Request node headers.
4. Update the Discord Webhook URL and Gmail credentials in the alerting nodes.
5. Activate the workflow and send a test payload to the webhook URL!
