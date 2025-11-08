# Data Health Check
Automates weekly Data Health Check by extracting mapping data from Dataverse, extracting visuals from PBI, storing in SharePoint, and emailing stakeholders to reduce manual effort and improve accuracy.

## Overview
**Business Problem**:
Business users need monthly visibility into the completeness of channel and product mapping. The underlying data for mapped and unmapped product and channel mappings is stored in Dataverse.
Previously, this process required:
- Manual extraction of data from Dataverse via CSV export.
- IT BRM manually analyzing unmapped items and creating a summary using pivot tables.
- Consolidating each country’s unmapped rows into different Excel tabs.

This manual process was time-consuming, prone to delays, and introduced:
- Operational overhead due to repetitive tasks.
- Risk of human error in preparing and attaching the correct visual.
- Lack of timely updates for stakeholders.

--

## Objectives
- Reduce manual effort by automating data retrieval and reporting.
- Improve accuracy by eliminating manual consolidation and pivoting.
- Speed up the process by delivering insights automatically on a fixed schedule.
