# Loyin's Brand AI Assistant

An n8n AI customer-service and sales assistant for Loyin's, a Nigerian clothing brand.

## What it does

- Answers product and pricing questions
- Recommends T-shirts, joggers and caps
- Captures potential buyers in Google Sheets
- Supports business/bulk enquiries
- Handles meeting-date interpretation
- Creates Google Calendar meetings through the connected calendar tool
- Uses conversational memory
- Uses Groq and OpenRouter chat models with fallback support
- Includes guardrails for payments, delivery, inventory, returns and human escalation

## Products configured

- SMT plain T-shirt — ₦4,500
- Joggers — ₦10,000
- Caps — ₦2,000
- 3 T-shirts + 1 cap — ₦22,500
- 6 T-shirts + 2 caps — ₦45,000

## Import notes

The workflow JSON has been sanitized before publication. n8n credential objects, credential IDs, webhook IDs, instance metadata and pin data were removed.

After importing into n8n, reconnect the required:
- Groq credential
- OpenRouter credential
- Google Sheets credential
- Google Calendar credential

The workflow references the configured Google Sheet and calendar from the original workflow. Verify those resources before production use.

## Status

Published as an evolving automation workflow in the Automation-Labs repository. Improvements and additional business tools can be added later.
