*Intuz — Your automation partner, one workflow at a time.*

<p align="center">
  <picture>
    <img alt="Banner Image" src="https://github.com/user-attachments/assets/210f97fc-0fce-404a-b647-7dfe1302cd37" />
  </picture>
</p>

[Intuz](https://www.intuz.com) helps organizations orchestrate AI, automation, and enterprise systems through scalable workflows. Our repository showcases proven implementations across healthcare, operations, customer support, document processing, sales, and back-office functions, enabling teams to accelerate automation initiatives without starting from scratch.

[N8N Creator](https://n8n.io/creators/intuz/) · [AI Automation Service](https://www.intuz.com/ai-automation-services/) · [AI Chatbot Development](https://www.intuz.com/ai-agents-for-business-automation/) · [For Custom Workflow Automation](https://www.intuz.com/get-started/)

# Automate Shopify orders from Airtable with Gmail confirmations

This n8n template from Intuz provides a complete solution to automate your order creation process.

It seamlessly syncs order data from an Airtable base directly to your Shopify store, creates the official order, and automatically sends a beautiful confirmation email to the customer, closing the loop by updating the status in Airtable.

## Who’s this workflow for?

- E-commerce Managers
- Operations Teams
- Businesses with Custom Order Processes (e.g., B2B, phone orders, quotes)
- Shopify Store Owners using Airtable as a CRM

## How it works

1. **Triggered from Airtable:** The workflow starts instantly when an Airtable Automation sends a signal via a webhook. This happens when you mark an order as ready to be processed in your Airtable base.

2. **Fetch Order Details:** n8n receives the record ID from Airtable and fetches the complete order details, including customer information and the specific line items for that order.

3. **Create Order in Shopify:** All the gathered information is used to create a new, official order directly in your Shopify store.

4. **Send Confirmation Email:** Once the order is successfully created in Shopify, a professionally formatted HTML order confirmation email is sent to the customer via Gmail.

5. **Update Airtable Status:** Finally, the workflow updates the original order record in Airtable, marking its status as “Done” to prevent duplicate processing and keep your records in sync.

## Key Requirements to Use This Template

1. **n8n Instance:** An active n8n account (Cloud or self-hosted).
2. **Airtable Base:** An Airtable base on a **Pro** plan or higher (required for Airtable Automations). It should contain tables for Orders and Order Line Items.
3. **Shopify Store:** An active Shopify store with API access permissions.
4. **Gmail Account:** A Gmail account to send confirmation emails.

## Setup Instructions

### 1. Configure the n8n Workflow

- **Webhook Node:** Activate the workflow to get the Production URL from the **Webhook** node. Copy this URL.
- **Airtable Nodes:** In the **Get a record** and **Update record** nodes, connect your Airtable credentials and select the correct Base and Table IDs.
- **Shopify Node:** In the **Create an order** node, connect your Shopify store using OAuth2 credentials.
- **Gmail Node:** In the **Send a message** node, connect your Gmail account.

### 2. Set Up the Airtable Automation (Crucial Step)

- Go to your Airtable base and click on **Automations**.
- Create a new automation. For the trigger, select **When a record meets conditions**.
- Choose your Orders table and set a condition that makes sense for you (e.g., When “Shopify Ordered” is “Pending”).
- For the action, choose **Run a script**. Paste the code below into the script editor **as-is**. Do not change the placeholder until you have copied **your** Production URL from the n8n Webhook node:

```javascript
const inputConfig = input.config();
const recordId = inputConfig.recordId;
const webhookUrl = 'PASTE_YOUR_N8N_PRODUCTION_URL_HERE';

await fetch(webhookUrl, {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ recordId: recordId }),
});```

FAQ
Is this template free to use? Yes. It's an open-source n8n workflow published by Intuz — copy the workflow JSON from this repo and import it into your own n8n instance at no cost.

Do I need a paid n8n plan to run this? No. It runs on n8n's free self-hosted Community Edition or on n8n Cloud. You'll need your own Airtable, Shopify, and Gmail credentials, not a specific n8n pricing tier.

How does Airtable start the workflow? An Airtable Automation posts the record ID to the n8n webhook when an order meets your condition (e.g., “Shopify Ordered” is “Pending”). n8n then creates the Shopify order, emails the customer, and marks the Airtable record as “Done.”

Related n8n templates from Intuz
Automate QuickBooks invoicing & customer creation from Airtable sales orders
Automate expense reporting from Airtable to QuickBooks
Automate full-cycle invoicing from Airtable to QuickBooks and Stripe
See all of Intuz's free n8n templates

Connect with us
Intuz is a USA-based AI & workflow automation company with 16+ years of experience building custom AI-enabled workflow automations for SMBs and Enterprises, specializing in agentic AI, LLM integrations, and CRM/ERP sync across Healthcare, FinTech, eCommerce, Manufacturing, and Real Estate.

Website: https://www.intuz.com
Email: getstarted@intuz.com
LinkedIn: https://www.linkedin.com/company/intuz/
Get Started: https://n8n.partnerlinks.io/intuz
For Custom Workflow Automation
Click here - Get Started

