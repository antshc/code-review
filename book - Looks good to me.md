## Communication Qualities in Code Reviews

### 1. Use constructive tone and phrasing (“we” instead of “you”)

**Meaning:**
Replace personal or accusatory phrasing (“You forgot to handle nulls”) with collaborative, team-oriented phrasing (“Could we add a null check here?”). It signals shared ownership, reduces defensiveness, and promotes an inclusive learning culture. The tone shapes the team’s emotional safety and directly affects willingness to engage in reviews.

**Connection to real practice:**
Constructive tone supports long-term team trust. In distributed or asynchronous teams, written tone replaces body language — so phrasing *is* body language. Teams that consistently use inclusive language see higher participation in reviews and lower turnover of junior devs.

**Examples:**

1. ❌ “You didn’t follow the naming standard.” → ✅ “Can we align this name with our convention from the TWA?”
2. ❌ “This function is confusing.” → ✅ “We might make this function easier to follow by splitting the logic.”
3. ❌ “You should fix this test.” → ✅ “Could we pair on updating the test to clarify the intent?”

**Lesson learned:** Words drive psychological safety. Review tone determines whether developers perceive feedback as *a challenge* or *a collaboration*.

---

### 2. Apply structured feedback formats (Conventional Comments, MoSCoW)

**Meaning:**
Structure brings clarity and prioritization. Conventional Comments standardize tone (“nit:”, “suggestion:”, “question:”), while MoSCoW (“Must”, “Should”, “Could”, “Won’t”) communicates importance levels. Both prevent emotional misinterpretation and make responses easier to prioritize.

**Why comments are important:**
Code review comments are the main vehicle of knowledge transfer, mentorship, and quality alignment. They shape team culture, set expectations for future work, and record design decisions. Each comment contributes to the shared language and history of the codebase.

**What makes a comment effective:**

* Focused on code, not the coder.
* Clear about *what* and *why*, not just *how*.
* Respectful in tone and phrased collaboratively.
* Actionable, verifiable, and traceable.

**How to write effective comments:**

* Start with context (why it matters).
* State the suggestion succinctly.
* Offer reasoning or alternative examples.
* Use structured labels for clarity: `question:`, `suggestion:`, `nit:`.
* Apply MoSCoW categories for urgency and impact.

**5P Process for evaluating suggestions:**

<img width="320" height="280" alt="image" src="https://github.com/user-attachments/assets/0543dd72-89f5-40a9-9451-87c074b2e31d" />

1. **Purpose** – Does it align with the team or business goal?
2. **Principle** – Is it consistent with coding standards or architecture?
3. **Practicality** – Is it feasible to implement in scope or time?
4. **Performance** – Will it improve quality or efficiency?
5. **People** – Will it help the team learn or collaborate better?
   If at least three of these Ps are positive, the suggestion is valid to add.

**MMG Exchange (Meaning–Mechanism–Goal):**

Explanation: https://github.com/antshc/code-review/blob/main/MMG-Exchange-solve-conflicts.adoc

A framework for resolving conflicting “objective” views:

* *Meaning:* clarify what each developer interprets the issue to mean.
* *Mechanism:* explain how each solution works technically.
* *Goal:* restate the shared end goal.
  This ensures both sides can see logic rather than emotion, leading to mutual clarity.

**Comment signals & categories:**

* Use **MoSCoW** to prioritize: Must / Should / Could / Won’t.
* Apply **Conventional Comments** prefixes: `question:`, `nit:`, `suggestion:`, `praise:`.
* Combine them to form clear, ordered communication, e.g., `Must – suggestion:` or `Could – question:`.

**The Triple‑R pattern for requesting changes:**

Explanation: https://github.com/antshc/code-review/blob/main/Triple-R%20Pattern%20feedback.adoc

1. **Recognize** – Acknowledge what works well.
2. **Reason** – Explain why a change helps (context, risk, benefit).
3. **Request** – Make a specific, respectful ask for change.

**Examples:**

1. *Conventional Comment:* “**suggestion:** Could we extract this block to a helper for readability?”
2. *MoSCoW:* “**Must:** Add validation for negative values before merge. **Could:** Replace `List` with `HashSet` for faster lookup later.”
3. *Triple‑R example:* “Nice modular design! Since this loop is O(n²), consider caching results for performance.”

**Lesson learned:** Effective comments create clarity, empathy, and traceable action. Standardized phrasing and structured reasoning build predictability and help reviewers spend less mental energy deciphering tone and intent — increasing review throughput.

---

### 3. Include positive reinforcement for well-written code

**Meaning:**
Balance critique with appreciation. Acknowledge good structure, clear naming, and well-documented logic. Reinforcement encourages repetition of good patterns and fosters motivation, especially for junior or new contributors.

**Connection to real-world practice:**
Positive reinforcement turns code reviews into *learning moments*, not *judgments*. Teams that highlight good examples in PRs create “live style guides” — practical references of what “good” looks like in the project.

**Examples:**

1. “Great test coverage here — the edge case for null inputs is a good addition.”
2. “Love this use of `using` — this pattern reduces risk of leaks.”
3. “Nice refactor; smaller method makes intent clearer.”

**Lesson learned:** Praise is a multiplier. Reinforcing good practices makes reviewers *teachers* and authors *motivated learners*.

---

### 4. Avoid review anti-patterns: lazy, mean, shape-shifting, and stringent reviews

**Meaning:**
Bad review behaviors destroy trust and slow velocity:

* **Lazy:** “LGTM” with no context or review effort.
* **Mean:** Harsh or personal comments (“Did you even test this?”).
* **Shape-shifting:** Constantly changing PR scope, causing re-reviews.
* **Stringent:** Bureaucratic review processes with manual gates or micromanagement.

**Connection to practice:**
These patterns cause resentment and process fatigue. Preventing them is a leadership issue — requiring social norms (Team Working Agreement) and automation to remove repetitive checks.

**Examples:**

1. *Lazy:* Reviewer writes only “LGTM”. → **Fix:** Require brief rationale (“LGTM – ran tests locally and verified new config works”).
2. *Mean:* “This code is terrible.” → **Fix:** “The function is complex; could we extract smaller methods to improve readability?”
3. *Shape-shifting:* PR constantly updated during review. → **Fix:** Use draft PRs until ready and freeze scope once review starts.

**Lesson learned:** Consistency and empathy are productivity tools. Removing negative patterns saves time and morale.

---

### 5. Move to synchronous discussion after excessive back-and-forth

**Meaning:**
When PR discussions become long threads or circular arguments, shift to real-time conversation (chat, call, pair session). Written async feedback loses nuance and breeds misunderstanding.

**Connection to decision-making:**
Timely voice conversations speed resolution of design disagreements and preserve delivery velocity. Recording or summarizing outcomes in the PR keeps transparency and institutional memory.

**Examples:**

1. After 10+ comments about design choice, comment:
   “Let’s sync for 10 min to clarify context — I’ll summarize results in PR afterward.”
2. Two reviewers disagree → quick 3-way call resolves in minutes.
3. Large feature with multiple affected modules → schedule mini “mob review” session to walk through logic together.

**Lesson learned:** Async comments scale knowledge; sync talks resolve tension. The best teams balance both.

---

### 6. Summarize offline resolutions in PR comments for transparency

**Meaning:**
After an offline or voice discussion, add a summary comment of what was decided, why, and any next steps. This closes the loop and avoids “hidden” decisions that others can’t see.

**Connection to real-world collaboration:**
Summarizing outcomes improves traceability, reduces repeated questions, and teaches others. It also prevents “siloed” tribal knowledge — critical in regulated or multi-team environments.

**Examples:**

1. “Discussed with @Maria offline — we’ll keep this config local until next release; adding TODO in backlog.”
2. “Synced with reviewer: validation logic stays in service layer per design doc.”
3. “Outcome: no change required; doc updated to clarify naming convention.”

**Lesson learned:** Written closure is professional discipline. It transforms transient talk into durable team memory.

---

## Main Takeaways

| Principle              | Impact on Culture                          | Measurable Effect                |
| ---------------------- | ------------------------------------------ | -------------------------------- |
| Constructive phrasing  | Builds psychological safety                | Higher PR participation rate     |
| Structured feedback    | Makes review actionable and auditable      | Shorter review cycles            |
| Positive reinforcement | Increases motivation and learning          | Better code quality consistency  |
| Avoiding anti-patterns | Prevents review fatigue and resentment     | Reduced PR rejection rate        |
| Synchronous resolution | Speeds alignment and removes tone friction | Fewer re-openings or escalations |
| PR outcome summaries   | Ensures transparency and shared knowledge  | Fewer duplicate discussions      |

**Overall lesson:**

> *Effective communication is the backbone of effective code reviews.*
> It turns reviews from gatekeeping into mentorship, from friction into collaboration, and from opinion into shared decision-making.
