# 🚀 Travel Request Management System


---

## 📘 Overview

The **Travel Request Management System** is a Salesforce-based project designed to streamline the process of submitting, approving, and tracking employee travel requests.  
It automates workflows using Salesforce Flows, Apex triggers, and Email Alerts while providing an intuitive Lightning App interface for easy navigation and management.

---

## 🧩 Features

- Create and manage **Travel Requests**  
- Automated **Approval Creation** for high-value requests  
- **Email Notifications** to approvers for high-amount requests  
- Custom **Lightning App** for travel management  
- **Reports and Dashboards** for monitoring expenses  
- **Web-to-Lead Integration** for capturing external submissions  

---

## 🏗️ Tech Stack

| Component | Description |
|------------|-------------|
| **Platform** | Salesforce |
| **Automation Tools** | Flows, Email Alerts |
| **Backend Logic** | Apex Triggers |
| **UI Framework** | Lightning App Builder |
| **Data Management** | Data Import Wizard |
| **Integration** | Web-to-Lead HTML Form |
| **Analytics** | Reports & Dashboards |

---

## ⚙️ Objects & Relationships

### 🧾 Custom Objects
1. **Travel_Request__c** – Employee’s travel details (Destination, Dates, Amount, etc.)  
2. **Travel_Approval__c** – Approval records linked to each travel request  

**Relationship:**  
→ `Travel_Approval__c.Related_Travel_Request__c` → Lookup relationship to Travel_Request__c  

---

## 🔄 Automation

### **1. Flow: Travel Request High Amount Flow**
- Checks if the `Amount__c > 10000`
- Sends **Email Alert** to manager for approval

### **2. Email Alert**
- Template: `High Amount Travel Request Alert`
- Triggered automatically from the flow

---

## 💻 Apex Trigger

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
🧭 Lightning App Navigation
Home

Travel Requests

Travel Approvals

Reports

Dashboards

🌐 Integration
Web-to-Lead HTML Form
Used to collect data from an external website directly into Salesforce Leads.

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
Report: Total Travel Requests by Employee

Dashboard: Visual analysis of total travel amount and approvals

🎥 Demo Video
A walkthrough video demonstrates:

Creating a travel request

Automatic approval creation via trigger

Flow execution and email notification

Reports and Dashboard overview

📎 [https://drive.google.com/file/d/1rs2URxzM0OSJ1ATIlQP3XOdkyJG6XIYf/view?usp=sharing]

🏁 Conclusion
This Salesforce project showcases end-to-end CRM app development using both declarative and programmatic tools.
It simplifies travel request management, increases approval efficiency, and enhances visibility through data-driven insights.

