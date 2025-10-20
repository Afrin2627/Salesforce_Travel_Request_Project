# ☁️ Salesforce Travel Request Management System  

### 🔹 Cloud-Based CRM Automation Project  

The **Travel Request Management System** is a **Salesforce Cloud Application** that streamlines how employees submit, approve, and track travel requests.  
It combines **declarative tools (Flows, Email Alerts, Reports)** and **programmatic logic (Apex Trigger)** within a custom **Lightning App** — delivering a complete, automated CRM experience.

---

## 🧠 Tech Stack Summary
| Category | Technology / Tool | Description |
|-----------|------------------|--------------|
| ☁️ Platform | Salesforce (Force.com) | Cloud-based CRM & low-code platform |
| ⚙️ Backend Logic | Apex Triggers | Automates approval creation for travel requests |
| 🔄 Automation | Flows, Email Alerts | Streamlines workflows for high-amount approvals |
| 💻 UI Layer | Lightning App Builder | Custom navigation & object access |
| 🌐 Integration | Web-to-Lead Form | Captures leads from external websites |
| 📊 Analytics | Reports & Dashboards | Monitors travel amounts and approval trends |
| 📦 Data Tools | Data Import Wizard | Bulk upload and management of records |

---

## 🧩 Core Features
- 🧾 **Submit & Manage Travel Requests**  
- ✅ **Automatic Approval Record Creation** for high-value requests (> ₹10,000)  
- 📧 **Email Notifications** to approvers triggered via Flows  
- 🖥️ **Lightning App Interface** for centralized management  
- 📊 **Reports & Dashboards** showing expense insights  
- 🌐 **Web-to-Lead Integration** for external submissions  

---

## ⚙️ Custom Objects & Relationships

### 1️⃣ Travel_Request__c  
Stores details about each employee’s travel (Destination, Dates, Amount, etc.)

### 2️⃣ Travel_Approval__c  
Tracks approval status for travel requests.

**Relationship:**  
`Travel_Approval__c.Related_Travel_Request__c → Lookup → Travel_Request__c`

---

## 💻 Apex Trigger

Automatically creates an approval record when a travel request exceeds ₹10,000.

```apex
trigger TravelRequestTrigger on Travel_Request__c (after insert) {
    List<Travel_Approval__c> approvalsToCreate = new List<Travel_Approval__c>();

    for (Travel_Request__c req : Trigger.new) {
        if (req.Amount__c > 10000) {
            approvalsToCreate.add(new Travel_Approval__c(
                Related_Travel_Request__c = req.Id,
                Status__c = 'Pending Approval'
            ));
        }
    }

    if (!approvalsToCreate.isEmpty()) {
        insert approvalsToCreate;
    }
}
🔄 Automation (Flows & Alerts)
🧠 Flow: Travel_Request_High_Amount_Flow
Checks if Amount__c > 10000

Sends email alert to approver

Updates approval record status

✉️ Email Alert
Template: High Amount Travel Request Alert

Triggered automatically from the Flow

🧭 Lightning App Navigation
Includes key navigation tabs:

🏠 Home

🚀 Travel Requests

✅ Travel Approvals

📈 Reports

📊 Dashboards

🌐 Integration — Web-to-Lead Form
Captures leads directly from an external website into Salesforce Leads.

html
Copy code
<form action="https://webto.salesforce.com/servlet/servlet.WebToLead?encoding=UTF-8&orgId=00DdM00000fqnUs" method="POST">
  <input type=hidden name="oid" value="00DdM00000fqnUs">
  <input type=hidden name="retURL" value="https://www.salesforce.com/thankyou">
  <label>First Name</label><input name="first_name" type="text"><br>
  <label>Last Name</label><input name="last_name" type="text"><br>
  <label>Email</label><input name="email" type="text"><br>
  <label>Company</label><input name="company" type="text"><br>
  <input type="submit" name="submit">
</form>
📊 Reports & Dashboards
Reports:

Total Travel Requests by Employee

High-Amount Requests by Status

Dashboard:

Visual summary of total travel costs and approvals

🎥 Demo Video
🎬 https://drive.google.com/file/d/1rs2URxzM0OSJ1ATIlQP3XOdkyJG6XIYf/view?usp=sharing

Video Highlights:

Creating a new Travel Request

Automatic Approval Record generation via Trigger

Email Notification Flow

Dashboard and Report Overview

📁 Folder Structure
css
Copy code
Salesforce_Travel_Request_Project/
│
├── README.md
├── Project_Report.pdf
├── demo-video.mp4
├── screenshots/
│   ├── flow.png
│   ├── trigger.png
│   ├── dashboard.png
│   └── lightning-app.png
└── web-to-lead.html
🏁 Conclusion
The Salesforce Travel Request Management System demonstrates end-to-end CRM application development using both Admin and Developer tools.
It simplifies travel approval workflows, automates manual tasks, and provides analytical insights through Reports and Dashboards.
This project reflects proficiency in Salesforce Cloud, Automation, Apex, and Integration — essential skills for real-world CRM solutions.

