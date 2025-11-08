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
| Reduce Manual Effort | Automate repetitive tasks like data extraction, pivoting, and emailing. |
| Improve Accuracy | Minimize human error in data handling and reporting. |
| Increase Frequency & Visibility | Move from monthly to weekly updates for better monitoring. |
| Speed Up the Process | Deliver insights faster to stakeholders for timely decision-making. |

## Tools & Technologies Used

| Tool / Technology | Purpose |
| --- | --- |
| Power Automate | Orchestrates the entire workflow, including email triggers and actions. |
| Power BI Service | Hosts the Data Health Report and sends weekly snapshots via subscription. |
| Dataverse | Source of Channel and Product Mapping data. |
| SharePoint Folder | Storage for snapshots and CSV files. |
| Outlook Email | Sends automated summary reports to the IBP team. |
