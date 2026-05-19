# Infosys - ServiceNow R1 Interview &#x2022; 19th May, 2026

### Questions

1. [What is CSM?](#1-what-is-csm)
2. [Core tables in CSM?](#2-core-tables-in-csm)
3. [How SLA gets attached in CSM Case?](#3-how-sla-gets-attached-in-csm-case)
4. [What is Service Offering?](#4-what-is-service-offering)
5. [How many Case Types are there OOB?](#5-how-many-case-types-are-there-oob)
6. [Difference between Incident and Problem?](#6-difference-between-incident-and-problem)
7. [Fundamentals/components of CSM?](#7-fundamentalscomponents-of-csm)
8. [Worked with Flow Designer?](#8-worked-with-flow-designer)
9. [Different types of triggers in Flow Designer?](#9-different-types-of-triggers-in-flow-designer)
10. [What are Flow Variables and their use?](#10-what-are-flow-variables-and-their-use)
11. [Recommended limit of Flow steps?](#11-recommended-limit-of-flow-steps)
12. [Have you created Catalog Items?](#12-have-you-created-catalog-items)
13. [Difference between Catalog Item and Record Producer?](#13-difference-between-catalog-item-and-record-producer)
14. [How to check active records in huge Incident table?](#14-how-to-check-active-records-in-huge-incident-table)
15. [Using GlideAggregate for active record check?](#15-using-glideaggregate-for-active-record-check)
16. [Types of Business Rules?](#16-types-of-business-rules)
17. [What is g_scratchpad?](#17-what-is-gscratchpad)
18. [What is GlideAjax?](#18-what-is-glideajax)
19. [Syntax of GlideAjax?](#19-syntax-of-glideajax)
20. [What is this GlideAjax code doing?](#20-what-is-this-glideajax-code-doing)
21. [Best practices for Server-side scripting?](#21-best-practices-for-server-side-scripting)
22. [Best practices for Client Scripts?](#22-best-practices-for-client-scripts)
23. [What is Database View?](#23-what-is-database-view)
24. [What is Major Incident?](#24-what-is-major-incident)
25. [Who can create Major Incident?](#25-who-can-create-major-incident)
26. [OOB who can create Major Incident?](#26-oob-who-can-create-major-incident)
27. [Worked with Change Request?](#27-worked-with-change-request)
28. [How Priority gets set using Impact and Urgency?](#28-how-priority-gets-set-using-impact-and-urgency)
29. [How would you gather requirements for Priority Matrix setup?](#29-how-would-you-gather-requirements-for-priority-matrix-setup)
30. [Who configures Priority Matrix?](#30-who-configures-priority-matrix)
31. [Steps to configure Priority Matrix?](#31-steps-to-configure-priority-matrix)
32. [What extra things are needed for custom table Priority setup?](#32-what-extra-things-are-needed-for-custom-table-priority-setup)


### Question's Answer

#### 1. What is CSM?
Customer Service Management (CSM) is a ServiceNow application that helps organizations manage customer support requests, resolve issues, and improve customer satisfaction by connecting customer service with other departments like engineering, operations, or finance.

#### 2. Core tables in CSM?
- Case (`sn_customerservice_case`)
- Consumer (`cmn_sec_users` / `sn_customerservice_consumer`)
- Account (`customer_account`)
- Contact (`customer_contact`)
- Product (`cmdb_model`)
- Asset (`alm_asset`)
- Entitlement (`service_entitlement`)
- Contract (`ast_contract`)

#### 3. How SLA gets attached in CSM Case?
SLAs in CSM cases are attached based on SLA Definition rules defined on the Case table. These definitions specify start, pause, and stop conditions. When a Case is created or updated, the SLA engine evaluates these conditions. If the start condition is met and no other stop/cancel conditions are true, the SLA is attached. Entitlements and Contracts can also play a role in determining which SLA is applied.

#### 4. What is Service Offering?
A Service Offering is a specific variation of a Service that defines a specific level of service for a specific price. It includes details like service commitments, SLAs, pricing, and the specific catalog items available to the user. It is part of the Service Portfolio Management.

#### 5. How many Case Types are there OOB?
OOB, CSM provides various case types such as Product Support, Order, and generally categorizes cases into B2B (Business-to-Business, using Accounts and Contacts) and B2C (Business-to-Consumer, using Consumers).

#### 6. Difference between Incident and Problem?
- **Incident**: An unplanned interruption to an IT service or a reduction in the quality of an IT service. The goal is to restore normal service operation as quickly as possible.
- **Problem**: A cause of one or more incidents. The goal of Problem Management is to investigate the root cause of incidents and prevent them from happening again or minimize their impact.

#### 7. Fundamentals/components of CSM?
Key components include:
- Case Management
- Accounts and Contacts (B2B)
- Consumers (B2C)
- Service Entitlements and Contracts
- Product and Asset Management
- Omni-channel communication (Portal, Chat, Email, Phone)
- Knowledge Management integration
- Communities
- Field Service Management (often integrated)

#### 8. Worked with Flow Designer?
*(Assuming a generic "Yes" for the answer context)* Yes, I have worked with Flow Designer. It is a non-technical interface for building and enabling process automation capabilities, allowing users to automate approvals, tasks, notifications, and record operations without writing complex code.

#### 9. Different types of triggers in Flow Designer?
- **Record-based triggers**: Created, Updated, Created or Updated.
- **Date/Time-based triggers**: Daily, Weekly, Monthly, Once, Run at specific time.
- **Application-based triggers**: Inbound Email, Service Catalog, REST API (Webhook), SLA Task.

#### 10. What are Flow Variables and their use?
Flow variables are temporary storage elements defined within a Flow that allow you to store and pass data between different actions or steps within the same Flow. They are useful for storing calculated values, counters, or flags that need to be referenced later in the flow's execution.

#### 11. Recommended limit of Flow steps?
ServiceNow generally recommends keeping flows modular and manageable. While there isn't a strict hard limit that stops execution at a low number, best practice suggests keeping it under 50 actions to maintain readability, performance, and ease of troubleshooting. For complex logic, it's recommended to use Subflows.

#### 12. Have you created Catalog Items?
*(Assuming a generic "Yes")* Yes, I have created Catalog Items. These are the goods or services available for request in the Service Catalog. They require defining variables, UI Policies, Client Scripts, and an execution plan or workflow/Flow Designer flow for fulfillment.

#### 13. Difference between Catalog Item and Record Producer?
- **Catalog Item**: Used to request goods or services (e.g., a new laptop). It typically results in a Request (REQ), Requested Item (RITM), and Catalog Tasks (SCTASK). It uses Workflows or Flows for fulfillment.
- **Record Producer**: A specific type of catalog item that allows users to create task-based records (like an Incident, Change, or custom table record) from the Service Portal. It maps user inputs directly to fields on the target record.

#### 14. How to check active records in huge Incident table?
You can use `GlideAggregate` for counting records efficiently. For querying specific records, use `GlideRecord` with `setLimit()` or iterate using `next()` carefully. Database views or reporting can also be used. To just get a count, `GlideAggregate` is the best approach.

#### 15. Using GlideAggregate for active record check?
```javascript
var count = new GlideAggregate('incident');
count.addQuery('active', true);
count.addAggregate('COUNT');
count.query();
if (count.next()) {
    gs.info('Active Incidents: ' + count.getAggregate('COUNT'));
}
```

#### 16. Types of Business Rules?
- **Before**: Execute before the record is saved to the database.
- **After**: Execute after the record is saved to the database.
- **Async**: Execute asynchronously (in the background) after the record is saved.
- **Display**: Execute before the form is presented to the user, used to pass data from server to client via `g_scratchpad`.

#### 17. What is g_scratchpad?
`g_scratchpad` is an object used to pass data from the server (using a Display Business Rule) to the client (using Client Scripts) when a form loads. This avoids synchronous GlideAjax calls on form load.

#### 18. What is GlideAjax?
`GlideAjax` is an API used in Client Scripts to make asynchronous calls to the server to execute server-side code (Script Includes) and return data to the client without reloading the page.

#### 19. Syntax of GlideAjax?
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

#### 20. What is this GlideAjax code doing?
*(Since the specific code isn't provided, this is a general explanation)* The code initializes a call to a specific Script Include, passes the function name to execute via `sysparm_name`, passes any additional parameters, and then asynchronously waits for the response. Once the server returns data, the callback function is executed to process that data on the client side (e.g., populating a field).

#### 21. Best practices for Server-side scripting?
- Use `GlideAggregate` instead of `GlideRecord` for counting.
- Avoid hardcoding sys_ids; use System Properties.
- Keep Business Rules lightweight and use Script Includes for complex logic.
- Avoid `current.update()` in Before Business Rules.
- Use asynchronous execution (Async Business Rules or Events) when immediate response is not required.
- Add descriptive comments and use meaningful variable names.

#### 22. Best practices for Client Scripts?
- Use asynchronous GlideAjax (`getXMLAnswer`) instead of synchronous `getReference` or synchronous GlideAjax.
- Minimize server calls.
- Use UI Policies instead of Client Scripts for simple field visibility/read-only/mandatory changes.
- Avoid global client scripts.
- Check for `isLoading` at the start of `onLoad` and `onChange` scripts to prevent unwanted execution.

#### 23. What is Database View?
A Database View defines a table join for reporting purposes. It allows you to query data from multiple tables as if they were a single table. It is read-only and primarily used when you need to report on data that spans across related tables (e.g., Incidents and their associated SLAs).

#### 24. What is Major Incident?
A Major Incident is an incident that has a high impact and high urgency, causing significant disruption to the business. It requires a coordinated, swift response, often involving a dedicated Major Incident Management team, special communication plans, and specific resolution processes.

#### 25. Who can create Major Incident?
Typically, Major Incident Managers, IT Service Desk Managers, or sometimes designated L2/L3 support agents can propose or promote an incident to a Major Incident.

#### 26. OOB who can create Major Incident?
OOB, users with the `major_incident_manager` role can promote a regular incident to a Major Incident or create a new Major Incident directly. ITIL users can typically propose a Major Incident, which then needs approval/promotion by a Major Incident Manager.

#### 27. Worked with Change Request?
*(Assuming a generic "Yes")* Yes, I have worked with Change Requests. Change Management involves standard, normal, and emergency changes. It includes processes for risk assessment, conflict detection, approvals (CAB), and implementation task generation to ensure changes to the IT environment are controlled and minimize risk.

#### 28. How Priority gets set using Impact and Urgency?
Priority is automatically calculated based on a Priority Data Lookup matrix (Priority Matrix). When a user selects the Impact and Urgency on a task (like Incident), the system cross-references these values in the "Data Lookup Definitions" rules to automatically populate the Priority field.

#### 29. How would you gather requirements for Priority Matrix setup?
I would conduct workshops with key stakeholders (Service Desk managers, IT directors, business unit owners). I'd ask them to define levels of business impact (e.g., number of users affected, financial loss) and levels of urgency (how quickly the business needs it fixed). Then, map combinations of these to define what constitutes a P1 (Critical), P2 (High), etc., agreeing on the SLAs associated with each priority.

#### 30. Who configures Priority Matrix?
System Administrators or users with the `admin` role or specific configuration roles (like `data_lookup_admin` or specific application admin roles) can configure the Priority Matrix.

#### 31. Steps to configure Priority Matrix?
1. Navigate to **System Policy > Rules > Priority Data Lookups** (or Data Lookup Definitions).
2. Open the record for the relevant table (e.g., Incident).
3. In the related list "Matcher Field Definitions", ensure Impact and Urgency are matcher fields.
4. In the "Setter Field Definitions", ensure Priority is the setter field.
5. In the "Data Lookup Definition" related list (or the actual lookup table like `dl_u_priority`), add or modify rows defining the Matrix (e.g., Impact = 1, Urgency = 1 -> Priority = 1).

#### 32. What extra things are needed for custom table Priority setup?
For a custom table:
1. Ensure the custom table has `impact`, `urgency`, and `priority` fields (usually inherited if extended from Task).
2. Create a new Data Lookup Definition for the custom table.
3. Define the Matcher fields (Impact, Urgency).
4. Define the Setter field (Priority).
5. Create a dedicated lookup table (or use an existing one if applicable, though usually a specific one is better if rules differ) to hold the matrix values, or populate the generic data lookup table referencing your custom table.
6. Ensure the fields are on the form and dictionary overrides are set up if needed for default values or choices.