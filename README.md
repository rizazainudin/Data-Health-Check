# Data Health Check
This project automates the monthly data health reporting process for Channel Mapping and Product Mapping, which are essential components of the sales reporting pipeline. Without proper mapping, sales insights are incomplete and potentially misleading.

## Overview
**Business Problem**:
The manual process of extracting mapping data, analyzing it, and reporting to stakeholders was time-consuming and prone to human error. It also lacked consistency and scalability as data volume grew.
Previously, the data health check was performed manually:
1. Data Extraction: Export mapping data from Dataverse.
2. Data Processing: Create a pivot table to summarize the number of NonMapped entries by Country Code (ID, MY, PH, SG, TH, VN).
3. Reporting: Email the IBP team with a summary and attach the processed file.

This manual process was time-consuming, prone to delays, and introduced:
- Operational overhead due to repetitive tasks.
- Risk of human error in preparing and attaching the correct visual.
- Lack of timely updates for stakeholders.

## Objectives

| Main Point | Explanation |
| --- | --- |
| Reduce manual effort | Automate repetitive tasks like data extraction, pivoting, and emailing. |
| Improve accuracy | Minimize human error in data handling and reporting. |
| Increase frequency & visibility | Move from monthly to weekly updates for better monitoring. |
| Speed up the process | Deliver insights faster to stakeholders for timely decision-making. |

## Tools & Technologies Used

| Tool / Technology | Purpose |
| --- | --- |
| Power Automate | Orchestrates the entire workflow, including email triggers and actions. |
| Power BI Service | Hosts the Data Health Report and sends weekly snapshots via subscription. |
| Dataverse | Source of Channel and Product Mapping data. |
| SharePoint Folder | Storage for snapshots and CSV files. |
| Outlook Email | Sends automated summary reports to the IBP team. |

## Workflow (Post-Automation)
The new automated workflow leverages **Power BI Service** (Report Subscription) and **Power Automate** to streamline the process:

### 🟢 Trigger
The flow is triggered when a new email arrives in Outlook with the following properties:

- Subject: Weekly Data Health Check
- From: no-reply.powerbi@microsoft.com
- Has Attachment: Yes (Power BI report snapshot)

### ⚙️ Actions
1. Save Snapshot to SharePoint: The email attachment (report snapshot) is saved to a designated folder in SharePoint for archival and reference.
2. Run Power BI Dataset Query: A query is executed against the Power BI dataset to extract the non-mapped data.
3. Create a CSV Table: Save the data in the form of CSV
4. Send an email: An automated email is sent to the IBP team.
  Includes:
  📎 Snapshot image of the report (Summary of data health status)
  📎 CSV file with mapping breakdown
