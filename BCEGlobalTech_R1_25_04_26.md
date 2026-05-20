# BCE Global Tech - ServiceNow Developer R1 Interview &#x2022; 25th April, 2026

### Questions
---

## 1. ITSM

1. [End-to-end process of ITSM](#q1)
2. [Maintaining ITSM](#q2)

---

## 2. Catalog / Service Catalog

3. [What are different types of Catalog Items?](#q3)
4. [Difference between Order Guide, Record Producer, and Catalog Item](#q4)
5. [Can we use them in Workflow?](#q5)

---

## 3. Flow Designer / Automation

6. [What is Flow Designer?](#q6)
7. [Can we call Flow Designer from server-side scripting?](#q7)

---

## 4. Client-Server Communication

8. [How can we send data from server side to client side? Different options in ServiceNow](#q8)
9. [Can we use Query Business Rule instead of Display Business Rule?](#q9)

---

## 5. ACL / Security / Scripting

10. [What is Inherit checkbox?](#q10)
11. [Use of Isolate Script checkbox](#q11)
12. [What is ACL and types of ACLs?](#q12)

---

## 6. Script Includes / Reference Qualifier

13. [How many types of Script Includes do we have in ServiceNow?](#q13)
14. [Can we use Script Include in Reference Qualifier?](#q14)
15. [Types of Reference Qualifiers](#q15)

---

## 7. Dictionary / Form / UI Configuration

16. [What is Dictionary Override?](#q16)
17. [Remove Category, Assignment Group, Assigned To globally from Incident list view](#q17)
18. [When State = In Progress:](#q18)

* Hide Resolution Information section
* Make Configuration Item read-only
* Make Description read-only

19. [Should it be onLoad or onChange?](#q19)
20. [Why Configuration Item is not becoming read-only?](#q20)

---

## 8. Client Scripts / UI Policies

21. [How to implement the above requirement using Client Script/UI Policy?](#q21)

---

## 9. Server-Side Questions

22. [Bulk update without triggering notifications and Business Rules](#q22)
23. [Priority field wrong → recalculate based on Impact & Urgency](#q23)
24. [SLA not applied due to misconfiguration → attach SLA manually](#q24)
25. [Background Script](#q25)

---

### Question's Answer

## 1. ITSM

**<a id="q1"></a>1. End-to-end process of ITSM**
*   **Answer:** The ITSM (IT Service Management) process typically follows the ITIL framework to deliver and support IT services. The core flow includes:
    *   **Service Catalog / Request Fulfillment:** Users request standard services or items (creates REQ/RITM).
    *   **Incident Management:** Users report disruptions; the goal is to restore normal service operation as quickly as possible.
    *   **Problem Management:** Investigating the root cause of one or multiple recurring incidents to provide permanent workarounds or fixes.
    *   **Change Management:** Implementing the fix identified by Problem Management in a controlled manner to minimize risk.
    *   **Knowledge Management:** Documenting known errors, workarounds, and processes to aid in future resolution.

**<a id="q2"></a>2. Maintaining ITSM**
*   **Answer:** Maintaining ITSM involves continuous monitoring and improvement (CSI). It includes tracking Key Performance Indicators (KPIs) like Mean Time To Resolve (MTTR) and SLA compliance, conducting periodic audits, reviewing and optimizing automated workflows, keeping the CMDB up to date, maintaining accurate Knowledge Base articles, and upgrading the ServiceNow platform to leverage new features and security patches.

---

## 2. Catalog / Service Catalog

**<a id="q3"></a>3. What are different types of Catalog Items?**
*   **Answer:** The main types include:
    *   **Catalog Item:** Standard request for goods or services (generates REQ, RITM, SCTASK).
    *   **Record Producer:** A user-friendly form on the portal that creates a task-based record like an Incident or Change Request instead of a Request.
    *   **Order Guide:** Groups multiple related Catalog Items into a single, guided user experience (e.g., New Employee Onboarding).
    *   **Content Item:** Provides information, links, or navigation rather than initiating a request.

**<a id="q4"></a>4. Difference between Order Guide, Record Producer, and Catalog Item**
*   **Answer:** 
    *   **Catalog Item:** Creates a hierarchical request structure (Request -> Request Item -> Catalog Task).
    *   **Record Producer:** Directly inserts a record into a specific task table (like `incident` or `problem`) mapping variables to fields. It does not use the REQ/RITM structure.
    *   **Order Guide:** A single interface that uses rules to present and submit multiple Catalog Items together under one Request.

**<a id="q5"></a>5. Can we use them in Workflow?**
*   **Answer:** 
    *   **Catalog Items & Order Guides:** Yes, they are intrinsically linked to Workflows (or Flow Designer Flows) that run on the Request Item (`sc_req_item`) table to manage approvals and task generation.
    *   **Record Producers:** They do not directly trigger Service Catalog workflows. Instead, they insert a record into a target table (e.g., Incident), and any Workflow or Flow configured to run on that target table will then trigger.

---

## 3. Flow Designer / Automation

**<a id="q6"></a>6. What is Flow Designer?**
*   **Answer:** Flow Designer is a non-scripting, natural language interface for automating business processes in ServiceNow. It uses "Triggers" (when to run) and "Actions" (what to do) to build automation seamlessly. It replaces traditional Workflows and enables process owners to build processes with minimal coding.

**<a id="q7"></a>7. Can we call Flow Designer from server-side scripting?**
*   **Answer:** Yes, you can trigger a Flow, Subflow, or Action from any server-side script (like Business Rules or Script Includes) using the `sn_fd.FlowAPI`. 
    *   Example: `sn_fd.FlowAPI.getRunner().flow('global.my_flow').withInputs(inputs).run();`

---

## 4. Client-Server Communication

**<a id="q8"></a>8. How can we send data from server side to client side? Different options in ServiceNow**
*   **Answer:** 
    *   **GlideAjax (Best Practice):** An asynchronous API used in Client Scripts to call a client-callable Script Include and return specific data without freezing the browser.
    *   **g_scratchpad & Display Business Rule:** A Display Business Rule runs before the form loads and places server data into the `g_scratchpad` object, which is then immediately available to `onLoad` or `onChange` Client Scripts.
    *   **getReference() with callback:** Fetches the entire record of a reference field. It is less efficient than GlideAjax if you only need a single field value.

**<a id="q9"></a>9. Can we use Query Business Rule instead of Display Business Rule?**
*   **Answer:** No, they serve completely different purposes. 
    *   A **Query Business Rule** runs *before* a database query is executed to restrict the records returned (row-level security, e.g., hiding VIP incidents from regular users). 
    *   A **Display Business Rule** runs just *before* a form is rendered to pass server-side variables to the client via `g_scratchpad`.

---

## 5. ACL / Security / Scripting

**<a id="q10"></a>10. What is Inherit checkbox?**
*   **Answer:** In the context of **UI Policies**, checking the "Inherit" checkbox applies the UI Policy not just to the current table, but also to all tables that extend it. For example, a UI Policy on the `task` table with Inherit checked will also run on the `incident` and `change_request` tables.

**<a id="q11"></a>11. Use of Isolate Script checkbox**
*   **Answer:** The "Isolate script" checkbox applies to Client Scripts and UI Policies. When checked (which is the default on modern releases), it prevents the script from accessing the browser DOM directly (e.g., using `document.getElementById` or jQuery). It enforces the use of standard `g_form` APIs, ensuring scripts remain upgrade-safe and compatible with the Service Portal and mobile apps.

**<a id="q12"></a>12. What is ACL and types of ACLs?**
*   **Answer:** **ACL (Access Control List)** rules restrict what data users can access and what actions they can perform (create, read, write, delete). To grant access, a user must pass the Role, Condition, and Script evaluations.
    *   **Types:** Table-level (restricts access to the entire record), Field-level (restricts access to specific fields on a record), UI Pages, Client Callable Script Includes, Processors, and REST Endpoints.

---

## 6. Script Includes / Reference Qualifier

**<a id="q13"></a>13. How many types of Script Includes do we have in ServiceNow?**
*   **Answer:** 
    *   **On-demand (Classless):** A script containing a single function, never instantiated, just called directly.
    *   **Class-based:** Defines a JavaScript class utilizing `Class.create()`.
    *   **Client-callable (Ajax):** Extends `AbstractAjaxProcessor` and can be called from client-side scripts via `GlideAjax`.

**<a id="q14"></a>14. Can we use Script Include in Reference Qualifier?**
*   **Answer:** Yes. In an **Advanced Reference Qualifier**, you can use a Script Include to dynamically return an encoded query string. Syntax: `javascript: new MyScriptInclude().myFunction()`.

**<a id="q15"></a>15. Types of Reference Qualifiers**
*   **Answer:** 
    *   **Simple:** Uses the standard condition builder to apply static filters (e.g., `active=true`).
    *   **Dynamic:** Uses a Dynamic Filter Option (e.g., "is (dynamic) Me").
    *   **Advanced:** Uses a JavaScript statement or Script Include to generate a dynamic encoded query string based on complex server-side logic.

---

## 7. Dictionary / Form / UI Configuration

**<a id="q16"></a>16. What is Dictionary Override?**
*   **Answer:** It allows you to override specific dictionary properties (like default value, reference qualifier, dependent field, or read-only status) for a specific extended table without altering the parent table's dictionary entry. For example, setting a different default "State" for Incidents versus Problems, even though both extend from Task.

**<a id="q17"></a>17. Remove Category, Assignment Group, Assigned To globally from Incident list view**
*   **Answer:** Navigate to the Incident list, right-click the column header, select **Configure > List Layout**, and remove those fields from the "Selected" slushbucket. To enforce this and prevent users from personalizing their lists to add them back, you would need to use **List Controls (Omit filters)** or define strict **ACLs** restricting read access to those fields in list context.

**<a id="q18"></a>18. When State = In Progress:**
*   Hide Resolution Information section
*   Make Configuration Item read-only
*   Make Description read-only
*   **Answer:** *(See implementation details in Question 21).*

**<a id="q19"></a>19. Should it be onLoad or onChange?**
*   **Answer:** It is best implemented as a **UI Policy**, which by default runs both `onLoad` and `onChange`. If you were to use a Client Script, you would need an `onChange` script on the State field, and potentially an `onLoad` script to ensure the logic applies when opening an existing record already in the "In Progress" state. 

**<a id="q20"></a>20. Why Configuration Item is not becoming read-only?**
*   **Answer:** If a UI Policy or Client Script is failing to make a field read-only, common reasons include:
    *   A higher-order UI Policy or a subsequent Client Script is reverting the field back to writable.
    *   The field has a Dictionary-level "Read only" attribute or Dictionary Override conflicting with the script.
    *   There is a UI Policy Script throwing a JavaScript error, preventing the rest of the policies from executing.
    *   (Rare) Admin override on forms, though UI Policies generally execute client-side regardless.

---

## 8. Client Scripts / UI Policies

**<a id="q21"></a>21. How to implement the above requirement using Client Script/UI Policy?**
*   **Answer:** **Using UI Policy (Best Practice):**
    1.  Create a new UI Policy on the Incident table.
    2.  Set Condition: `State` `is` `In Progress`.
    3.  Create UI Policy Actions:
        *   Field: `Configuration Item` [cmdb_ci] -> Read only: `True`.
        *   Field: `Description` [description] -> Read only: `True`.
    4.  Check the "Run scripts" checkbox.
    5.  In the **Execute if true** script: `g_form.setSectionDisplay('resolution_information', false);`
    6.  In the **Execute if false** script: `g_form.setSectionDisplay('resolution_information', true);`

---

## 9. Server-Side Questions

**<a id="q22"></a>22. Bulk update without triggering notifications and Business Rules**
*   **Answer:** Run a Background Script or Fix Script utilizing the `setWorkflow(false)` method on the GlideRecord. This disables Business Rules and engine-based events (which trigger notifications). Using `autoSysFields(false)` is also recommended to prevent altering the audit timestamps.
    ```javascript
    var gr = new GlideRecord('incident');
    gr.addEncodedQuery('YOUR_QUERY_HERE');
    gr.query();
    while (gr.next()) {
        gr.state = 6; // Example update
        gr.setWorkflow(false); // Disables BRs and Notifications
        gr.autoSysFields(false); // Disables sys_updated_on/by updates
        gr.update();
    }
    ```

**<a id="q23"></a>23. Priority field wrong → recalculate based on Impact & Urgency**
*   **Answer:** Priority is usually calculated via Data Lookup Rules. To fix existing records, run a Fix Script to "touch" the records. Updating the record with `setForceUpdate(true)` will re-trigger the Data Lookup rules.
    ```javascript
    var gr = new GlideRecord('incident');
    gr.addEncodedQuery('priority!=...YOUR_QUERY_HERE');
    gr.query();
    while(gr.next()) {
        gr.setForceUpdate(true);
        gr.update(); // Triggers engine rules to recalculate priority
    }
    ```

**<a id="q24"></a>24. SLA not applied due to misconfiguration → attach SLA manually**
*   **Answer:** Similar to Priority recalculation, after fixing the SLA configuration, you can use a Fix Script to "touch" the records that should have had the SLA attached. Updating the record will re-evaluate the SLA condition rules.
    ```javascript
    var gr = new GlideRecord('incident');
    gr.addQuery('sys_id', 'INCIDENT_SYS_ID');
    gr.query();
    if(gr.next()) {
        gr.setForceUpdate(true);
        gr.update(); // Triggers SLA evaluation
    }
    ```
    *Note: If retroactively applying SLAs, you may need to write a script to manually create `task_sla` records and calculate the start time to reflect the incident's true creation time, as touching the record will start the SLA from the current time.*

**<a id="q25"></a>25. Background Script**
*   **Answer:** Background Scripts (found under System Definition > Scripts - Background) allow administrators to execute server-side JavaScript on demand. They run with system administrator privileges and are used for data correction, mass updates, or testing script logic. Because they bypass UI and can bypass business logic (if scripted to do so), they are powerful but risky in production; Fix Scripts are generally preferred for trackable, repeatable execution.