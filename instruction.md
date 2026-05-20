# Company Name - ServiceNow Round Interview • Date

This template defines the standard format that all interview questions and answers markdown files (excluding `README.md`) must follow.

**Important Rules:** 
1. When adding new questions to a file, you MUST also provide and format the corresponding technical answers in the "Answers Block" section. Do not leave the answers blank.
2. Whenever a new interview file is added, you MUST update `README.md` to include a link to the new file in the table, keeping the rows sorted chronologically by Date.

---

## Template Structure

### 1. File Naming Nomenclature
The file name must follow this strict format: `CompanyName_Round_Date.md` (e.g., `BCEGlobalTech_R1_25_04_26.md`).
- Use underscores instead of spaces.
- The date should typically be in `DD_MM_YY` or `DD_Month_YYYY` format.

### 2. Document Title
The document must start with a level 1 heading containing the company name, round, and interview date.
```markdown
# [Company Name] - ServiceNow [Round] Interview • [Date]
```

### 2. Questions List (Top Section)
- Contains a `### Questions` header followed by a horizontal rule `---`.
- Grouped by topics/categories under Level 2 headings (`## 1. Category Name`).
- Categories must be separated by horizontal rules `---`.
- Each question must be listed as a numbered item with a markdown anchor link pointing to its answer (`#q{number}`).
- Question numbers must start at 1 and run sequentially through the entire list across all categories.

Example:
```markdown
### Questions
---

## 1. ITSM

1. [What is the difference between Incident and Problem?](#q1)
2. [Explain the Incident lifecycle.](#q2)

---

## 2. Service Catalog

3. [What is a Record Producer?](#q3)
```

### 3. Answers Block (Bottom Section)
- Prefaced by a `### Question's Answer` header.
- Answers are grouped under the exact same Level 2 category headings used in the Questions list.
- Each answer is separated by horizontal rules `---` between categories.
- Answers must be formatted with:
  - An HTML anchor tag `<a id="q{number}"></a>` before the question text.
  - The question text bolded (`**`).
  - An bulleted answer block starting with `*   **Answer:**`.
  - Code blocks wrapped in three backticks (` ```javascript `) where applicable.

Example:
```markdown
### Question's Answer

## 1. ITSM

**<a id="q1"></a>1. What is the difference between Incident and Problem?**
*   **Answer:** 
    *   **Incident:** A sudden disruption to an IT service.
    *   **Problem:** The underlying root cause of one or more incidents.

**<a id="q2"></a>2. Explain the Incident lifecycle.**
*   **Answer:** The lifecycle includes New, In Progress, On Hold, Resolved, Closed, and Canceled.

---

## 2. Service Catalog

**<a id="q3"></a>3. What is a Record Producer?**
*   **Answer:** A client-facing form that creates a record (e.g., an Incident) on a target table.
```

---

## Category Conventions
When creating categories, try to map questions into these standard ServiceNow topics:
1. **ITSM** (Incident, Problem, Change)
2. **CSM** (Customer Service Management)
3. **Catalog / Service Catalog**
4. **Flow Designer / Automation**
5. **Client-Server Communication** (GlideAjax, g_scratchpad)
6. **Client Scripts / UI Policies**
7. **Server-Side Questions / Scripting** (Business Rules, Script Includes)
8. **Database Views & Reporting**
9. **Priority Matrix & Data Lookups** (or Dictionary / Form Configuration)
