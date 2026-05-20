# Master Study Guide: All Questions by Topic

> **Navigation Menu (Sidebar Equivalent)**: Click on any topic or question to jump directly to its answer.

## Table of Contents

* [1. Client Scripts & UI Policies](#1-client-scripts--ui-policies)
  * [Q1. Have you written Client Script? There is a checkbox named Global?](#q1)
  * [Q2. What is All Views?](#q2)
  * [Q3. What all functions/methods can you use in onChange Client Script?](#q3)
  * [Q4. OnChange method 5 parameters?](#q4)
  * [Q5. If isTemplate = true, what will happen?](#q5)
  * [Q6. UI Policy vs Data Policy? Can we write scripts in them?](#q6)
  * [Q7. When does onChange and onLoad run?](#q7)
* [2. Client-Server Communication](#2-client-server-communication)
  * [Q8. How can we send data from server side to client side?](#q8)
  * [Q9. What is g_scratchpad?](#q9)
  * [Q10. What is GlideAjax? Syntax?](#q10)
* [3. Server-Side Scripting](#3-server-side-scripting)
  * [Q11. Difference between After and Async Business Rule?](#q11)
  * [Q12. How to prevent a Business Rule from re-triggering?](#q12)
  * [Q13. Types of Business Rules?](#q13)
  * [Q14. How to check active records in huge Incident table? (GlideAggregate)](#q14)
  * [Q15. Fix Script vs Background Script](#q15)
  * [Q16. Bulk update without triggering notifications and BRs?](#q16)
* [4. Integrations & API](#4-integrations--api)
  * [Q17. What type of integrations have you worked on? (Jira, etc.)](#q17)
  * [Q18. Main difference between Basic Authentication and OAuth?](#q18)
  * [Q19. Steps for Jira integration / Updating an Incident via REST?](#q19)
  * [Q20. Client needs one Knowledge Base API returning both details and attachments. How?](#q20)
* [5. ITSM (Incident, Problem, Change)](#5-itsm-incident-problem-change)
  * [Q21. Difference between Incident and Problem?](#q21)
  * [Q22. What is a Major Incident and who can create it?](#q22)
  * [Q23. Parent-Child Incident — explain.](#q23)
  * [Q24. Priority field wrong → recalculate based on Impact & Urgency?](#q24)
* [6. Catalog & Flow Designer](#6-catalog--flow-designer)
  * [Q25. Difference between Catalog Item, Record Producer, and Order Guide?](#q25)
  * [Q26. What is Flow Designer and its trigger types?](#q26)
  * [Q27. Catalog Item: Block HR users from 'requested_for' variable?](#q27)
* [7. CSM, CMDB & Other Modules](#7-csm-cmdb--other-modules)
  * [Q28. What is CSM? Core tables in CSM?](#q28)
  * [Q29. How SLA gets attached in CSM Case?](#q29)
  * [Q30. CMDB exposure (IRE, Classes, Connectors)?](#q30)
* [8. Transform Maps](#8-transform-maps)
  * [Q31. Concept of Transform Map scripts — onStart, onBefore, etc.](#q31)
  * [Q32. I have one Excel with 10 records. How many times will scripts run?](#q32)

---

## Answers Block

### 1. Client Scripts & UI Policies

**<a id="q1"></a>Q1. Have you written Client Script? There is a checkbox named Global?**
* **Answer:** Yes. The Global checkbox indicates that the script will run on all form views. If unchecked, you must specify a single 'View' (like Default, Self Service).

**<a id="q2"></a>Q2. What is All Views?**
* **Answer:** This directly relates to the "Global" checkbox. When "Global" is checked, it means "All Views". The script executes regardless of the view selected.

**<a id="q3"></a>Q3. What all functions/methods can you use in onChange Client Script?**
* **Answer:** `g_form` API (`getValue`, `setValue`, `setMandatory`, `addInfoMessage`), `g_user` API (to check roles), and `GlideAjax` for asynchronous server calls.

**<a id="q4"></a>Q4. OnChange method 5 parameters?**
* **Answer:** `control`, `oldValue`, `newValue`, `isLoading`, and `isTemplate`.

**<a id="q5"></a>Q5. If isTemplate = true, what will happen?**
* **Answer:** `isTemplate` is true when a field value changes because a user applied a Template. We use `if (isLoading || isTemplate) { return; }` to prevent heavy scripts from running during mass template changes.

**<a id="q6"></a>Q6. UI Policy vs Data Policy? Can we write scripts in them?**
* **Answer:** **UI Policies** are client-side (visible, read-only, mandatory on forms) and CAN have scripts (Execute if True/False). **Data Policies** are server-side (enforce mandatory/read-only at DB level for imports/lists) and CANNOT have scripts.

**<a id="q7"></a>Q7. When does onChange and onLoad run?**
* **Answer:** `onLoad` runs when a form is first rendered. `onChange` runs immediately when a user modifies a field and moves focus away.

### 2. Client-Server Communication

**<a id="q8"></a>Q8. How can we send data from server side to client side?**
* **Answer:** GlideAjax (best practice, asynchronous), `g_scratchpad` via Display Business Rules (on load), and `getReference()` with a callback (less efficient).

**<a id="q9"></a>Q9. What is g_scratchpad?**
* **Answer:** An object used to pass data from the server (using a Display Business Rule) to the client (`onLoad` Client Scripts) instantly when a form loads.

**<a id="q10"></a>Q10. What is GlideAjax? Syntax?**
* **Answer:** An API used in Client Scripts to make asynchronous calls to a client-callable Script Include.
```javascript
var ga = new GlideAjax('ScriptIncludeName');
ga.addParam('sysparm_name', 'functionName');
ga.addParam('sysparm_myParam', 'value');
ga.getXMLAnswer(function(response) { console.log(response); });
```

### 3. Server-Side Scripting

**<a id="q11"></a>Q11. Difference between After and Async Business Rule?**
* **Answer:** **After** runs synchronously immediately after DB update, making the user wait. **Async** runs in the background via the scheduler queue, returning UI control instantly (used for heavy tasks/integrations).

**<a id="q12"></a>Q12. How to prevent a Business Rule from re-triggering?**
* **Answer:** Use `current.setWorkflow(false);` before an update to prevent other BRs and notifications from running, avoiding infinite loops.

**<a id="q13"></a>Q13. Types of Business Rules?**
* **Answer:** Before, After, Async, and Display.

**<a id="q14"></a>Q14. How to check active records in huge Incident table?**
* **Answer:** Do not use GlideRecord `getRowCount()`. Use **GlideAggregate**:
```javascript
var count = new GlideAggregate('incident');
count.addQuery('active', true);
count.addAggregate('COUNT');
count.query();
```

**<a id="q15"></a>Q15. Fix Script vs Background Script**
* **Answer:** Background Scripts are ad-hoc, run immediately, and are NOT captured in Update Sets. Fix Scripts are designed to be captured in Update Sets and migrated across environments.

**<a id="q16"></a>Q16. Bulk update without triggering notifications and BRs?**
* **Answer:** Run a Fix Script using `gr.setWorkflow(false);` to disable BRs/notifications, and `gr.autoSysFields(false);` to prevent changing audit timestamps.

### 4. Integrations & API

**<a id="q17"></a>Q17. What type of integrations have you worked on? (Jira, etc.)**
* **Answer:** Both Inbound (Scripted REST APIs) and Outbound (REST Messages, IntegrationHub) connecting with Jira, Workday, and Active Directory.

**<a id="q18"></a>Q18. Main difference between Basic Authentication and OAuth?**
* **Answer:** Basic Auth sends username/password directly. OAuth uses temporary, scoped Access Tokens, which is much more secure as credentials aren't shared and tokens can be revoked.

**<a id="q19"></a>Q19. Steps for Jira integration / Updating an Incident via REST?**
* **Answer:**
1. Setup Jira API Token / OAuth Profile.
2. Create Outbound REST Message (HTTP POST/PUT).
3. Create an Async Business Rule triggered on Incident update.
4. Call a Script Include that uses `sn_ws.RESTMessageV2`, passes variables (`current.number`), and executes the call.

**<a id="q20"></a>Q20. Client needs one Knowledge Base API returning both details and attachments. How?**
* **Answer:** Create a Custom Scripted REST API. Query `kb_knowledge` for details, then query `sys_attachment` for the related file. Use `GlideSysAttachment().getContentBase64()` to get the file, combine both into one JSON, and return.

### 5. ITSM (Incident, Problem, Change)

**<a id="q21"></a>Q21. Difference between Incident and Problem?**
* **Answer:** **Incident** is an unplanned disruption; the goal is to restore service instantly. **Problem** is the underlying root cause of one or more incidents; the goal is to find a permanent fix.

**<a id="q22"></a>Q22. What is a Major Incident and who can create it?**
* **Answer:** High impact/urgency incident causing major disruption. OOB, users with the `major_incident_manager` role can promote or create them.

**<a id="q23"></a>Q23. Parent-Child Incident — explain.**
* **Answer:** Multiple incidents caused by the same issue are linked to a Parent. Updating/resolving the Parent automatically cascades those updates down to all Child incidents.

**<a id="q24"></a>Q24. Priority field wrong → recalculate based on Impact & Urgency?**
* **Answer:** Run a Fix Script that updates the records using `gr.setForceUpdate(true);`. This forces the Data Lookup rules to re-evaluate and set the correct priority.

### 6. Catalog & Flow Designer

**<a id="q25"></a>Q25. Difference between Catalog Item, Record Producer, and Order Guide?**
* **Answer:** **Catalog Item** creates a REQ/RITM/SCTASK hierarchy. **Record Producer** directly creates a task record (like an Incident) without the REQ structure. **Order Guide** groups multiple catalog items into one form.

**<a id="q26"></a>Q26. What is Flow Designer and its trigger types?**
* **Answer:** A natural language automation tool. Triggers include Record-based (Created/Updated), Date/Time-based (Daily/Weekly), and Application-based (Service Catalog, Inbound Email).

**<a id="q27"></a>Q27. Catalog Item: Block HR users from 'requested_for' variable?**
* **Answer:** Use an **Advanced Reference Qualifier** on the `requested_for` variable. Set the Reference Qual script to exclude the HR department (e.g., `javascript: new UserUtils().getNonHR();`).

### 7. CSM, CMDB & Other Modules

**<a id="q28"></a>Q28. What is CSM? Core tables in CSM?**
* **Answer:** Customer Service Management helps manage external customer support. Core tables: Case, Consumer, Account, Contact, Product, Asset, Entitlement, Contract.

**<a id="q29"></a>Q29. How SLA gets attached in CSM Case?**
* **Answer:** Via SLA Definitions on the Case table. The SLA engine evaluates start/pause/stop conditions. Entitlements and Contracts also influence which SLA is applied.

**<a id="q30"></a>Q30. CMDB exposure (IRE, Classes, Connectors)?**
* **Answer:** Involved in creating CI Classes, configuring the CI Class Manager, building Identification and Reconciliation engine (IRE) rules to prevent duplicates, and mapping data via Service Graph Connectors.

### 8. Transform Maps

**<a id="q31"></a>Q31. Concept of Transform Map scripts — onStart, onBefore, etc.**
* **Answer:** `onStart` (runs once before import starts), `onBefore` (runs before a specific row is inserted - used for row validation), `onAfter` (runs after row insertion), `onComplete` (runs once at the end).

**<a id="q32"></a>Q32. I have one Excel with 10 records. How many times will scripts run?**
* **Answer:** `onStart`: 1 time. `onBefore`: 10 times. `onAfter`: 10 times. `onComplete`: 1 time.
