# NaijaMart AI Customer Support Automation

## Project overview

An n8n-based AI customer-support workflow for a Nigerian retail business. The intended workflow handles product-price enquiries, stock checks, order placement enquiries, order-status lookups, complaints, and unknown or low-confidence messages. The project is being developed for the AIL Lead Systems & Automation Engineer Candidate Assessment.

## Current implementation status

**Status: In progress — workflow review completed; repairs and end-to-end testing remain.**

The current exported workflow is stored in [n8n/NaijaMart-AI-WhatsApp-Automation-sanitized.json](n8n/NaijaMart-AI-WhatsApp-Automation-sanitized.json).

### Implemented or represented in the current workflow

- Receives a customer message through an n8n chat trigger.
- Uses an AI agent to classify messages into product availability, price enquiry, place-order, order-status, complaint, or unknown intents.
- Parses the AI classification and checks a confidence threshold.
- Includes database queries for products, stock availability, and order status.
- Includes a product/quantity validation path for order enquiries.
- Includes response-generation nodes for several customer intents.
- Includes a complaint-handling path and a Gmail staff-notification node.
- Includes a PostgreSQL setup/seed node and an automation-log table definition.
- Includes low-confidence, unknown-intent, and product-not-found response nodes.

> These are workflow elements present in the export, not a claim that every path has passed live testing.

### Known gaps to fix

- **Stock unavailable:** connect and implement the out-of-stock response branch.
- **Order not found:** connect a useful order-not-found response.
- **Invalid order quantity:** connect the invalid-quantity branch and return a clear explanation.
- **Order placement:** the current path validates product and quantity but does not create an order. Do not tell a customer that an order has been placed until order creation and confirmation are implemented.
- **Order lookup:** stop relying on a hard-coded phone number; validate and use the appropriate customer-provided order reference/identity.
- **Customer identity:** remove hard-coded customer phone assumptions and establish a safe, explicit way to associate messages with customers.
- **SQL safety:** replace brittle string interpolation in SQL queries with parameterized query inputs where supported.
- **Greeting and common messages:** add friendly greeting handling and test short inputs such as “hi”.
- **Complaint response:** ensure the customer receives the complaint acknowledgement even when staff notification is sent; avoid returning Gmail metadata as the chat answer.
- **Disconnected nodes:** review the disconnected Gemini model and price-clarification response path; connect or remove unused nodes.
- **Activity logging:** add an actual insert/logging step for each interaction and its outcome; creating the log table alone is not sufficient.
- **Failure handling:** handle AI-provider failures, database failures/timeouts, malformed model output, and notification failures with customer-safe fallback responses and appropriate internal alerts.
- **Operational visibility:** add a basic performance view or report for volume, intent, response outcomes, escalations, failures, and response times.
- **Security and privacy:** keep credentials out of exports, avoid unnecessary customer data in logs, and document access/retention expectations.

## Assessment deliverables still to prepare

- Repaired workflow export and a successful import/run check in n8n.
- Test plan and test record covering normal requests, missing products, out-of-stock items, invalid quantities, missing orders, low-confidence messages, complaints/escalations, and integration failures.
- Short demo video showing the workflow working.
- Problem/solution brief and architecture diagram.
- Cost analysis and risk/reliability/security notes.
- Operations runbook and handover/90-day improvement plan.

## Recommended implementation order

1. Repair all missing IF/Switch branches and make every customer path return a customer-facing response.
2. Implement actual order creation with duplicate/order-integrity safeguards.
3. Replace hard-coded customer identity and improve order-reference handling.
4. Parameterize SQL and add safe error/fallback paths.
5. Add interaction logging and an operational summary.
6. Run and document the full test matrix.
7. Complete the assessment documentation and demo.

## Validation note

This status document reflects a structural review of the exported workflow JSON. The workflow has **not** been represented as runtime-validated; import checks, credential configuration, database integration, and end-to-end execution must still be verified in the target n8n instance. Never commit real credentials, API keys, access tokens, or customer data.
