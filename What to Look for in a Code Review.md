# 🧩 What to Look for in a Code Review — Summary (Trisha Gee, JetBrains)

> _“Automate the trivial; humans review the meaningful.”_

---

## 🧭 Executive Summary

**Central theme:**  
Trisha Gee’s *What to Look for in a Code Review* outlines how to conduct effective, high-value code reviews that go beyond syntax and style checking. It teaches reviewers to focus on **design quality, correctness, readability, maintainability, and communication**. The book emphasizes that code reviews are not just about catching bugs—they’re about **collaboration, learning, and building collective code ownership**.

**Key insights:**
- Let automation handle formatting and static checks; human reviewers focus on design and intent.  
- The purpose of a code review is to ensure that new code fits well with the overall architecture and evolves the system in the right direction.  
- Tests are the most valuable documentation—reviewers should assess their coverage, clarity, and intent.  
- Reviews are a form of communication: clear comments and mutual respect matter as much as technical accuracy.  
- A good review culture fosters knowledge sharing, reduces risk, and builds trust across teams.

**Real-world connection:**  
Modern teams practicing DevOps and CI/CD rely on fast, iterative reviews. Effective reviews catch systemic issues, promote maintainable design, and reduce future debugging costs. Gee’s framework helps developers and leads focus their energy where human judgment matters most.

---

## 💡 Core Theses – Deep Insights and Real-World Anchors

### 1. **“Automate the trivial; humans review the meaningful.”**
**Meaning:**  
Style, indentation, and formatting should be handled by linters and IDE inspections. Human effort should focus on deeper insights like architecture, intent, and risk.

**Examples:**
- Let JetBrains inspections or ESLint catch style issues automatically.  
- Discuss whether a service boundary is correct, not whether a brace is misplaced.  
- A team that automates the mechanical frees reviewers for architectural critique.

---

### 2. **“Design consistency is the soul of maintainable code.”**
**Meaning:**  
Check whether new code aligns with architecture and design principles (SOLID, DDD). Detect duplication, misplaced logic, or over-engineering.

**Examples:**
- Ensure a new “OrderService” doesn’t contain customer logic.  
- Identify abstractions that were added “just in case” (YAGNI).  
- Promote gradual migration toward modern patterns, not legacy ones.

---

### 3. **“Readable code is reviewable code.”**
**Meaning:**  
If reviewers struggle to read code, they can’t verify correctness. Naming, intent, and structure matter more than clever one-liners.

**Examples:**
- Rename `procData()` → `calculateInvoiceTotals()`.  
- Simplify nested conditions for clarity.  
- Rewrite cryptic tests so future developers instantly grasp their purpose.

---

### 4. **“Tests are living documentation, not afterthoughts.”**
**Meaning:**  
A review should validate test intent, coverage, and readability. Tests describe business logic as much as they verify it.

**Examples:**
- Confirm coverage of both happy paths and failure scenarios.  
- Ensure tests explain *why* a behavior exists.  
- Encourage tests that document system limits or intentional constraints.

---

### 5. **“Ask the ‘What if?’ questions—spot the unseen risks.”**
**Meaning:**  
Reviewers provide system-level awareness. They should question how code behaves under pressure, at scale, or in failure scenarios.

**Examples:**
- “What happens if the network call fails halfway?”  
- “Could this log line leak sensitive data?”  
- “Does this dependency version have known vulnerabilities?”

---

### 6. **“Code reviews are collective learning, not individual judgment.”**
**Meaning:**  
Reviews spread knowledge, align mental models, and build shared ownership. The goal is understanding, not policing.

**Examples:**
- Reviewers learn new libraries or APIs from others’ PRs.  
- Encourage authors to document reasoning directly in code or PR descriptions.  
- Use discussions to mentor juniors and capture tribal knowledge.

---

## ⚙️ Easy-Recall Section — Best Practices & Rules of Thumb

### ✅ Do
- Automate formatting and style enforcement.  
- Focus human reviews on design, maintainability, and correctness.  
- Treat tests as documentation—read them closely.  
- Ask open questions to reveal reasoning (“Why was this pattern chosen?”).  
- Share feedback constructively and with context.  
- Encourage small, atomic PRs for fast iteration.

### 🚫 Don’t
- Nitpick formatting or personal preferences.  
- Use reviews to assert authority or assign blame.  
- Approve large, unclear PRs just to move faster.  
- Ignore missing or unclear tests.  
- Skip security and performance considerations.  

### ⚖️ Rules of Thumb
| Rule | Description |
|------|--------------|
| **30-Minute Rule** | A PR should be reviewable within 30 minutes; split if longer. |
| **Explain the Why** | Every change should tell a clear story—what and why. |
| **Test Triangle** | Unit → Integration → Edge cases—check all levels. |
| **One Comment = One Action** | Keep feedback specific and actionable. |
| **Human over Tool** | Tools enforce syntax; humans ensure empathy and intent. |

---

## 🕓 Key Points (Chronological Highlights)

1. **Introduction:**  
   - Code reviews are essential but often misunderstood.  
   - Tools help with mechanics; people ensure design coherence.

2. **Design Review:**  
   - Evaluate architectural fit, SOLID adherence, and dependency management.  
   - Encourage reuse and prevent unnecessary complexity.

3. **Readability & Maintainability:**  
   - Code and tests must communicate intent.  
   - Names, structure, and clarity reduce long-term cost.

4. **Functionality:**  
   - Validate logic correctness and edge-case handling.  
   - Ensure the code meets the explicit requirements.

5. **Tests:**  
   - Confirm adequate test coverage and clarity.  
   - Review tests for missing cases and documentation value.

6. **Performance & Security:**  
   - Detect inefficient resource use or potential vulnerabilities early.

7. **Data Structures & Principles:**  
   - Encourage appropriate structure selection and adherence to SOLID.

8. **Outcome:**  
   - Effective reviews create shared understanding, fewer defects, and more maintainable systems.

---

## 🧩 Closing Insight

> “A great code review isn’t about proving someone wrong—it’s about making the code, the team, and the product better.”

Code reviews, done right, are one of the most powerful tools for **quality, collaboration, and learning**.  
They are less about *approval* and more about *alignment*—between people, practices, and the evolving system.
