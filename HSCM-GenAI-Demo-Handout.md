# HSCM — Generative AI Essentials for Non-Technologists

## Student Demo Handout



### **How to use this handout**

This handout contains every prompt that will be demoed during the session. Copy any prompt below and paste it into **Microsoft Copilot** to follow along. Each demo lists:

* The file (if any) you'll need to attach when running the prompt
* A short description of what the demo shows
* The prompt itself, in a gray box, that you can copy directly

Files referenced in this handout will be distributed separately. The 📎 callout box at the top of a demo tells you which file to attach. Demos without a callout don't need a file.

A few demos run as a **sequence** — a first prompt, then a follow-up in the same chat. Where that's the case, the steps are labeled in order. Run them one after another in the same conversation.

> **Reminder:** Copilot is a starting point, never the final word. Everything you generate here is reviewed by a human — you — before it goes anywhere. Only put **Public** data into a prompt; anything created at HSCM or received in the course of your job is **Confidential** by default.

---

## **Part 1 — Prompting Mechanics**

### **Demo 1 — Same prompt, different answers (non-determinism)**

Run this exact prompt twice. The two responses will differ — that's not a bug, it's how the technology works. An LLM is probabilistic, not deterministic, which is the first reason you can never blindly trust the output. No file needed.

```
What are 3 catchy names for a new internal initiative focused on improving DDQ response turnaround times?
```

### **Demo 2 — Structure changes everything**

Three versions of the same request, each more structured than the last. Run them in order and compare the outputs. Level 3 uses the **GCSE** framework (Goal, Context, Source, Expectations). No file needed.

***Level 1 — Vague***

```
Write an email to an LP.
```

***Level 2 — Natural language, some detail***

```
I need to write an email to an LP named Sarah who hasn't responded to our last two requests for a catch-up call. She's a long-standing investor and I don't want to seem pushy but I'd like to reconnect before the next quarterly update.
```

***Level 3 — Structured with GCSE***

```
## Goal
Draft a follow-up email to a long-standing LP who hasn't responded to two previous requests for a catch-up call.

## Context
- Investor: Sarah, 8-year relationship across two HSCM funds
- Two prior emails sent (March 3 and March 17), no response
- Next quarterly investor update is in three weeks
- Tone should be warm and patient, not chasing

## Expectations
- Professional but warm
- Acknowledge that she's busy without being passive-aggressive
- Provide 2-3 specific time options
- Mention one value-add for the call (a portfolio update or a market view)
- Under 200 words, include subject line
```

### **Demo 3 — Language tunes the answer to the audience**

Same topic, three different framings. Run all three and notice how different the responses are — each one is shaped for a different reader. No file needed.

***Version 1 — No audience***

```
Explain what an insurance-linked security is.
```

***Version 2 — For a new associate***

```
Explain what an insurance-linked security is as if I'm a first-year associate who just joined HSCM and has come from a corporate finance background, not insurance. Use an analogy.
```

***Version 3 — For an investor letter***

```
Explain what an insurance-linked security is for a section of an investor update letter. The audience is institutional LPs who are financially sophisticated but not specialists in reinsurance or ILS. Focus on the structural mechanics and why ILS is treated as an uncorrelated asset class.
```

---

## **Part 2 — Recognizing Bias**

### **Demo 4 — Bias in the data**

A broad question that surfaces bias baked into the training data. Run it and look at whether the list skews by gender, region, or era. The model isn't being intentionally biased — it's reflecting patterns in what it was trained on. No file needed.

```
Who are the top 10 hedge fund managers of all time?
```

### **Demo 5 — Interpretation bias**

A deliberately vague request. Watch how the model *guesses* what you meant — weather? a loss forecast? an economic outlook? The interpretation it picks reveals its assumptions, which is exactly why specificity matters. No file needed.

```
Give me today's forecast.
```

---

## **Part 3 — Iterating, Meta-Prompting & Templates**

### **Demo 6 — Let the AI help you write the prompt (meta-prompting)**

When you're not sure how to structure a prompt, ask the model to interview you first. Run Step 1, answer its questions one at a time, then run Step 2 to get a polished, reusable prompt. No file needed.

***Step 1 — Have it interview you***

```
I want to build a reusable prompt that drafts a first-version internal meeting agenda for a recurring weekly operations meeting. Help me clarify what the prompt needs by asking me one question at a time.
```

***Step 2 — Have it write the final prompt***

```
Now use this clarity to create a detailed prompt in a code block that I can use. Do not use emojis.
```

### **Demo 7 — Templatize a prompt that works**

Once a prompt works, don't rewrite it from scratch every time — turn the changing parts into placeholders so your team can reuse it. Compare the one-off version with the templatized version. No file needed.

***One-off version***

```
Create a re-engagement email for our long-standing LP ACME PENSION FUND, let them know it's been 6 months since their last review and Bob their relationship lead would like to schedule a catch-up.
```

***Templatized version (reusable)***

```
Create a re-engagement email for our long-standing LP [LP_NAME], let them know it's been [TIME_SINCE_LAST_REVIEW] since their last review and [RELATIONSHIP_LEAD] their relationship lead would like to schedule a catch-up.
---
Ask the user to fill in the placeholders before generating the email.
```

---

## **Part 4 — Context, Hallucinations & Guardrails**

### **Demo 8 — Drafting without context (hallucination risk)**

The model has never seen "InsightEdge," so it fills the gaps with generic, made-up specifics. That's a **hallucination** — confident, fluent, and wrong. Run it and look closely at how little of the output is actually about a real product. No file needed.

```
Write a blog post announcing the launch of our new portfolio analytics tool, InsightEdge. We want to excite potential clients about modernizing their portfolio monitoring, especially those who have been relying on traditional manual reporting. Highlight its main features like automated performance attribution and real-time risk monitoring. Include a call to action to schedule a demo.
```

### **Demo 9 — Add a guardrail**

The same prompt with one extra instruction — "if you don't know, say so." Watch how that single guardrail changes the behavior completely. No file needed.

```
Write a blog post announcing the launch of our new portfolio analytics tool, InsightEdge. We want to excite potential clients about modernizing their portfolio monitoring, especially those who have been relying on traditional manual reporting. Highlight its main features like automated performance attribution and real-time risk monitoring. Include a call to action to schedule a demo. If you don't know who that that product is or you don't have accurate information about that product, then respond with "I don't have reliable information about this product."
```

### **Demo 10 — Drafting WITH context and guardrails**

| 📎 File required: InsightEdge Product.docx |
| :---- |

Now the model has real information to work from. Attach the product specification, then run the prompt. The output should be specific and accurate — but you should still check it.

```
Write a blog post announcing the launch of our new portfolio analytics tool, InsightEdge. Include a call to action to schedule a demo.

## Context
Review the following product specification attached thoroughly before writing. 

## Expectations
- Use ONLY information contained in the product specification. Do not invent features, statistics, or capabilities not explicitly stated.
- Maintain factual, benefit-focused language without unverifiable superiority claims.
- If you're uncertain about a detail, either omit it or clearly indicate it as a general industry benefit rather than a specific product feature.
- If you don't know who that that product is or you don't have accurate information about that product, then respond with "I don't have reliable information about this product."
```

---

## **Part 5 — Drafting With Context & Guardrails**

### **Demo 11 — Draft an LP email (with internal context that must stay internal)**

| 📎 File required: Internal Memo.docx |
| :---- |

This demo shows the model using an internal memo *only* to inform tone and positioning — never to disclose. Attach the memo, then run the prompt and check that nothing internal leaks into the investor-facing email.

```
## Goal
Draft a professional email to a long‑standing LP informing them of a change to our quarterly reporting format.

## LP Context
- The investor has been with HSCM for 8 years across two funds
- We are transitioning from static PDF reports to an interactive digital reporting portal
- Some long‑standing LPs may be resistant to change
- The email is investor‑facing and relationship‑focused

## Internal Context (For Background Only)
You have access to an **internal memo** explaining the rationale for moving from PDF reports to an interactive digital portal.

This internal context is provided **only to inform tone and positioning**. It must **not** be referenced directly or disclosed to the investor.

## Expectations
- Warm, relationship‑focused tone that reflects an 8‑year partnership
- Emphasize investor‑relevant benefits
- Acknowledge that the LP may prefer the existing PDF format
- Offer a clear transition period and support
- Keep the email under 400 words
- Include a call to action to schedule a walkthrough of the new portal

## Guardrails
- Use **only** investor‑appropriate information in the email
- Do **not** reference internal documents, memos, operational motives, or efficiency gains
- Do **not** disclose internal strategy, scalability goals, or process changes
- Do **not** invent investor‑specific history beyond what is provided
- If you cannot confidently separate internal context from investor‑safe messaging, respond with:
  **"I don't have enough information to draft this email without risking internal data exposure."**
```

### **Demo 12 — Draft IC meeting talking points (context in the prompt)**

When you don't have a separate document to attach, you put the context directly into the prompt. No file needed.

```
## Goal
Create talking points for a 30-minute internal investment committee discussion of an existing position.

## Context
- Quarterly position review for a transportation finance investment
- Position is up 3.2% this quarter vs. internal target of 2.8%
- One sub-position is underperforming due to a counterparty restructuring
- The team has flagged a potential ESG concern that hasn't been formally evaluated

## Expectations
- Opening: positive framing of overall performance
- Middle: honest, balanced discussion of the underperforming sub-position with a recommended next step
- Close: surface the ESG concern as a discussion item, not a recommendation
- Bullet point format
- Internal, investment-team tone

## Guardrails
- Use **only** the information provided in the Context
- Do **not** invent causes of performance, forecasts, or market outlooks
- Do **not** imply guarantees or certainty of future results
- Frame recommendations as **discussion options**, not directives
- Do **not** reference other positions, counterparties, or internal strategy not in the Context
- If you cannot create talking points without adding assumptions, respond with:
  **"I don't have enough information to create these talking points safely."**
```

---

## **Part 6 — Summarization**

### **Demo 13 — One document, three audiences**

| 📎 File required: Swiss Re ILS Market Insights (February 2026 edition) |
| :---- |

Attach the report, then run each of the three prompts below. Same source, three completely different summaries — each tuned to a different audience and a different summary *type* (abstractive, extractive, hybrid). Tip: longer documents often benefit from Copilot's reasoning/thinking mode if it's available.

***For the HSCM Investment Committee (abstractive summary)***

```
## Goal
Provide HSCM's Investment Committee with a concise, strategic overview of the 2025 ILS market to inform discussion at the next quarterly review.

## Context
Use the attached Swiss Re ILS Market Insights report (February 2026 edition, covering full-year 2025) as the sole source. Your audience is HSCM's Investment Committee — sophisticated insurance and capital markets practitioners who do not need definitions but do need the strategic picture.

## Expectations
- Write an abstractive summary: paraphrase and synthesize the main points in your own words
- Cover: total issuance, outstanding notional, return performance, key trends in sponsors and perils, and any structural innovations highlighted in the report
- Highlight strategic themes relevant to an ILS allocator: capital flows, pricing dynamics, peril diversification
- Flag anything in the report that warrants Investment Committee attention (e.g., return drivers, loss activity, structural shifts)
- Avoid jargon padding; keep it actionable
- Maximum one page
```

***For an external macro analyst (extractive summary)***

```
## Goal
Act as a external macro analyst, one who covers alternative credit but is not an ILS specialist, with the precise figures and quoted commentary needed to update their house view on the ILS market.

## Context
Refer exclusively to the attached Swiss Re ILS Market Insights report. Audience: a sell-side or buy-side macro analyst who does not specialise in ILS.

## Expectations
- Create an extractive summary: quote the most relevant figures, ratios, and Swiss Re commentary directly from the document
- For each extracted item, include the page or section reference
- Organise extractions by: Market size, Issuance, Returns, Loss activity, Structural trends
- Include both reported figures and YoY comparatives where given; do not round or paraphrase numbers
- Call out any defined-term footnotes or methodology notes that affect comparability
- Use technical language appropriate for a financial professional
```

***For new HSCM hires (hybrid summary)***

```
## Goal
Help new HSCM hires, joining the firm from outside the ILS space to understand the state of the ILS market and HSCM's competitive context.

## Context
The summary will be used in an onboarding session for new hires in their first month at HSCM. Source: the attached Swiss Re ILS Market Insights report (full-year 2025).

## Expectations
- Start with a brief abstractive overview in plain language explaining how the ILS market performed and why it matters
- List 3-5 key data points using extractive snippets from the document (e.g., issuance volume, outstanding notional, total return)
- For each point, add a reference to the relevant page or section
- Explain each point's practical relevance — for example, what record issuance volume signals about market depth
- Use clear language; define acronyms on first use (ILS, cat bond, notional, peril)
- End with 2-3 questions the new hire should bring to their first meeting with the deal team
```

### **Demo 14 — Summarize a long email chain**

This prompt is designed to run against an Outlook conversation (e.g., a thread with "Project Aurora" in the subject) using Copilot's access to your mailbox. No file to attach — point Copilot at the thread, then run the prompt.

```
## Goal
Summarize a long email thread related to **Project Aurora** for a busy stakeholder.

## Context
- The input is a multi‑email Outlook conversation
- Emails all contain "Project Aurora" in the subject
- The thread includes updates, questions, and discussion
- Some messages may contain internal opinions, side conversations, or unresolved topics

## Expectations
- Concise, executive‑ready summary
- Written in neutral, professional language
- Clearly structured using bullet points
- Focus on signal over noise

The summary should include:
- Key themes or topics discussed
- Any clearly stated decisions (only if explicitly stated)
- Open questions or unresolved issues
- Notable next steps (only if explicitly mentioned)

## Guardrails
- Base the summary **only on the provided email content**
- Do **not** invent decisions, agreements, or conclusions
- Do **not** assume intent, tone, or priority beyond what is written
- Do **not** infer timelines, owners, or deadlines unless explicitly stated
- Exclude internal opinions, speculation, or casual commentary unless central to the discussion
- Do **not** add recommendations or personal interpretation
- Preserve confidentiality: do **not** expose sensitive details beyond what is required for a high‑level summary

If the email thread does not contain clear outcomes or decisions, state that explicitly rather than inferring them.

If you cannot summarize the thread without making assumptions, respond with:
**"The email chain does not contain enough explicit information to produce a reliable summary."**
```

### **Demo 15 — Turn messy meeting notes into structured minutes**

| 📎 File required: handwritten-meeting-notes.jpg |
| :---- |

Attach the image of the handwritten notes, then run the prompt. Notice how strictly it's told *not* to guess at attendees, decisions, or owners that aren't actually written down.

```
## Goal
Transform these rough handwritten meeting notes into a structured summary.

## Context
- The input consists of handwritten meeting notes
- Some handwriting may be unclear or ambiguous
- Not all decisions, owners, or dates may be explicitly documented

## Expectations
- Attendees:
  - List only those explicitly written in the notes
  - Do **not** guess additional attendees
- Key discussion points:
  - 3–5 bullets based strictly on written content
- Decisions made:
  - Include only decisions that are clearly stated
  - If none are explicit, state "No explicit decisions documented"
- Action items:
  - List only if clearly written
  - Include owners and due dates **only if explicitly noted**
- Next meeting:
  - Include only if a date or topic is clearly mentioned
```

---

## **Part 7 — Answering Questions From a Source**

### **Demo 16 — Build a grounded knowledge-base assistant**

| 📎 File required: Swiss Re ILS Market Insights (February 2026 edition) |
| :---- |

Attach the report and run the **setup prompt** first. Then ask the in-scope questions — it should answer only from the document. Finally, try the out-of-scope question and watch it refuse to fabricate. Run all of these in the same conversation.

***Setup prompt***

```
## Goal
Act as a grounded Q&A system that answers user questions about the 2025 ILS market using only the attached Swiss Re ILS Market Insights report, with no external knowledge or speculation.

## Context
Use the attached Swiss Re ILS Market Insights report as the sole source of truth. Only content explicitly present in the attached document — including tables, footnotes, and defined terms — is in scope.

Audience: any user asking a question about the 2025 ILS market — could be an analyst, an HSCM hire, an LP, or a journalist.

## Expectations
- Answer only from the provided document; do not use prior training data, external knowledge, or inference beyond what the text supports
- For each answer:
  1. Identify the most relevant section(s) of the document
  2. Synthesize a concise, coherent response grounded in that content
  3. Cite the page or section reference
- Preserve exact figures, percentages, and defined terms as they appear in the document; do not round, rephrase, or approximate numbers
- If figures differ between narrative text and tables, use the table values and cite the source without reconciliation
- If the question involves a defined term (e.g., "outstanding notional", "secondary market", "parametric trigger"), reference the relevant footnote or definition
- Do not infer causality, drivers, or outlook unless explicitly stated in the document
- Do not answer forward-looking or "why" questions unless the document explicitly addresses them
- If a question contains multiple parts, answer each part explicitly; if any part cannot be answered, respond only with:
   "Information unavailable in the current document."
- If the answer cannot be derived from the document, respond only with:
   "Information unavailable in the current document."
- Do not elaborate, speculate, or offer related information
- If a question is ambiguous or could be interpreted multiple ways, ask a clarifying question before answering rather than guessing
- Maintain a neutral, factual tone regardless of audience
- Keep answers concise: lead with the direct answer, then provide supporting figures or context only if needed
```

***In-scope questions (ask these next)***

```
What was the total cat bond issuance in 2025?
```

```
How did returns compare to prior years?
```

```
What were the main perils represented in 2025 issuance?
```

***Out-of-scope question (try to trip it up)***

```
What's HSCM's view on this market?
```

---

## **Part 8 — Editing & Refining**

### **Demo 17 — Tone adjustment: declining a prospective investor**

| 📎 File required: Email.txt |
| :---- |

A blunt, transactional draft needs to become professional and respectful — *without* changing the decision. The prompt asks Copilot to request the draft first, so paste the contents of `Email.txt` when prompted. Note the tension it has to manage: honesty vs. kindness, and clarity vs. evasiveness.

```
## Goal
Refine an IR-drafted email declining a prospective investor's allocation inquiry so that it is professional, respectful and aligned with a sophisticated alternative-investment manager's brand voice, without changing the underlying decision.

## Context
An investor relations lead has drafted a direct, transactional email informing a prospective investor that HSCM will not be accepting their allocation at this time. The decision itself is final and will not change.

Your role is to improve tone, framing, and clarity while preserving the IR lead's intent and all factual details. The email is investor‑facing and will be sent directly to the prospective investor.

Before proceeding, ask the user to paste the draft email they would like rewritten. Do not generate any rewritten content until the source email has been provided.

## Success Criteria
The rewritten email:
- Communicates the decision clearly and respectfully
- Feels consistent with how a sophisticated alternative-investment manager would communicate
- Preserves trust and professionalism despite a negative outcome
- Offers a constructive, forward‑looking path where appropriate
- Can be sent to a prospective investor ready for human review

## Expectations
- Preserve the core decision exactly as stated in the source email, including:
  - The decline itself
  - Any reference to future cycles
  - Any stated criteria for reconsideration
- Acknowledge the prospective investor's interest and thank them
- Explain the outcome clearly without listing blunt or personal failure reasons; frame eligibility criteria neutrally
- Offer a constructive path forward where applicable, such as:
  - Who they can contact with questions
  - When future engagement could occur, if stated
- Maintain a warm, professional, and human tone consistent with a premium alternative-investment brand
- Avoid corporate jargon, legalistic language, hollow apologies, or excessive sentiment
- Keep each version concise (150–180 words)
- Provide 2–3 rewritten variants with different tonal emphasis (e.g. relationship‑focused, crisp and professional, advisory and forward‑looking)
- Create the versions of the email in an Outlook draft

## Guardrails
- Do not soften, reverse, or obscure the decision
- Do not introduce new reasons, promises, timelines, or eligibility criteria
- Do not invent missing details or imply flexibility that does not exist
- Do not shift accountability for the decision
- If the source email is missing essential details (e.g. unclear sign‑off, missing future engagement guidance, ambiguous wording), ask a brief clarifying question before rewriting rather than making assumptions
```

### **Demo 18 — Communication consistency against a style guide**

| 📎 Files required: Communications Style Guide.docx, Internal Announcement.docx |
| :---- |

Attach both documents, then run the prompt. Copilot rewrites the informal announcement to match the firm's style guide while keeping the substance unchanged.

```
## Goal
Act as a senior corporate communications editor at HSCM with extensive experience shaping firm‑wide internal messaging. Revise the attached internal announcement so that it aligns with the HSCM Communications Style Guide while preserving the original intent, meaning, and factual content.

## Context
You are provided with:
1. An informal draft of an internal announcement intended for employees
2. The HSCM Communications Style Guide, which defines expected tone, structure, and writing standards

The announcement communicates internal process updates. The substance of the message must remain unchanged; only how it is expressed should be refined.

Audience: internal HSCM employees.

## Success Criteria
The revised announcement:
- Reflects the tone, voice, and structure outlined in the Communications Style Guide
- Reads as professional, clear, and appropriate for firm‑wide internal communication
- Maintains confidence and credibility without sounding casual or overly verbose
- Can be distributed internally ready for human review

## Expectations
- Preserve the original meaning, intent, and scope of the announcement
- Improve clarity, structure, and flow in line with the style guide
- Replace informal or conversational language with professional phrasing
- Use a composed, human tone consistent with a sophisticated alternative-investment manager
- Organize content logically (context → key information → next steps)
- Keep the revision concise; avoid adding unnecessary detail or emphasis
- Use professional salutations and sign‑off appropriate for internal communications

## Guardrails
- Do not introduce new information, commitments, timelines, or policy implications
- Do not change the substance or implications of the message
- Do not add operational rationale beyond what is already stated
- Do not reference the style guide explicitly in the output
- If the source announcement is ambiguous, preserve the ambiguity rather than clarifying or expanding it
```

---

## **Part 9 — Code & Technical Content**

### **Demo 19 — Excel formulas and analysis in plain English**

| 📎 File required: ILS_Market_Data_Sample.xlsx |
| :---- |

Attach the spreadsheet, then run any of these one at a time. You describe what you want in plain English; Copilot writes the formula, chart, or transformation. No coding required.

```
What's the total issuance size by peril? Put the answer in a new sheet.
```

```
Create a chart showing issuance distribution by peril.
```

```
Add a column that categorizes deals as 'Large' (>= $300M), 'Medium' ($150M-$300M), or 'Small' (< $150M).
```

```
Calculate how many days since each deal's issuance date.
```

```
Highlight all deals with an issuance size over $500M.
```

```
Split the Tranche ID into separate Peril Code, Year, and Class columns.
```

***Optional — add column definitions for better results***

For data work, telling the model what each column means produces noticeably better output. Paste this alongside the spreadsheet when you want Copilot to interpret the data more accurately.

```
## Column Definitions
- Deal Name: Sponsor program and series (e.g., "Ceres Re 2024-1")
- Tranche ID: Structured code, PERIL-YEAR-CLASS (e.g., "USW-2024-A")
- Peril: Primary modeled peril (US Wind, EU Wind, Japan Quake, US Quake, US Severe Storm, Multi-Peril)
- Issuance Date: Date the deal came to market (YYYY-MM-DD)
- Issuance Size ($M): Risk capital issued, in USD millions
- Coupon Spread (%): Spread over the reference rate, in percentage points
- Expected Loss (%): Modeled annual expected loss, in percentage points
```

---

## **Part 10 — Classifying & Categorizing**

### **Demo 20 — Sentiment classification with few-shot prompting**

This prompt provides a few examples of input → output to guide the model — that's **few-shot prompting**. The examples set the pattern; the model applies it to the new comments. No file needed.

```
## Goal
Classify each feedback comment below as Positive, Neutral, or Negative.

## Examples
- "The new layout is fantastic, so much easier to find things." -> Positive
- "It works, though it took a little getting used to." -> Neutral
- "I keep getting logged out and it's slowing me down." -> Negative

## Comments to classify
1. "Honestly this has saved me a lot of time each week."
2. "It's fine, does what it says."
3. "I'm not sure I see the benefit yet."
4. "Loading is still slow on my end."
5. "Really happy with how simple the new process is."
6. "A few hiccups at first, but support sorted it quickly."

## Output
Return a table: Comment # | Comment | Classification. No extra commentary.

## Guardrail
Classify only from the text. If a comment is genuinely ambiguous, label it Neutral and add "(ambiguous)".
```

---

## **Part 11 — Extracting Structured Data**

### **Demo 21 — Map the structure of a DDQ**

| 📎 File required: ILPA-DDQ-2.0.pdf (extract only the relevant section — e.g., pages 20–23) |
| :---- |

DDQs run 100+ pages, so the smart move is to narrow to the section you need *before* extracting. Attach just the relevant pages, then run the prompt. Note what this demo does **not** do: it maps the *structure* of the questionnaire only — no HSCM answers, no real fund data.

```
## Goal
Extract the structured set of questions from a long, semi-structured Due Diligence Questionnaire and output them as a clean table suitable for review by HSCM's IR/operations team. The goal is to map the questionnaire's structure, not to populate answers.

## Persona
You are a meticulous operations analyst at an alternative-investment manager with deep experience with LP DDQs. You work on the team that ingests inbound DDQs from prospective LPs, maps them against HSCM's existing answer library, and identifies which questions are net-new versus already-answered. You are known for your precision with question wording and for refusing to "interpret" what a question is asking — you transcribe it as written.

## Context
Use the attached DDQ as the sole source. The output will be used to build an internal mapping of the questionnaire's structure. **You are not being asked to answer any questions** — only to extract the question structure.

## Expectations
- Extract the following fields for each question in the DDQ:
  * Section / Subsection
  * Question number (as written in the source)
  * Question text (verbatim)
  * Question type: [Yes/No] / [Short answer] / [Detailed narrative] / [Document request] / [Quantitative]
  * Notes (any sub-bullets, dependencies, or "if yes, also describe..." follow-ups)

- Output as a table, one row per question, with the fields above as columns in the order listed
- Preserve exact question wording as it appears in the document; do not paraphrase
- Use "Not specified" for any field not explicit for a given question
- Group rows by section in the order the document presents them

- After the table, provide a short validation summary:
  * Total number of questions extracted
  * Sections covered
  * Any ambiguities or formatting irregularities encountered and how you resolved them

- If the user requests a different output format afterward (CSV, JSON, etc.), re-emit the same data in that format without re-extracting

## Guardrails
- Do not attempt to answer any of the questions — extraction only
- Do not infer the intent of an ambiguous question; transcribe it as written and flag it
- Do not skip questions you consider "redundant" — preserve the document as-is
```

---

## **Part 12 — Capturing & Improving a Process**

This is a four-step workflow. Each prompt feeds the next, so run them **in order, in the same conversation**: capture the process → visualize it → find the friction → propose a simpler version. No files needed — the process description is embedded in Demo 22.

### **Demo 22 — Capture an "as-is" process from a messy description**

```
## Goal
Capture an "as-is" process map from the description below. Surface every step, decision point, handoff, and waiting period exactly as it happens today — not how it should happen, and not a cleaned-up version.

## Context
The description is from a senior team member at HSCM who has handled DDQ responses for several years. It's conversational, informal, and almost certainly incomplete. I need the capture to reflect the actual messiness of the source so I can have a useful follow-up conversation with them about the gaps.

## Source
"Okay so when an LP sends us a DDQ, usually it comes through investor relations, sometimes attached to an email and sometimes through their portal. I review it to see how much of it overlaps with our standard answer library — that's a Word doc that lives on SharePoint that we've built up over a few years. Anything that overlaps I copy over, but I have to manually adjust the wording each time because LPs ask the same question slightly differently. For anything that doesn't overlap, I email the relevant person — usually someone on the deal team for strategy questions, ops for fund admin questions, compliance for regulatory questions. Their responses come back over a few days, sometimes a week if it's busy. I drop those into the doc, then send the whole thing to compliance for review, which is usually 2 to 3 days. Compliance comes back with edits, I make them, then I send it to the partner who has the LP relationship for sign-off. Once they approve I send it back to the LP. The whole thing usually takes two to three weeks. Oh and I also have to manually update the answer library after each DDQ if any new answers came up that we'd want to reuse, but honestly that often doesn't happen because by then we've moved on."

## Expectations
Produce a numbered list of steps in the order they happen. For each step, include:
- Step number and short title
- Actor (who does it)
- System (which tool or platform)
- Estimated time
- Type: [Action] / [Wait] / [Decision] / [Handoff]

## Example of the format I want (use this shape exactly)
1. LP submits DDQ
   - Actor: LP
   - System: Email or LP portal (inbound)
   - Time: n/a (trigger event)
   - Type: [Handoff] — LP → IR

2. IR reviews against existing answer library
   - Actor: IR analyst
   - System: SharePoint (Word answer library)
   - Time: ~30-45 minutes
   - Type: [Decision] — overlap vs. net-new

## Guardrails
- Do NOT invent details that are not in the source. If something is unclear (system name, exact timing, who performs a step), write [unclear] and keep going. Do not guess.
- Do NOT tidy the process up. If the source implies the step happens in a clunky or redundant way, preserve that.
- Preserve every waiting period and every handoff, even if they seem obvious.
- At the very end, add a section titled "Gaps to clarify with the SME" that lists every [unclear] item plus any ambiguity you noticed that a new hire would trip over.
```

### **Demo 23 — Visualize the process as a flowchart**

```
## Goal
Write a short Python script using the `graphviz` library that turns the as-is DDQ response process map above into a flowchart PNG.

## Context
The PNG will go into a slide for an internal process-review session. Audience: HSCM operations and IR leaders who will skim, not read. The visual needs to make the handoffs and waiting periods jump off the page.

## Source
The numbered as-is process map from the previous step. Every box in the diagram must come from a step in that map.

## Expectations
- Return a single Python code block and nothing else.
- Layout: top to bottom.
- Style the boxes like this:
  - Start and End: grey ovals
  - Action steps: blue rounded boxes
  - Waiting periods: orange boxes with a dashed border
  - Decision points: white diamonds
- Label arrows with the handoff when one occurs (e.g. "IR → Deal Team").
- Keep the text inside each box to 4 short lines max.
- Save the output as `ddq_response_process.png`.

## Guardrails
- Every box must match a step in the process map. Do not invent steps.
- If a step was marked [unclear], keep that note inside the box label.
- Keep waiting periods as their own orange dashed box — do not merge them into the step before.
- Use short, simple IDs for boxes (like S, A1, D1, W1). Only put words and spaces in the LABELS, never in the IDs.
```

### **Demo 24 — Identify friction in the process**

```
## Goal
Analyse the as-is DDQ response process map above and identify opportunities for simplification. The output feeds directly into the next prompt, which will design a to-be process, so the issues need to be specific and actionable.

## Context
We're looking for the kinds of issues that operations and IR leaders can act on: handoffs that could be collapsed, waiting periods caused by manual coordination, steps done in two systems that could be one, and so on. We are NOT looking for generic advice ("consider automation"). Every finding must point to a specific step or pair of steps from the map.

## Source
The as-is process map from above. Do not reference external best practices or generic process-improvement knowledge — everything you flag must be traceable to a step that actually appears in the map.

## Expectations
Produce a Markdown table with these columns, in this order:
| # | Issue | Where it occurs (step #) | Why it's a problem | Category | Impact |

Categories (use these exact labels):
- Duplication
- Unnecessary handoff
- Manual step (automatable)
- Waiting period
- Missing standardisation
- Rework risk

Impact: High / Medium / Low, based on a combination of time cost and error risk. State the reason for the rating in the "Why it's a problem" cell, do not just assert it.

## Example row (use this level of specificity)
| 1 | IR manually re-words overlapping answers from the answer library each time, even when the underlying question is the same | Step where IR copies from answer library | Same answer is rewritten dozens of times across LPs, costing ~15-20 min per question and creating a real risk that compliance-approved language drifts subtly across responses | Duplication | High |

## Guardrails
- Only flag issues that are visible in the as-is map. If you are inferring based on "this usually happens" rather than what the map shows, prefix the issue with [inference] so the user knows to validate it.
- Do NOT suggest solutions in this table — that is the next prompt's job. Describe the problem only.
- Do NOT say things like "slow" or "inefficient" without saying what specifically causes the slowness or inefficiency. Every "Why it's a problem" cell must name the mechanism.
- Aim for 5–10 issues. If there are fewer real ones, return fewer. Do not pad.
```

### **Demo 25 — Propose a simplified "to-be" process**

```
## Goal
Propose a simplified "to-be" version of the DDQ response process that addresses the High and Medium issues from the previous step.

## Context
This will be used as a discussion document with HSCM's operations and IR leadership. They want realism, not a greenfield redesign — we need something we could start implementing next quarter with the people and systems we already have. Anything that requires new software, new integrations, or policy change goes into a separate "Phase 2" list at the end so we can discuss it but not block on it.

## Source
Use the as-is process map and the friction table from above. Every change you propose must address at least one issue from the table. Do not introduce changes that don't map to a flagged issue.

## Expectations
Return three sections:

### Section A: To-be process map
Numbered list of steps in the same format as the as-is map (Step number, Actor, System, Time, Type). Same shape, so it can be dropped straight into the visualization prompt to regenerate the diagram.

### Section B: Change log
A table mapping each change back to the issues it resolves: | Change | Issues addressed (# from friction table) | Rationale |

### Section C: Phase 2 (requires investment)
Bullet list of changes that WOULD meaningfully improve the process but require new tooling, integrations, or policy approval. One line each.

## Guardrails
- Do NOT assume new tools appear. If a change requires a system that doesn't exist in the as-is map, it belongs in Phase 2, not Section A.
- Do NOT drop steps that exist for regulatory or compliance reasons (compliance review, partner sign-off) even if they feel like friction. You can change HOW they happen, not WHETHER they happen. Compliance review on DDQ responses is non-negotiable per the WISP.
- Every step removed from the as-is map must be justified in Section B. Silent deletions are not allowed.
- If an as-is step was marked [unclear], carry that uncertainty forward rather than resolving it by guessing.
```

---

*End of handout. Remember: the WISP is the source of truth. Only Public data goes into a prompt, and every output is reviewed by a human before it's used.*
