# Cognizant - ServiceNow Developer Interview • 11 May 2026

### Questions
---

## 1. Client Scripts & UI Policies

1. [Have you written Client Script? There is a checkbox named Global?](#q1)
2. [What is All Views?](#q2)
3. [What all functions/methods can you use in onChange Client Script?](#q3)
4. [OnChange method 5 parameters?](#q4)
5. [If `isTemplate = true`, what will happen?](#q5)
6. [UI Policy vs Data Policy?](#q6)
7. [Can we write script in Data Policy?](#q7)
8. [Can we write script in UI Policy?](#q8)

---

## 2. ITSM & Incident Management

9. [Parent-Child Incident — explain.](#q9)
10. [During a Major Incident, incident owner wants notification updates every 30 mins. Junior suggests email → causes email storms. What will you do?](#q10)

---

## 3. Data Import & Transform Maps

11. [Transform Maps?](#q11)
12. [Import data into `sys_user` table — explain `onStart` and `onBefore`. If Excel has 10 records, how many times will they run?](#q12)

---

## 4. Integration & API

13. [Worked on Integrations?](#q13)
14. [How did you do Jira integration?](#q14)
15. [What are the steps for Jira integration?](#q15)

---

## 5. CSM, HRSD, CMDB & General Modules

16. [Other than ITSM module?](#q16)
17. [In CSM, what type of customer requirements?](#q17)
18. [HRST / HRSD?](#q18)
19. [CMDB?](#q19)
20. [Worked on Analytics Platform / Dashboard?](#q20)

---

## 6. End-to-End Development

21. [End-to-end development — have you done it?](#q21)
22. [Give an example of end-to-end development.](#q22)
23. [Other example?](#q23)

### Question's Answer

## 1. Client Scripts & UI Policies

**<a id="q1"></a>1. Have you written Client Script? There is a checkbox named Global?**
*   **Answer:** Yes, I write Client Scripts frequently. The **Global** checkbox indicates that the script will run on all form views of the selected table. If unchecked, you must specify a single 'View' (like Default, Self Service, etc.) where the script will execute. (Note: in the context of application scopes, 'Global' can also mean the script belongs to the Global scope, but on the form layout, it refers to views).

**<a id="q2"></a>2. What is All Views?**
*   **Answer:** This directly relates to the "Global" checkbox. When "Global" is checked, it means "All Views". The script executes regardless of whether the user is looking at the Default view, the Mobile view, or a custom workspace view.

**<a id="q3"></a>3. What all functions/methods can you use in onChange Client Script?**
*   **Answer:** In an onChange Client Script, you primarily use the `g_form` API (e.g., `g_form.getValue()`, `g_form.setValue()`, `g_form.setMandatory()`, `g_form.addInfoMessage()`). You also use the `g_user` API (to get current user details like roles), and `GlideAjax` to communicate asynchronously with the server.

**<a id="q4"></a>4. OnChange method 5 parameters?**
*   **Answer:** The five parameters provided automatically in an onChange function are: `control` (the HTML element), `oldValue` (the field's value before the change), `newValue` (the field's value after the change), `isLoading` (boolean, true if the form is currently loading), and `isTemplate` (boolean, true if the change is being applied via a template).

**<a id="q5"></a>5. If `isTemplate = true`, what will happen?**
*   **Answer:** `isTemplate` is true when the field value is being changed automatically because a user applied a Template to the form. Usually, we add `|| isTemplate` to the `if (isLoading || newValue == '') { return; }` condition to prevent the Client Script from executing heavily when a template is applying mass changes, saving browser performance.

**<a id="q6"></a>6. UI Policy vs Data Policy?**
*   **Answer:** 
    *   **UI Policies** are client-side. They make fields mandatory, read-only, or visible dynamically on the form UI, but they can be bypassed (e.g., via list edits or REST API calls). 
    *   **Data Policies** are server-side. They enforce data integrity (mandatory, read-only) at the database level, ensuring rules are followed regardless of how the record is updated (Form, List, API, Import Set).

**<a id="q7"></a>7. Can we write script in Data Policy?**
*   **Answer:** No. Data Policies do not support scripting. They only use the condition builder and UI-based rules (Make Mandatory, Make Read-Only) because they must execute extremely fast purely at the database transaction layer.

**<a id="q8"></a>8. Can we write script in UI Policy?**
*   **Answer:** Yes. UI Policies have a section for **Run Scripts** (Execute if true / Execute if false). This allows you to write client-side JavaScript for more complex logic that the standard condition builder cannot handle.

---

## 2. ITSM & Incident Management

**<a id="q9"></a>9. Parent-Child Incident — explain.**
*   **Answer:** The Parent-Child incident relationship is used when multiple incidents are caused by the same underlying issue. Instead of updating each one manually, you link them to a single 'Parent' Incident. When the Parent incident is updated or resolved, out-of-the-box Business Rules automatically cascade those updates (like work notes, resolution code) to all linked 'Child' incidents.

**<a id="q10"></a>10. During a Major Incident, incident owner wants notification updates every 30 mins. Junior suggests email → causes email storms. What will you do?**
*   **Answer:** Sending an email every 30 minutes to a large group will definitely cause an email storm and alert fatigue. Instead, I would recommend using the **Major Incident Workbench** where stakeholders can view real-time status. For active notifications, we could integrate with a communication channel (Slack/MS Teams via IntegrationHub) to post silent updates to a dedicated channel, or send targeted SMS alerts only to the critical resolution team.

---

## 3. Data Import & Transform Maps

**<a id="q11"></a>11. Transform Maps?**
*   **Answer:** A Transform Map is a set of field maps that determine the relationships between fields in an Import Set table (the staging area) and fields in an existing ServiceNow target table. It handles the conversion, validation, and migration of data.

**<a id="q12"></a>12. Import data into `sys_user` table — explain `onStart` and `onBefore`. If Excel has 10 records, how many times will they run?**
*   **Answer:** 
    *   **onStart:** Runs once before any rows are processed. Used to initialize variables or log the start. (Runs **1 time**).
    *   **onBefore:** Runs before a specific row is transformed and inserted/updated in the target table. Used to validate or alter data for that specific user record. (Runs **10 times**).

---

## 4. Integration & API

**<a id="q13"></a>13. Worked on Integrations?**
*   **Answer:** Yes, extensively. I have built both inbound (Scripted REST APIs) and outbound integrations (REST Messages, IntegrationHub) connecting ServiceNow with platforms like Jira, Active Directory, Workday, and SolarWinds.

**<a id="q14"></a>14. How did you do Jira integration?**
*   **Answer:** I used Outbound REST Messages triggered by an Async Business Rule. When an incident met certain conditions (e.g., Category = Software), the BR triggered a Script Include. The Script Include formatted a JSON payload with the incident details and sent a POST request to Jira's REST API. Jira returned the new Issue Key, which was parsed and saved back to the ServiceNow incident.

**<a id="q15"></a>15. What are the steps for Jira integration?**
*   **Answer:** 
    1. Create Jira API Token/Credentials.
    2. Set up an Authentication profile in ServiceNow (Basic Auth or OAuth).
    3. Create an Outbound REST Message in ServiceNow with the Jira endpoint and HTTP Method (POST for create).
    4. Define variables in the Request Body (Summary, Description).
    5. Write a Script Include to instantiate `sn_ws.RESTMessageV2`, populate variables, and execute the call.
    6. Create an Async Business Rule on the Incident table to trigger the Script Include.

---

## 5. CSM, HRSD, CMDB & General Modules

**<a id="q16"></a>16. Other than ITSM module?**
*   **Answer:** Besides ITSM, I have experience working on Customer Service Management (CSM), HR Service Delivery (HRSD), ITOM (Discovery, CMDB), and building custom scoped applications from scratch.

**<a id="q17"></a>17. In CSM, what type of customer requirements?**
*   **Answer:** Common requirements in CSM involve setting up Account and Contact hierarchies, defining Entitlements and SLAs specific to different customers, configuring the Customer Service Portal (CSP) for case creation, and setting up Advanced Work Assignment (AWA) to route cases to the correct agent queues based on skill and availability.

**<a id="q18"></a>18. HRST / HRSD?**
*   **Answer:** In HR Service Delivery, I have configured HR Cases, HR Services, and Record Producers on the Employee Center. A major part of the work involves handling data security using HR Criteria and Client Role Rules, ensuring strict confidentiality for sensitive employee data (COE Security Policies).

**<a id="q19"></a>19. CMDB?**
*   **Answer:** My CMDB experience includes creating new CI Classes, configuring the CI Class Manager, setting up Identification and Reconciliation engine (IRE) rules to prevent duplicate CIs, and creating Transform Maps/Service Graph Connectors to import assets from external discovery tools.

**<a id="q20"></a>20. Worked on Analytics Platform / Dashboard?**
*   **Answer:** Yes, I have created standard Reports (Bar, Pie, Time Series) and combined them into interactive Dashboards. I have also used Database Views to join multiple tables (like Incident and Metric) for complex reporting, and utilized Performance Analytics (PA) for trend analysis over time.

---

## 6. End-to-End Development

**<a id="q21"></a>21. End-to-end development — have you done it?**
*   **Answer:** Yes, I have built complete custom Scoped Applications from scratch. This involves everything from data modeling (creating tables, fields) to building the backend logic, and designing the final user interface (Portals or Workspaces).

**<a id="q22"></a>22. Give an example of end-to-end development.**
*   **Answer:** I built a "Visitor Management System" for office security. I created custom tables for Visitors and Visits. I built a Record Producer for employees to pre-register guests on the portal. I created Flow Designer flows to automatically send a QR code via email to the visitor upon approval. Finally, I built a custom Workspace for the reception desk to scan the QR code and log the visitor's entry/exit times.

**<a id="q23"></a>23. Other example?**
*   **Answer:** Another example is a "Fleet Vehicle Management" app. I created a custom table to track company cars, another for booking requests, and a third for maintenance logs. I set up UI Policies to handle date validations, a Scheduled Job to alert managers of upcoming maintenance, and a Dashboard to show fleet utilization rates.
