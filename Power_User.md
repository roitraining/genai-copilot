

# Copilot for Power Users — Advanced Prompting and Agents

## Student Demo Handout



### **How to use this handout**

This handout contains every prompt that will be demoed during the session. Copy any prompt below and paste it into Copilot to follow along. Each demo lists:

* The file (if any) you'll need to attach when running the prompt
* A short description of what the demo shows
* The prompt itself, in a gray box, you can copy directly

Files referenced in this handout will be distributed separately. The 📎 callout box at the top of each demo tells you which file to attach. Demos without a callout don't need a file. Some demos read directly from Outlook or run inside an agent — those are flagged with an ℹ note instead.

A reminder on model choice: these prompts ask Copilot to do more complex reasoning, so use a reasoning ("Think Deeper" / slower) model rather than a quick-response model. The quick models will generally not produce reliable results here.

## **Part 1 — From One-Off Prompts to Sequenced Workflows**

### **Demo 1 — Vending machine vs. a sequenced chain**

Two ways to approach the same goal — getting up to speed on the private credit market. Run the casual one-shot first so you can see the generic "vending machine" result, then run the two-step sequenced version where each step's output is handed to the next.

***The casual one-shot version (run this first)***

```
Search the web and tell me about the current state of the private credit market.
```

***Step 1 — Identify the right questions first***

```
I want to get up to speed on the private credit market. Search the web for current, reliable information on it.

Before writing any explanation, work out the key questions someone new to this topic needs answered to genuinely understand it, the things that actually matter, in an order that builds understanding. Give me that list of questions, and for each one a short note on why it matters. Cite the sources you draw on.

Don't answer the questions yet, just identify the right ones.
```

***Step 2 — Use those questions as the structure for a briefing***

```
Now use the questions you laid out in the previous step as the structure for a briefing.

Search the web again where you need current detail, and write a one-page, plain-language briefing that answers each of those questions in turn. Lead with the single most important thing someone should understand first, keep the language accessible to a non-specialist, and cite your sources.

Stick to the questions you already identified, don't introduce new ones or wander off into unrelated detail.
```

## **Part 2 — Advanced Prompting & Verification (Word & Outlook)**

### **Demo 2 — Persona + self-critique (compliance review)**

| 📎 File required: Sample_Compliance_Disclosure_DRAFT.docx |
| :---- |

First run the casual version to see the baseline. Then run the power-user version, which adds a persona and a sharply defined job. Finally run the self-check pass, which makes the model re-test each of its own findings against the actual document text — self-critique anchored to an external source.

***The casual version***

```
Review this document and tell me if there's anything wrong with it.
```

***The power-user version (persona + defined job)***

```
## Persona
Act as a senior compliance analyst at an alternative-investment manager with deep experience reviewing investor-facing disclosures for regulatory exposure. You are known for being precise, conservative, and for flagging issues clearly rather than rewriting around them.

## Goal
Review the attached draft for regulatory and reputational gaps before it goes to a human compliance reviewer. You are the first pass, not the last word.

## Source
Use only the attached document. Do not assume facts that are not present in it.

## Expectations
- Work through the document step by step before reaching any conclusions: go through it section by section and, for each section, state what claims or statements it makes and which of the risk categories below (if any) each one touches. Show this reasoning — do not skip straight to the answer.
- Then, drawing on that walkthrough, return your findings as a table: | # | Issue | Where it appears | Why it's a problem | Severity (High/Med/Low) |
- Flag in particular: unverifiable performance claims, forward-looking statements without appropriate qualification, absolute or superlative language, and anything that reads as advice rather than information.
- After the table, list any questions you'd want answered before sign-off.

## Guardrails
- Do NOT rewrite the document: identify issues only. A human will decide on fixes.
- Do NOT invent regulatory citations or rule numbers. If you believe a rule may apply but you're not certain, say so plainly and mark it for human verification.
- If the document is clean on a given dimension, say so rather than manufacturing a finding.
```

***The self-check pass (run after the review above)***

```
## Goal
Review your own findings from the previous step for reliability, before they go to a human compliance reviewer.

## Source
Use only the original document and your own list of findings from the previous step.

## Expectations
- For each finding, check it back against the document and quote the exact text it relies on. If you cannot point to specific supporting text, mark the finding [UNSUPPORTED: possibly overcautious] so the reviewer knows to discount it.
- Then read the document once more, specifically hunting for any issue your first pass did NOT flag, and add those.
- Re-state your final list with a confidence label (High / Medium / Low) on every item.

## Guardrails
- Do NOT defend a finding you cannot tie to specific text; it is better to withdraw a weak finding than to justify it.
- Do NOT invent regulatory citations in this pass either.
```

### **Demo 3 — A four-link chain with Chain of Verification**

| 📎 File required: ILS_Market_Insights_H1_2025_SAMPLE.docx |
| :---- |

The scenario: you need a one-page internal briefing for the deal team ahead of a discussion on a market development, using a long industry report as your source. Run these four links in order, in the same conversation, so each link can use the prior output. Link 4 is the key pattern — the model writes its own verification questions and answers them against the Link 1 fact list, not against its own narrative.

***Link 1 — Extract the raw material***

```
## Goal
Pull the key facts from the attached industry report that a deal team would care about for a market discussion.

## Source
Use only the attached report. Preserve figures exactly as written; do not round or estimate.

## Expectations
- Return 8-12 bullet points, grouped under: Market size, Pricing, Returns, Loss activity, Structural trends.
- Each bullet must be traceable to the document. If a figure is unclear, write [unclear] rather than guessing.
- No interpretation yet: facts only.
```

***Link 2 — Turn facts into a narrative (feeding Link 1's output)***

```
## Goal
Using the fact list above, draft a half-page narrative briefing for HSCM's deal team on what this market data means for our discussion.

## Source
Use ONLY the fact list produced in the previous step. Do not introduce new figures or facts that weren't in that list.

## Expectations
- Lead with the single most important takeaway.
- Neutral, internal, analytical tone: this is for colleagues, not investors.
- Where the data supports more than one reading, present both rather than picking one.

## Guardrails
- Do not state conclusions the facts don't support. Frame judgement calls as "this suggests" / "one reading is", not as established fact.
- Do not add market outlook or forecasts that weren't in the source.
```

***Link 3 — Generate the wrapper (feeding Link 2's output)***

```
## Goal
Create a 3-bullet executive summary and a list of 3-4 discussion questions to open the deal-team meeting, based on the narrative briefing above.

## Source
Use only the narrative briefing from the previous step.

## Expectations
- Executive summary: 3 bullets, one sentence each, skimmable in 15 seconds.
- Discussion questions: open-ended, designed to provoke debate, not yes/no.
- Output ready to paste at the top of the briefing document.
```

***Link 4 — Verify before finalizing (Chain of Verification)***

```
## Goal
Before this briefing is finalized, verify it for accuracy against the source facts. You drafted it; now check the draft. Do not assume it is correct.

## Source
- The verified fact list from Link 1.
- The assembled briefing (narrative + executive summary + questions) from the steps above.

## Expectations
1. Generate a list of verification questions: one for every factual claim, figure, and characterization in the briefing.
2. Answer each question using ONLY the Link 1 fact list as evidence. Do NOT treat the briefing itself as evidence for its own claims.
3. Flag every claim the fact list does not support, contradicts, or supports only partially, and quote the relevant fact, or note its absence.
4. List any number in the briefing that does not appear, exactly, in the fact list.

## Guardrails
- Treat the briefing as a draft to be tested, not as established truth.
- If a claim cannot be tied to the fact list, mark it [UNSUPPORTED: human check] rather than rationalizing it.
- Do NOT introduce any new facts, figures, or outlook in this step. This pass only checks; it does not add.
```

### **Demo 4 — Analyze-then-draft in Outlook**

| ℹ Note: No file attachment — Copilot reads the thread from Outlook directly. Look for the thread with "Project Lighthouse" in the subject (Glenmara / Fund III allocation). |
| :---- |

The Outlook power-user pattern in two moves: first make the model read and analyze the thread, then make it draft a follow-up from its own analysis. Run them in order in the same conversation.

***Link 1 — Analyze the thread***

```
## Goal
Analyze the email thread with "Project Lighthouse" in the subject and extract the state of play for someone who needs to catch up fast.

## Source
Use only the messages in this thread.

## Expectations
Return four clearly labeled sections:
- COMMITMENTS: who promised to do what, and by when (only if explicitly stated)
- OPEN QUESTIONS: anything raised that hasn't been answered
- DECISIONS: anything explicitly agreed
- UNRESOLVED TENSIONS: points where participants appear to disagree

Run a verification pass on your own extraction before finalizing: for every item across all four sections, quote the exact line it is based on and name the sender. If an item cannot be tied to a specific line in the thread, mark it [UNSUPPORTED] and move it out of the main lists — do not keep it on the strength of a general impression.

## Guardrails
- Only extract what is explicitly written. Do not infer commitments, owners, or deadlines that aren't stated.
- If a section has no items, write "None explicitly stated" rather than inventing entries.
- Do not editorialize on people's tone or motives.
```

***Link 2 — Draft the follow-up (feeding Link 1)***

```
## Goal
Draft a follow-up email that closes out the open questions and confirms the commitments identified above.

## Source
Use the analysis from the previous step and the original thread.

## Expectations
- Match the tone and formality of the existing thread: read it and mirror it.
- Structure: brief context line, then a short numbered list of what's confirmed, then the specific open items I need responses on, with names.
- Under 200 words. Include a subject line that continues the thread.
- Produce it as a draft I can edit in Outlook, not a final send.

## Guardrails
- Do not commit HSCM to anything that wasn't already agreed in the thread.
- Do not invent dates or owners. If something needs a deadline and none was given, leave a clearly marked placeholder: [confirm deadline].
- This is investor-adjacent correspondence: keep it precise and conservative.
```

### **Demo 5 — Updating a Word document with tracked changes**

| 📎 Files required: Sample_Internal_Guidance_Marketing.docx AND Amended_Marketing_Requirements.pdf |
| :---- |

| ℹ Setup: Open Sample_Internal_Guidance_Marketing.docx in Word and turn on Track Changes first (Review tab → Track Changes). This way every edit Copilot makes is captured for human approval. |
| :---- |

Copilot in Word can take an existing document and update it against a new input (a new regulation, a new internal standard) with tracked changes, so a human reviews every edit before anything is accepted. After it runs, review the tracked changes and the change log together, and accept/reject each edit yourself.

```
## Persona
Act as a compliance analyst updating internal guidance to reflect a new regulatory requirement, working carefully and conservatively because every edit will be reviewed by a senior reviewer before anything is finalized.

## Goal
Update the attached internal guidance document so it aligns with the new requirement described in the second attachment. Make the changes directly in the document. (Track Changes is switched on in Word, so each edit you make will be captured as a tracked change for human approval.)

## Source
- Document 1: the existing internal guidance document
- Document 2: the new regulatory requirement
Use only these two documents.

## Expectations
- Make the minimum changes necessary to bring the guidance into alignment: do not rewrite sections that don't need to change.
- Do NOT add comments inside the document. Instead, after making your edits, output a numbered change log here in the chat. For each edit, state the section you changed, what you changed it to, and which part of the new requirement triggered it, so the reviewer can read the log alongside the tracked changes.
- Where the new requirement is ambiguous about how it applies to us, do NOT guess and do NOT make that edit. List it instead under "Open questions for the reviewer" at the end of your chat reply.

## Guardrails
- Every edit you make to the document must appear in your chat change log with a reason. Do not change anything you haven't logged.
- Do NOT invent obligations the new requirement doesn't actually impose.
- If a required change needs legal or compliance judgement (not just wording), do not make the call yourself: leave it as an open question in the chat.
- Preserve the document's existing structure and defined terms unless the requirement specifically forces a change.
- Do not turn off Track Changes or accept any edits yourself; leave every change pending for the reviewer.
```

## **Part 3 — Copilot Pages**

### **Demo 6 — Turning an answer into a collaborative Page**

| 📎 File required: ILPA-DDQ-2.0.pdf |
| :---- |

Copilot Pages turns a good chat answer into a persistent, shareable, collaborative document. Run the prompt below, then select **Edit in pages** at the bottom of the response to open it as a Page the team can work on together. Once it's a Page, try editing it live (e.g., ask to "add a target-date column") and then use the export-to-Word path when you're ready.

```
## Goal
Turn the attached LP Due Diligence Questionnaire into a response-coordination tracker that the IR and operations team can work on together in a Copilot Page. This is a planning and ownership document, not the answers themselves.

## Source
Use only the attached DDQ. Work from its section structure and questions.

## Expectations
- Produce a table with one row per top-level section of the DDQ, with these columns:
  - Section (number and title)
  - What it covers (one short line)
  - Suggested owner (the team or role best placed to respond; e.g. IR, Operations,
    Finance, Compliance, Legal, ESG lead)
  - Status (default every row to "Not started")
- Format it as a clean table suitable for a Copilot Page the team will edit together.

## Guardrails
- Do NOT draft or attempt any actual answers. This is a coordination and ownership map only.
- Do NOT infer or invent any fund data, performance figures, fees, or terms.
- Flag any section that will require Confidential information (performance, positions, PII, fees, or third-party terms) with [COMPLIANCE GATE] in that row, so the team knows it needs special handling and compliance sign-off.
```

## **Part 4 — Copilot Notebooks**

### **Demo 7 — Grounded review across a curated source set**

| 📎 Files required (add all three to the Notebook): Sample_Compliance_Disclosure_DRAFT.docx, Sample_Internal_Guidance_Marketing.docx, Amended_Marketing_Requirements.pdf |
| :---- |

A Notebook is a persistent workspace where you gather the reference material for an ongoing piece of work, and Copilot grounds its answers only on that curated set. Add the three files to a Notebook first, then run the prompt below — notice the answer reasons over those documents only.

```
Review the draft "Sample_Compliance_Disclosure_DRAFT" against both our internal marketing guidance and the amended marketing requirements.

- List each point where the draft does not comply, and for every point name which document the rule comes from (the internal guidance or the amended requirements).
- Note anything the draft is missing that the amended requirements now expect.
- Do not use any knowledge outside the documents in this notebook.
```

## **Part 5 — Microsoft's Built-In Agents (Researcher & Analyst)**

### **Demo 8 — The Researcher agent**

| ℹ Note: No file attachment — Researcher works across the web and your Microsoft 365 work content. It is built for depth, not speed, so expect it to take a while. It may pause to ask clarifying questions before it starts. |
| :---- |

Researcher builds a plan, reasons across multiple sources, and delivers a structured, source-cited report. The prompt below also asks it to run a verification pass on its own output. Remember to click through and validate the cited sources yourself.

```
## Goal
Prepare a structured market-intelligence briefing on cyber catastrophe bonds / cyber ILS to support an early-stage internal discussion about whether it warrants deeper diligence.

## Scope and Sources
- From the web: recent market size, structural trends, notable transactions, and risk themes in this sector.
- From my work content: identify any comparable past internal analyzes or precedents on similar opportunities, and note their existence and structure: do NOT reproduce confidential figures or client-identifying detail in the briefing.

## Expectations
- Deliver a structured, source-cited report with these sections: Market overview, Key trends, Risk themes, Comparable precedents (existence and approach only), Open questions for the deal team.
- Cite every external claim. Mark anything you couldn't verify as [unverified].
- End with the 5 questions a skeptical investment committee would ask first.
- Then run a verification pass on your own report: list the three claims you are LEAST confident in, state what additional source would confirm or refute each, and give every section an overall reliability label (High / Medium / Low).

## Guardrails
- This is a FIRST DRAFT for analyst review, not a recommendation and not a deliverable.
- Do NOT include confidential HSCM data, specific position-level information, or client-identifying detail in the output, even if you can access it. Reference the existence and structure of internal precedents only.
- Do NOT state a buy/hold/pass view: surface considerations, don't make the call.
- If you need information you can't responsibly access or verify, ask me a clarifying question rather than filling the gap.
```

### **Demo 9 — The Analyst agent**

| 📎 File required: ILS_Portfolio_Holdings_Sample.xlsx |
| :---- |

The Analyst agent is like an on-demand data scientist — it writes and runs Python in a secure environment and shows you the code so you can verify how it got the answer. Run the first prompt, then review the reasoning chain and the Python it used before running the follow-up.

***Prompt 1 — Find and explain the outlier***

```
Analyze this ILS portfolio, find the single biggest performance outlier and what's driving it, and give me a chart plus a short plain-language summary I could share with a non-technical stakeholder.
```

***Prompt 2 — Break it down further***

```
Now break the mark-to-market P&L down by peril and region.
```

## **Part 6 — Building Your Own Agents**

### **Demo 10 — Level 1: an Instruction-Follower agent (FAQ Validator)**

| 📎 File required (as the agent's grounding source): HSCM_Operations_Compliance_FAQ.docx |
| :---- |

A level 1 agent is a role definition, instructions, and constraints pointed at approved grounding material. Build the agent with the instructions below, then test it with the questions that follow. The first two are answerable from the source; the third deliberately is not — watch the agent refuse rather than guess.

***Agent instructions***

```
Goal:
You are a FAQ Validator. Your goal is to answer questions accurately using only approved source documents.

Context:
You are helping employees get reliable answers to common questions. Keep responses clear and concise. Always tell the user which document your answer came from. Do not speculate or add information that is not in the sources.

Source:
Use only the specified knowledge sources. Do not use general knowledge, prior training data, or any other documents. If the answer cannot be found in the given sources, tell the user clearly and do not answer from memory.

Expectations:
For every response you must:
- First generate a draft response.
- Next, identify and list the key factual claims in that draft.
- Then verify each claim against the specified sources and show the verification.
- Finally, produce a revised response that includes only verified information and references the source.

If you cannot find a verified answer, respond with: "I could not find a verified answer to this question in the approved documents."
```

***Test question 1 (in scope)***

```
What's the limit for accepting a gift from a counterparty?
```

***Test question 2 (in scope)***

```
Do I need pre-clearance to trade in my personal account?
```

***Test question 3 (out of scope — should be refused)***

```
What was Fund III's net return last quarter?
```

### **Demo 11 — Level 6: a Fully Autonomous agent (Due Diligence Scoping)**

| ℹ Note: No file attachment — the engagement description is provided as the agent's input. A level 6 agent decides each next step from what it just learned rather than following a fixed plan, so its route may differ each time it runs. |
| :---- |

The other end of the spectrum from Demo 10. Build the agent with the instructions below, then give it the engagement description as its input.

***Agent instructions***

```
Goal:
You are a Due Diligence Scoping agent. Given a brief description of an engagement, work out the due diligence that is needed by reasoning and acting one step at a time. Do NOT write a fixed plan up front; decide each next step from what you have just learned.

Loop:
Repeat the following until further steps would not materially change the scope:
- Thought: state what you know so far and the single most useful thing to establish next, and why.
- Action: take that one step (e.g. look up the manager or strategy, check what a standard manager due-diligence questionnaire would cover for this area, identify a specific document or data point to request, or test an assumption). Use only sample or approved sources; where you cannot actually retrieve something, state what you would request and continue.
- Observation: record what that step told you, including anything that changes your direction. Let each Observation drive the next Thought. Adapt as you learn rather than following a pre-set list of workstreams.

Final answer:
When the loop is complete, produce a one-page scoping summary: engagement overview, the due-diligence workstreams you arrived at (with why each matters), the top three risks, and suggested next steps.

If information is missing, state your assumption in the Observation and continue rather than stopping to ask.
```

***Agent input***

```
HSCM is considering a first-time allocation of approximately $75 million to an external ILS fund manager we have not previously invested with. The manager runs a collateralized reinsurance strategy concentrated in US and Japanese catastrophe risk. Scope the due diligence we would need to complete before recommending an allocation.
```

### **Demo 12 — Level 2: an Orchestrated-Workflow agent (Project Update)**

| ℹ Note: No file attachment — the agent reads from Outlook. Point it at the "Project Lighthouse" email thread when it asks. |
| :---- |

A level 2 agent executes a fixed sequence of steps, passing a named output from each step to the next (note the [Project], [Period], [EmailContent], [ExtractedUpdate] labels). Build the agent with the instructions below, then run it.

***Agent instructions***

```
Goal:
You are a Project Update agent. You produce a clear status update for a project by
working through a fixed sequence of steps, passing a named output from each step to the next.

Step 1 - Collect and store inputs:
- Ask the user for the project name and store it as [Project].
- Ask the user for the reporting period (e.g. "this week") and store it as [Period].
- Retrieve the relevant emails for [Project] during [Period] and store them as [EmailContent].

Step 2 - Extract from the stored emails:
- Using only [EmailContent], distil a structured set of findings covering Progress,
  Decisions, Open Questions, and Blockers.
- For each item, note which email it came from and why you included it.
- Store the result as [ExtractedUpdate].

Step 3 - Build the final update:
- Using [ExtractedUpdate], write a concise status update with the sections: Progress,
  Decisions, Open Questions, Blockers.
- If [ExtractedUpdate] contains any blockers, add an "Escalation needed" note at the top.
- Present it as an editable draft for the user to review before sharing.

Standing guardrails (apply to every step):
- Use only [EmailContent]; do not invent updates, dates, owners, or facts.
- If a section has nothing explicitly stated, write "None this period."
- Confidential-by-default: nothing leaves HSCM's licensed Copilot environment; the user reviews and sends.
```

### **Demo 13 — The Workflows agent (live exercise)**

| ℹ Note: No preset prompt and no file — this is a live, build-your-own exercise. There is nothing to copy in advance. |
| :---- |

When a workflow has more than three or four steps, baking it into a level 2 agent's instructions starts to drift. The Workflows agent in Microsoft 365 Copilot lets you describe the workflow and the outcome you want in plain natural language, and it generates the workflow for you.

In the session we'll take a workflow you do daily, describe it in a natural-language prompt, and have the Workflows agent turn it into a real workflow in Copilot 365. Come ready with one repetitive multi-step task from your own week (the more concrete, the better) as the raw material. For what the agent can and can't connect to, see the supported connectors and actions documentation:

`https://support.microsoft.com/en-us/microsoft-365-copilot/get-started-with-workflows-in-microsoft-365-copilot`
