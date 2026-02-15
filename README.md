I just finished building a fully automated Threat Intelligence & Incident Response pipeline (SOAR-lite) from scratch! 

I wanted a project that goes beyond theory and solves a real-world Security Operations Center (SOC) problem: alert fatigue and manual URL analysis.

Here is what the architecture does:
1️⃣ Ingestion: A webhook actively listens for suspicious URLs.
2️⃣ Enrichment: It automatically queries the VirusTotal API v3 to scan the domain across 70+ security vendors.
3️⃣ Parsing Logic: The system parses the complex JSON payload to extract the specific malicious hit count.
4️⃣ Automated Response: If the risk score is > 0, it formats the data and pushes a critical incident alert directly to a Discord webhook for immediate triage. Safe URLs are dropped silently to keep the channel clean.

Tech Stack: n8n (Automation), VirusTotal API (Threat Intel), REST APIs/JSON, Discord Webhooks.

It was a great challenge mapping the data structures and writing the conditional logic to make the system "think" on its own.
