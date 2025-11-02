# Bottlenecks

## 💡 Core Theses – Deep Insights and Real-World Anchors

### **1. “Bad code reviews are symptoms, not root causes.”**

**Meaning:**  
Toxic or broken reviews stem from unclear processes, lack of shared expectations, and weak psychological safety.

**Mechanism:**
- **Lazy reviews** → “LGTM” comments on unread code.
- **Mean reviews** → personal attacks instead of feedback.
- **Shape-shifting reviews** → code keeps changing mid-review.
- **Stringent reviews** → excessive bureaucracy without automation.

**Examples:**
1. A senior dev skims 40 PRs a week → critical bug slips through.  
2. Reviewer says “Do you even know async?” → new dev loses confidence.  
3. PR keeps changing every hour → reviewer fatigue and resentment.

**Lesson:** Fix the **system**, not the **symptom** — automate checks, set etiquette, and define review readiness.

---

### **2. “Bottlenecks kill trust and throughput.”**

**Meaning:**  
The “Single Senior Developer Reviewer” problem creates burnout, delays, and dependency.

**Mechanism:**
- Overreliance on one expert delays reviews.  
- Juniors never learn; team velocity drops.  

**Solutions:**
- Rotate reviewers; empower all devs to approve small PRs.  
- Safeguards: automated tests, CI/CD gates, and rollback mechanisms.  
- Encourage juniors to review as a learning exercise.  

**Real-world parallel:**  
> “If only one person can merge code, you don’t have a process — you have a single point of failure.”

---

### **3. “Preparation equals respect.”**

**Meaning:**  
Good reviews start with good pull requests. Unclear PRs waste everyone’s time.

**Mechanism:**
- Missing descriptions or unrelated changes confuse reviewers.  
- Oversized diffs delay feedback.

**Examples:**
- A 3,000-line PR combines refactoring + feature = impossible to review.  
- A PR without explanation = guesswork and frustration.

**Practices:**
- Limit PRs to ≤500 LOC or ≤30 minutes review time.  
- Use PR templates and validation bots.  
- Write meaningful titles: “Fix: Cache invalidation in BlobReader” > “Minor fix.”

---

### **4. “Discussion is valuable—but endless debate is waste.”**

**Meaning:**  
Asynchronous comment wars kill productivity and morale.

**Mechanism:**
- Text-only debates lack tone and empathy.  
- Async comments spiral into ego battles.

**Examples:**
- 47 comments debating variable naming.  
- Two engineers arguing over tab vs space for three days.

**Solutions:**
- Move to a 5-minute call after 2–3 comment rounds.  
- Summarize outcomes in PR comments for transparency.  
- Use “Conventional Comments” and MoSCoW categories to structure dialogue.

> 💬 *“Move the heat from text to talk — then document the peace.”*

---

### **5. “Big features must be split before they reach review.”**

**Meaning:**  
Oversized features reveal planning or design gaps — not just bad review discipline.

**Mechanism:**
- Poor decomposition leads to mega-PRs.  
- Reviewers can’t give meaningful feedback at scale.

**Examples:**
- “Implement billing system” PR touches 70 files.  
- Acceptance criteria missing → unclear scope.

**Best Practices:**
- Split by domain (UI, backend, API).  
- Use **feature flags** for incremental rollout.  
- Apply Git’s `cherry-pick` or `rebase` to create atomic PRs.  
- Discuss breakdown strategies during design, not review.

---

### **6. “A living process prevents loopholes.”**

**Meaning:**  
Even good review processes decay over time without maintenance.

**Mechanism:**
- Undefined workflows, outdated tools, or approval vanity metrics.  
- “Emergency merges” become normal.

**Examples:**
- Skipped reviews during hotfixes never documented.  
- Teams measure “PRs merged per week” instead of review quality.

**Solutions:**
- Maintain a **Team Working Agreement (TWA)**.  
- Audit automation and approval rules quarterly.  
- Introduce an **Emergency Playbook** for justified review bypasses.  
- Conduct post-mortems to ensure accountability.

**Leadership Connection:**  
Adaptive governance = clear rules + psychological trust. High-performing teams revisit both regularly.

---

## 🧠 Main Takeaways

1. **Code reviews are cultural mirrors** — not just technical gates.  
2. **Structure enables empathy** — automation frees humans for judgment.  
3. **Psychological safety drives feedback quality.**  
4. **Review processes need periodic tuning.**  
5. **Measure outcomes, not output** — value insights over velocity.

---

## 🧩 Real-World Scenarios

| Dilemma | Example | Remedy |
|----------|----------|--------|
| Lazy reviews | “LGTM” on unread PRs | Require review notes or checklist acknowledgment |
| Mean reviews | “Who wrote this mess?” | Enforce constructive tone and objective phrasing |
| Senior bottleneck | One reviewer for all PRs | Rotate reviewers; mentor juniors |
| Large PRs | 2,000+ LOC | Split by feature flags and submodules |
| Endless debate | Dozens of comments | Jump to call → summarize resolution |
| Process loopholes | Emergency merges | Use documented Emergency Playbook |
| Cultural burnout | “We hate PRs” attitude | Automate routine checks; celebrate great reviews |

---

## 🎯 Strategic and Leadership Implications

- **Leadership Principle:** A team’s communication quality defines its review quality.  
- **Strategic Insight:** Review processes are *organizational architecture* — they shape how information and trust flow.  
- **Decision-Making Link:** Dilemmas = trade-offs between speed, quality, and trust. High-performing teams make these trade-offs visible and revisited.

---

## 🧱 Example-Driven Practices

1. **Convert conflict to collaboration:**  
   “You forgot tests” → “Let’s add a test for X — here’s a pattern.”  

2. **Empower juniors early:**  
   Let new hires approve docs or tests to build confidence.  

3. **Turn reviews into learning rituals:**  
   Run a 30-min “PR Walkthrough Friday” for large PRs.  

4. **Use Emergency Playbooks:**  
   Skip review for critical Friday hotfix, then document post-mortem Monday.

---

## 💬 Integration with Complementary Insights

- **Trisha Gee:** Human reviewers should focus on *design, readability, maintainability*, not style or formatting — automate that.  
- **Tess Ferrandez-Norlander:** “Feedback is communication.” Be open to feedback, write reviewable PRs, settle style wars in a guide, and make small, self-contained PRs.  
- **Adrienne Tacke:** Code reviews are not just technical correctness checks — they are *cultural glue.*

---

## 🧭 Final Reflection

> **“Good teams review code. Great teams review how they review code.”**

Part 3 reminds us that the goal is not to make code perfect — it’s to make teams stronger. When feedback is respectful, processes are adaptive, and automation removes friction, code reviews evolve from a pain point into a *collective learning engine.*

---
