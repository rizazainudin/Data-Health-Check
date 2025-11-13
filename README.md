# Data Health Check
This automation ensures timely distribution of the Data Health Check snapshot to the business team every Monday. It leverages Power BI subscription emails as the trigger and eliminates manual steps in saving and sharing the report.

This data health is an essential component of the sales reporting pipeline. Without proper mapping, sales insights are incomplete and potentially misleading.

## Overview
**Business Problem**:
The manual process of extracting mapping data, analyzing it, and reporting to stakeholders was time-consuming and prone to human error. It also lacked consistency and scalability as data volume grew.
Previously, the data health check was performed manually:
1. Data Extraction: Export mapping data from Dataverse.
2. Data Processing: Create a pivot table to summarize the number of non-mapped entries by country (ID, MY, PH, SG, TH, VN).
3. Reporting: Email the business team with a summary and attach the processed file.

This manual process was time-consuming, prone to delays, and introduced:
- Operational overhead due to repetitive tasks.
- Risk of human error in preparing and attaching the correct visual and data file.
- Lack of timely updates for stakeholders, pre-automation was monthly update.

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
| Power BI Service | Hosts the Data Health Report and sends weekly snapshots via subscription. |
| Power Automate | Orchestrates the entire workflow, including email triggers and actions. |
| Dataverse | Source of Channel and Product Mapping data. |
| SharePoint Folder | Storage for snapshots and CSV files. |
| Outlook Email | Sends automated summary reports to the IBP team. |

## Flow Structure
The new automated workflow leverages **Power BI Service** (Report Subscription) and **Power Automate** to streamline the process:

### Trigger
The flow is triggered when a new email arrives in Outlook with the following properties:

- Subject: Data Health Check
- From: `no-reply-powerbi@microsoft.com`
- Include Attachments: Yes (Power BI report snapshot)

### Actions

<ins> Branch 1: Non-Mapped Data Extraction </ins>
- Initialize variable: CSV Data
- Apply to each Country Code (ID, MY, PH, SG, TH, VN):
   - Run a query against dataset (Power BI)
   - Extract non-mapped rows for each country
   - Save results in CSV structure
   - Append to array variable
 
<ins> Branch 2: Image Handling + Data Summary</ins>
- Initialize variable: Table HTML
- Initialize variable: Snapshot
- Apply to each attachment:
   - Condition - Checks if the attachment filename contains .png (ensures only image files are processed).
   - If Yes (Attachment is PNG): 
      - **Compose File Format & File Content**: Prepares the attachment data for saving.
      - **Create File**: Saves the snapshot image to SharePoint.
      - **Get File Content Using Path**: Retrieves the saved file content for further use.
      - **Compose Snapshot PNG**: Stores the snapshot image in a variable for embedding in the email.
      - **Run a Query Against Dataset (Summary)**: Executes a Power BI query to get summary of non-mapped data.
      - **Parse JSON Summary**: Converts the query result into structured data.
      - **Create HTML Table Summary**: Builds an HTML table summarizing non-mapped counts by country.
      - **Append to String Variable Snapshot**: Adds snapshot details to the email body.
      - **Append to String Variable Summary**: Adds summary table to the email body.
    
<ins> Merge & Output</ins>
- Compose Table CSS Styling
- Compose Message (email body)
- Compose Attachment (CSV files for each country)
- Send an email (V2) to Business Team:
   - Includes snapshot image
   - Includes summary table
   - Includes CSV attachments

**Expression**
| Step Name | Purpose | Expression |
| --- | --- | --- |
| Compose Date | Generate timestamp and append it to the file name | `convertFromUtc(utcNow(), 'Singapore Standard Time', 'yyyyMMddhhmm')` |
| Compose File Format | Extract the actual file format from the attachment name | `substring(items('Apply_to_each')?['name'], lastIndexOf(items('Apply_to_each')?['name'], '.'))` |
| Compose File Content | Convert file content from Base64 to binary before saving in SharePoint | `base64ToBinary(items('Apply_to_each')?['contentBytes'])` |
| Compose Snapshot PNG | Convert file to URI for embedding in HTML email body | `dataUri(body('Get_file_content_using_path'))` | 

