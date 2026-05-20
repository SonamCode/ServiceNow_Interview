# Infosys - ServiceNow R1 Interview • 19th May, 2026

### Questions

---

## 1. Customer Service Management (CSM)

1. [What is CSM?](#q1)
2. [Core tables in CSM?](#q2)
3. [How SLA gets attached in CSM Case?](#q3)
4. [What is Service Offering?](#q4)
5. [How many Case Types are there OOB?](#q5)
6. [Fundamentals/components of CSM?](#q6)

---

## 2. ITSM (Incident, Problem, Change)

7. [Difference between Incident and Problem?](#q7)
8. [What is Major Incident?](#q8)
9. [Who can create Major Incident?](#q9)
10. [OOB who can create Major Incident?](#q10)
11. [Worked with Change Request?](#q11)

---

## 3. Catalog / Service Catalog

12. [Have you created Catalog Items?](#q12)
13. [Difference between Catalog Item and Record Producer?](#q13)

---

## 4. Flow Designer / Automation

14. [Worked with Flow Designer?](#q14)
15. [Different types of triggers in Flow Designer?](#q15)
16. [What are Flow Variables and their use?](#q16)
17. [Recommended limit of Flow steps?](#q17)

---

## 5. Client-Server Communication

18. [What is g_scratchpad?](#q18)
19. [What is GlideAjax?](#q19)
20. [Syntax of GlideAjax?](#q20)
21. [What is this GlideAjax code doing?](#q21)

---

## 6. Client Scripts / UI Policies

22. [Best practices for Client Scripts?](#q22)

---

## 7. Server-Side Questions / Scripting

23. [How to check active records in huge Incident table?](#q23)
24. [Using GlideAggregate for active record check?](#q24)
25. [Types of Business Rules?](#q25)
26. [Best practices for Server-side scripting?](#q26)

---

## 8. Database Views & Reporting

27. [What is Database View?](#q27)

---

## 9. Priority Matrix & Data Lookups

28. [How Priority gets set using Impact and Urgency?](#q28)
29. [How would you gather requirements for Priority Matrix setup?](#q29)
30. [Who configures Priority Matrix?](#q30)
31. [Steps to configure Priority Matrix?](#q31)
32. [What extra things are needed for custom table Priority setup?](#q32)

---

### Question's Answer

## 1. Customer Service Management (CSM)

**<a id="q1"></a>1. What is CSM?**
*   **Answer:** Customer Service Management (CSM) is a ServiceNow application that helps organizations manage customer support requests, resolve issues, and improve customer satisfaction by connecting customer service with other departments like engineering, operations, or finance.

**<a id="q2"></a>2. Core tables in CSM?**
*   **Answer:**
    *   Case (`sn_customerservice_case`)
    *   Consumer (`cmn_sec_users` / `sn_customerservice_consumer`)
    *   Account (`customer_account`)
    *   Contact (`customer_contact`)
    *   Product (`cmdb_model`)
    *   Asset (`alm_asset`)
    *   Entitlement (`service_entitlement`)
    *   Contract (`ast_contract`)

**<a id="q3"></a>3. How SLA gets attached in CSM Case?**
*   **Answer:** SLAs in CSM cases are attached based on SLA Definition rules defined on the Case table. These definitions specify start, pause, and stop conditions. When a Case is created or updated, the SLA engine evaluates these conditions. If the start condition is met and no other stop/cancel conditions are true, the SLA is attached. Entitlements and Contracts can also play a role in determining which SLA is applied.

**<a id="q4"></a>4. What is Service Offering?**
*   **Answer:** A Service Offering is a specific variation of a Service that defines a specific level of service for a specific price. It includes details like service commitments, SLAs, pricing, and the specific catalog items available to the user. It is part of the Service Portfolio Management.

**<a id="q5"></a>5. How many Case Types are there OOB?**
*   **Answer:** OOB, CSM provides various case types such as Product Support, Order, and generally categorizes cases into B2B (Business-to-Business, using Accounts and Contacts) and B2C (Business-to-Consumer, using Consumers).

**<a id="q6"></a>6. Fundamentals/components of CSM?**
*   **Answer:** Key components include:
    *   Case Management
    *   Accounts and Contacts (B2B)
    *   Consumers (B2C)
    *   Service Entitlements and Contracts
    *   Product and Asset Management
    *   Omni-channel communication (Portal, Chat, Email, Phone)
    *   Knowledge Management integration
    *   Communities
    *   Field Service Management (often integrated)

---

## 2. ITSM (Incident, Problem, Change)

**<a id="q7"></a>7. Difference between Incident and Problem?**
*   **Answer:**
    *   **Incident:** An unplanned interruption to an IT service or a reduction in the quality of an IT service. The goal is to restore normal service operation as quickly as possible.
    *   **Problem:** A cause of one or more incidents. The goal of Problem Management is to investigate the root cause of incidents and prevent them from happening again or minimize their impact.

**<a id="q8"></a>8. What is Major Incident?**
*   **Answer:** A Major Incident is an incident that has a high impact and high urgency, causing significant disruption to the business. It requires a coordinated, swift response, often involving a dedicated Major Incident Management team, special communication plans, and specific resolution processes.

**<a id="q9"></a>9. Who can create Major Incident?**
*   **Answer:** Typically, Major Incident Managers, IT Service Desk Managers, or sometimes designated L2/L3 support agents can propose or promote an incident to a Major Incident.

**<a id="q10"></a>10. OOB who can create Major Incident?**
*   **Answer:** OOB, users with the `major_incident_manager` role can promote a regular incident to a Major Incident or create a new Major Incident directly. ITIL users can typically propose a Major Incident, which then needs approval/promotion by a Major Incident Manager.

**<a id="q11"></a>11. Worked with Change Request?**
*   **Answer:** Yes, I have worked with Change Requests. Change Management involves standard, normal, and emergency changes. It includes processes for risk assessment, conflict detection, approvals (CAB), and implementation task generation to ensure changes to the IT environment are controlled and minimize risk.

---

## 3. Catalog / Service Catalog

**<a id="q12"></a>12. Have you created Catalog Items?**
*   **Answer:** Yes, I have created Catalog Items. These are the goods or services available for request in the Service Catalog. They require defining variables, UI Policies, Client Scripts, and an execution plan or workflow/Flow Designer flow for fulfillment.

**<a id="q13"></a>13. Difference between Catalog Item and Record Producer?**
*   **Answer:**
    *   **Catalog Item:** Used to request goods or services (e.g., a new laptop). It typically results in a Request (REQ), Requested Item (RITM), and Catalog Tasks (SCTASK). It uses Workflows or Flows for fulfillment.
    *   **Record Producer:** A specific type of catalog item that allows users to create task-based records (like an Incident, Change, or custom table record) from the Service Portal. It maps user inputs directly to fields on the target record.

---

## 4. Flow Designer / Automation

**<a id="q14"></a>14. Worked with Flow Designer?**
*   **Answer:** Yes, I have worked with Flow Designer. It is a non-technical interface for building and enabling process automation capabilities, allowing users to automate approvals, tasks, notifications, and record operations without writing complex code.

**<a id="q15"></a>15. Different types of triggers in Flow Designer?**
*   **Answer:**
    *   **Record-based triggers:** Created, Updated, Created or Updated.
    *   **Date/Time-based triggers:** Daily, Weekly, Monthly, Once, Run at specific time.
    *   **Application-based triggers:** Inbound Email, Service Catalog, REST API (Webhook), SLA Task.

**<a id="q16"></a>16. What are Flow Variables and their use?**
*   **Answer:** Flow variables are temporary storage elements defined within a Flow that allow you to store and pass data between different actions or steps within the same Flow. They are useful for storing calculated values, counters, or flags that need to be referenced later in the flow's execution.

**<a id="q17"></a>17. Recommended limit of Flow steps?**
*   **Answer:** ServiceNow generally recommends keeping flows modular and manageable. While there isn't a strict hard limit that stops execution at a low number, best practice suggests keeping it under 50 actions to maintain readability, performance, and ease of troubleshooting. For complex logic, it's recommended to use Subflows.

---

## 5. Client-Server Communication

**<a id="q18"></a>18. What is g_scratchpad?**
*   **Answer:** `g_scratchpad` is an object used to pass data from the server (using a Display Business Rule) to the client (using Client Scripts) when a form loads. This avoids synchronous GlideAjax calls on form load.

**<a id="q19"></a>19. What is GlideAjax?**
*   **Answer:** `GlideAjax` is an API used in Client Scripts to make asynchronous calls to the server to execute server-side code (Script Includes) and return data to the client without reloading the page.

**<a id="q20"></a>20. Syntax of GlideAjax?**
*   **Answer:**
    ```javascript
    var ga = new GlideAjax('ScriptIncludeName');
    ga.addParam('sysparm_name', 'functionName');
    ga.addParam('sysparm_myParam', 'value');
    ga.getXMLAnswer(callbackFunction);

    function callbackFunction(response) {
        // Process the response
        console.log(response);
    }
    ```

**<a id="q21"></a>21. What is this GlideAjax code doing?**
*   **Answer:** The code initializes a call to a specific Script Include, passes the function name to execute via `sysparm_name`, passes any additional parameters, and then asynchronously waits for the response. Once the server returns data, the callback function is executed to process that data on the client side (e.g., populating a field).

---

## 6. Client Scripts / UI Policies

**<a id="q22"></a>22. Best practices for Client Scripts?**
*   **Answer:**
    *   Use asynchronous GlideAjax (`getXMLAnswer`) instead of synchronous `getReference` or synchronous GlideAjax.
    *   Minimize server calls.
    *   Use UI Policies instead of Client Scripts for simple field visibility/read-only/mandatory changes.
    *   Avoid global client scripts.
    *   Check for `isLoading` at the start of `onLoad` and `onChange` scripts to prevent unwanted execution.

---

## 7. Server-Side Questions / Scripting

**<a id="q23"></a>23. How to check active records in huge Incident table?**
*   **Answer:** You can use `GlideAggregate` for counting records efficiently. For querying specific records, use `GlideRecord` with `setLimit()` or iterate using `next()` carefully. Database views or reporting can also be used. To just get a count, `GlideAggregate` is the best approach.

**<a id="q24"></a>24. Using GlideAggregate for active record check?**
*   **Answer:**
    ```javascript
    var count = new GlideAggregate('incident');
    count.addQuery('active', true);
    count.addAggregate('COUNT');
    count.query();
    if (count.next()) {
        gs.info('Active Incidents: ' + count.getAggregate('COUNT'));
    }
    ```

**<a id="q25"></a>25. Types of Business Rules?**
*   **Answer:**
    *   **Before:** Execute before the record is saved to the database.
    *   **After:** Execute after the record is saved to the database.
    *   **Async:** Execute asynchronously (in the background) after the record is saved.
    *   **Display:** Execute before the form is presented to the user, used to pass data from server to client via `g_scratchpad`.

**<a id="q26"></a>26. Best practices for Server-side scripting?**
*   **Answer:**
    *   Use `GlideAggregate` instead of `GlideRecord` for counting.
    *   Avoid hardcoding sys_ids; use System Properties.
    *   Keep Business Rules lightweight and use Script Includes for complex logic.
    *   Avoid `current.update()` in Before Business Rules.
    *   Use asynchronous execution (Async Business Rules or Events) when immediate response is not required.
    *   Add descriptive comments and use meaningful variable names.

---

## 8. Database Views & Reporting

**<a id="q27"></a>27. What is Database View?**
*   **Answer:** A Database View defines a table join for reporting purposes. It allows you to query data from multiple tables as if they were a single table. It is read-only and primarily used when you need to report on data that spans across related tables (e.g., Incidents and their associated SLAs).

---

## 9. Priority Matrix & Data Lookups

**<a id="q28"></a>28. How Priority gets set using Impact and Urgency?**
*   **Answer:** Priority is automatically calculated based on a Priority Data Lookup matrix (Priority Matrix). When a user selects the Impact and Urgency on a task (like Incident), the system cross-references these values in the "Data Lookup Definitions" rules to automatically populate the Priority field.

**<a id="q29"></a>29. How would you gather requirements for Priority Matrix setup?**
*   **Answer:** I would conduct workshops with key stakeholders (Service Desk managers, IT directors, business unit owners). I'd ask them to define levels of business impact (e.g., number of users affected, financial loss) and levels of urgency (how quickly the business needs it fixed). Then, map combinations of these to define what constitutes a P1 (Critical), P2 (High), etc., agreeing on the SLAs associated with each priority.

**<a id="q30"></a>30. Who configures Priority Matrix?**
*   **Answer:** System Administrators or users with the `admin` role or specific configuration roles (like `data_lookup_admin` or specific application admin roles) can configure the Priority Matrix.

**<a id="q31"></a>31. Steps to configure Priority Matrix?**
*   **Answer:**
    1.  Navigate to **System Policy > Rules > Priority Data Lookups** (or Data Lookup Definitions).
    2.  Open the record for the relevant table (e.g., Incident).
    3.  In the related list "Matcher Field Definitions", ensure Impact and Urgency are matcher fields.
    4.  In the "Setter Field Definitions", ensure Priority is the setter field.
    5.  In the "Data Lookup Definition" related list (or the actual lookup table like `dl_u_priority`), add or modify rows defining the Matrix (e.g., Impact = 1, Urgency = 1 -> Priority = 1).

**<a id="q32"></a>32. What extra things are needed for custom table Priority setup?**
*   **Answer:** For a custom table:
    1.  Ensure the custom table has `impact`, `urgency`, and `priority` fields (usually inherited if extended from Task).
    2.  Create a new Data Lookup Definition for the custom table.
    3.  Define the Matcher fields (Impact, Urgency).
    4.  Define the Setter field (Priority).
    5.  Create a dedicated lookup table (or use an existing one if applicable, though usually a specific one is better if rules differ) to hold the matrix values, or populate the generic data lookup table referencing your custom table.
    6.  Ensure the fields are on the form and dictionary overrides are set up if needed for default values or choices.