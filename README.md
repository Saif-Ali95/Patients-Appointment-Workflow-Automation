# Patients-Appointment-Workflow-Automation
Clinic Appointment Automation (n8n Workflow)
Automates appointment confirmation, rescheduling, and cancellation via Google Sheets, Calendar, and Gmail.


Workflow Overview
Three main flows in this n8n workflow:

New Appointment

Reschedule Request

Cancellation Request

Each flow:

Listens for a webhook trigger

Queries Google Sheets for patient & appointment data

Updates Google Sheets with status

Updates Google Calendar (create/update/cancel)

Sends an email confirmation to the patient

⚙️ Getting Started
Prerequisites
n8n instance with access to:

Webhook trigger

Google Sheets credentials

Google Calendar credentials

Gmail or SMTP credentials

A Google Sheet with at least these columns:

Patient ID, Name, Email, Appointment Date, Appointment Time, Status

A Google Calendar configured for appointments

🛠 Workflow Setup
Import Workflow

Go to n8n Editor → Top right menu → Import from file

Upload your workflow JSON

Connect Credentials

Go to the Credentials panel in n8n

Add or update:

Google Sheets

Google Calendar

Gmail (or SMTP)

Set Trigger URLs

Each webhook node displays a unique URL

Copy these and configure your front-end or external triggers

Configure Sheets & IDs

In Query and Update nodes, select your target Sheet and Tab

Ensure correct column mapping (e.g., Patient ID, Status)

Customize Email Templates

Adjust the Appointment, Reschedule, and Cancel email nodes

Use variables like {{ $json.AppointmentDate }}, {{ $json.PatientName }}, and {{ $('Code').item.json.time }}

🕑 Execution Flow
A. 🆕 New Appointment Flow
Webhook triggers upon new booking

Google Sheets Query retrieves related row

Google Calendar creates the event

Appointment Email sends confirmation

B. 🔄 Reschedule Flow
Reschedule webhook triggers on user request

QueryParameters node fetches patient data

Calendar event is updated

Formatter normalizes date/time

Sheets and Email updated accordingly

C. ❌ Cancellation Flow
Cancel webhook receives the request

Sheets are updated with “Cancelled”

Google Calendar event is cancelled

Cancellation email is sent

🧩 Customization
Add new triggers: clone pattern of existing flows (Confirmation, Reschedule, Cancellation)

Change columns: update Google Sheets node column settings to match your sheet

Style emails: update HTML content to customize branding

Add logging: insert additional nodes e.g. “Set” or “Webhook Response” for debugging

💾 Backup & Versioning
Your workflow is already versioned as part of this GitHub repository.

To use in a new n8n instance:

Import JSON file via the n8n Editor

Reconnect credentials to your new account

