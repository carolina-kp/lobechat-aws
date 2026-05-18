# Q4 — AI chat dump

## Session 2 — Claude Sonnet 4.6 (claude.ai), 2026-05-10UTC

**What I used AI for:** Understanding the memo structure and required sections, explaining lock-in analysis and its four types (data, model, identity, tooling), explaining why Copilot lock-in is higher than ChatGPT Enterprise despite being cheaper, explaining DORA and its practical implications for a boutique fund, deriving the 3-year TCO numbers, reviewing my draft and flagging typos and the dangling sentence, adding the EC2 downtime sentence and DevOps FTE cost to the recommendation section.

**What I kept:** The four lock-in types framework and the counter-intuitive Copilot argument (cheapest price, highest exit cost). The DORA practical framing (document, monitor, exit plan). The TCO numbers ($115,200 vs $432,000 vs $216,000). The EC2 single-instance downtime risk sentence. The DevOps 0.2 FTE at €8,000/year figure in the recommendation. The reversal trigger framing around EU-sovereign deployment options.

**What I changed:** Completed the dangling "This considered," sentence. Corrected all typos throughout. Added the appendix pointing to Q3 cost model. Kept the lock-in section prose in my own voice rather than accepting AI rewrite of whole paragraphs.

**What I rejected:** AI rewrote the entire memo in a polished corporate register that no longer sounded like me. I rejected that version and asked for only specific targeted fixes applied to my original text instead.

**Prompts and responses:** Full conversation transcript below.

---


now lets get started with q4

14:51
Claude responded: Q4 is a memo, so format matters as much as content.
Q4 is a memo, so format matters as much as content. Before you draft, lock in your position and your structure.

Your position based on everything we have built:

Defend self-hosting, but with explicit conditions. Not "self-hosting is always better" but "self-host if X, Y, Z, otherwise buy." The nuance from Q3 makes this credible: you have the numbers to show it only works at 100+ MAU with DevOps capacity.

The required memo structure:

TO / FROM / DATE / SUBJECT header
TL;DR (3 bullets)
Body:
  1. 3-year TCO comparison
  2. Lock-in analysis
  3. Data sovereignty + compliance
  4. Capability gap
  5. Recommendation with explicit conditions
  6. Reversal trigger
Appendix (your Q3 tables)
The numbers you already have for TCO:

At 200 users over 3 years:

Self-hosted: $16/user/month x 200 x 36 = $115,200 total
ChatGPT Enterprise: $60/user/month x 200 x 36 = $432,000 total
Copilot: $30/user/month x 200 x 36 = $216,000 total
Self-hosting saves $316,800 vs ChatGPT and $100,800 vs Copilot over 3 years at 200 users. Those are your headline TCO numbers.

Before you draft, one decision: which sector are you using for the compliance section? You have been using finance throughout, so MiFID II + GDPR + DORA is your set. Confirm that and then draft. Ready?

You said: yes finance sector, mifid gdpr and dora, can you explain what lockin analysis is
yes finance sector, mifid gdpr and dora, can you explain what lockin analysis is

15:06
Claude responded: Lock-in analysis is an assessment of how difficult and costly it would be to switch away from each option if you wanted to leave.
Lock-in analysis is an assessment of how difficult and costly it would be to switch away from each option if you wanted to leave.

For each of the three options (self-hosted, ChatGPT Enterprise, Copilot) you analyse four types of lock-in:

Data lock-in Where does your data live and how hard is it to get out? With self-hosted your Postgres database, Qdrant vectors, and MinIO files are all on your own infrastructure. You can export everything at any time with no permission needed and no egress fee beyond AWS data transfer. With ChatGPT Enterprise your conversation history and any fine-tuning data lives on OpenAI servers. Export tools exist but the format is OpenAI-specific and you are dependent on their export API remaining available. With Copilot your data sits in Microsoft 365 tenant storage, tightly coupled to the Microsoft ecosystem.

Identity lock-in Who controls user authentication? With self-hosted Casdoor manages SSO and you own the identity store entirely. With ChatGPT Enterprise identity is managed through OpenAI's platform, potentially federated with your IdP but still dependent on OpenAI's auth layer remaining compatible. With Copilot identity is Azure AD, which is deeply integrated into Microsoft 365 and very hard to migrate away from.

Model lock-in Are you dependent on one model provider? With self-hosted you can swap models via OpenRouter or direct API with a config change. If Anthropic raises prices or degrades quality you switch to Gemini or a local model with minimal disruption. With ChatGPT Enterprise you are locked to OpenAI's model roadmap. If GPT-5 performs worse than GPT-4 on your use case you have no alternative within the platform. With Copilot you are locked to whatever Microsoft decides to serve.

Tooling lock-in How portable are your custom integrations? With self-hosted your MCP tools, Hayhooks pipelines, and Qdrant embeddings are built on open standards. Moving to a different hosting environment means redeploying the same containers, not rebuilding from scratch. With ChatGPT Enterprise any custom GPTs or plugins are built on OpenAI-specific APIs. With Copilot custom extensions use Microsoft's Graph API and Power Platform, which are not portable outside the Microsoft ecosystem.

Exit cost for each option:

Self-hosted: low. Your data is yours, your tooling is open, switching means redirecting DNS and redeploying elsewhere.

ChatGPT Enterprise: medium. Data export is possible but conversation history and any embeddings stored in OpenAI's systems need manual extraction. Custom GPT logic needs to be rebuilt.

Copilot: high. Azure AD dependency, Microsoft 365 integration, and Power Platform extensions create deep switching costs that go beyond the AI tool itself into core IT infrastructure.

In your memo, lock-in analysis is one section of the body, roughly 150-200 words. You do not need to go as deep as I just did. A table with the four lock-in types and a rating per option plus one paragraph of narrative is enough. Want to start drafting now?

You said: so copilot lock-in is actually worse than chatgpt enterprise lock-in even though chatgpt is more expensive.
so copilot lock-in is actually worse than chatgpt enterprise lock-in even though chatgpt is more expensive. is that a fair argument to make in the memo?

15:08
Claude responded: Yes, absolutely fair, and it is actually a non-obvious trade-off that will score well.
Yes, absolutely fair, and it is actually a non-obvious trade-off that will score well.

The argument is: ChatGPT Enterprise at $60/user is expensive but the exit cost is relatively contained. Your data is in OpenAI's system but the surface area of lock-in is limited to the AI layer. If you want to leave you export your conversation history, rebuild your custom GPTs elsewhere, and redirect your users to a new tool. Painful but bounded.

Copilot at $30/user looks cheaper but the lock-in is structural. It is not just an AI tool, it is an AI layer built on top of Azure AD, Microsoft 365, SharePoint, Teams, and Power Platform. By the time you have integrated Copilot deeply into your workflow the switching cost is not "find a new AI tool," it is "potentially migrate your entire productivity stack." For a boutique asset manager that probably already runs on Microsoft 365 this is a real risk because the Copilot integration will deepen an existing dependency rather than create a new standalone one.

So the argument in the memo is: Copilot has the lowest headline price but the highest exit cost because lock-in extends beyond the AI layer into core IT infrastructure. ChatGPT Enterprise has the highest headline price but a more bounded lock-in surface. Self-hosted has the lowest exit cost of all three because data, identity, models, and tooling are all under your control.

This is a genuinely interesting trade-off because it inverts the intuitive price-to-risk ordering. Most people assume more expensive means more lock-in. Here the cheapest option has the deepest lock-in. That kind of counter-intuitive observation is exactly what Level 3 rewards.

One caveat to include for honesty: if the firm already runs on Microsoft 365 and has no intention of leaving that ecosystem, Copilot lock-in is irrelevant because the dependency already exists. In that scenario Copilot is actually the rational buy option and you should say so. That conditional framing makes the argument more credible, not less.

Ready to draft?

You said: yesm i will draf and ask for feedback
yesm i will draf and ask for feedback

15:10
Claude responded: Perfect.
Perfect. Draft it and paste it here. I will review against the rubric and the required content checklist:

Memo format correct (To/From/Date/Subject header, not academic prose)
TL;DR 3 bullets at the top
3-year TCO comparison with your numbers ($115,200 vs $432,000 vs $216,000)
Lock-in analysis covering all four types with exit cost per option
Data sovereignty and compliance covering MiFID II, GDPR Article 28, DORA
Capability gap both directions (what self-hosted does that SaaS does not, and vice versa)
Recommendation with explicit conditions ("self-host if X, Y, Z, otherwise buy")
Reversal trigger
Take your time.

You said: wait, sint Data sovereignty and compliance covering MiFID II, GDPR Article 28, DORA
wait, sint Data sovereignty and compliance covering MiFID II, GDPR Article 28, DORA

Capability gap both directions (what self-hosted does that SaaS does not, and vice versa) this same as in q1, can i use that content, rewrite it a bit but is basically the same ,no?
15:52
Claude responded: Yes and no.
Yes and no. The content overlaps but the framing is completely different and that matters.

In Q1 you used the capability gap to justify why this stack is better than ChatGPT for the specific boutique fund use case. It was descriptive: here is what the stack can do, here is the workflow, here is why it fits.

In Q4 the capability gap is part of an executive decision memo. The framing is evaluative not descriptive: here is what self-hosting gives you that SaaS cannot, here is what SaaS gives you that self-hosting cannot, and here is the weight I assign to each in making a buy vs build recommendation. It needs to acknowledge both sides honestly, not just argue for self-hosting.

So the raw content is similar but you need to:

Add the "what SaaS does better" side which you barely touched in Q1. The assignment explicitly requires this. The honest SaaS advantages are: higher uptime SLA (OpenAI guarantees 99.9%, your EC2 does not), mobile apps, automatic model upgrades without your DevOps involvement, 24/7 vendor support, and zero maintenance burden.

Reframe everything as a trade-off table or weighted comparison rather than a one-sided argument.

Keep it shorter than Q1 since the memo format demands concision. In Q1 you had 800-1500 words for the whole answer. In Q4 the capability gap is one section of a memo, so 150-200 words maximum.

So: borrow the ideas, rewrite the framing, add the SaaS advantages side, cut the length. Do not copy-paste directly.

You said: this is the draft i have done, it should be addressed to the cto, no?

FROM: Carolina Kogan DATE: May 2026 SUBJECT: Build vs Buy - AI Platform Decision TL;DR (3 bullets) Self-hosting saves $316,800 vs ChatGPT Enterprise and $100,800 vs Copilot over 3 years at 200 users, while keeping full control over data, audit trails, and model selection no generic one-size-fi

pasted

this is the draft i have done, it should be addressed to the cto, no? . also tell me what nreeds refinement and aits i think 1292 words, is that ok?

16:33
Claude responded: Yes, it should be addressed to the CTO.
Yes, it should be addressed to the CTO. Add "TO: Chief Technology Officer" at the top of the header. That is a one-second fix.

1292 words is perfect. The assignment says approximately 1000 words and you are within range without padding.

What is working well:

The TCO numbers are clean and the conclusion is immediate. The lock-in inversion argument (Copilot cheapest but highest exit cost) is there and well-reasoned. The compliance section is precise with the right citations. The capability gap correctly covers both sides. The recommendation has explicit conditions. The reversal trigger is specific and credible.

What needs refinement:

Lock-in section: This is your weakest section, not because the content is wrong but because the writing is the roughest in the document. Sentences like "which rises same issues of privacy and sensitive information leaking as stated before" and "selfhosting allows us to have vendor specific features so we give more tailored and accurate responses/actions fro our task" are unclear and would not go in a CTO memo. The ideas are right but the language needs to be tightened to match the professional register of the rest of the document. You do not need to rewrite the whole section, just clean the prose so it reads like a memo not a draft.

The Copilot lock-in paragraph ends mid-thought. "This considered," has no conclusion after it. Either complete the sentence or cut it. A memo cannot have a dangling thought.

Data sovereignty section is good but slightly repetitive with Q1. In a memo this is fine since the CTO may not have read Q1, but tighten it. The three regulations are all cited correctly which is what matters.

Capability gap: The line "full stop" is good. The SaaS advantages paragraph is honest and well-framed. One thing missing: you do not mention uptime SLA numbers. You say "our EC2 has no SLA" which is correct but you should add what the self-hosted risk actually means in practice. One sentence: "A single-instance EC2 deployment has no redundancy, meaning any hardware failure or AWS AZ outage causes full platform downtime until manually recovered." That makes the SaaS uptime advantage concrete rather than abstract.

Recommendation section: Solid. The buy/self-host conditions are clear and specific. One small addition: add a sentence on what "has or can hire DevOps capacity" means in practice, 0.2 FTE at roughly €8,000/year, so the CTO knows what they are actually committing to.

Spelling and register fixes needed throughout:

"responsable" should be "responsible"
"equivelant" should be "equivalent"
"confort" should be "comfort"
"operationnal" should be "operational"
"convinience" should be "convenience"
"mau" should be "MAU" throughout
"opena" should be "OpenAI"
"eusovereign" should be "EU-sovereign"
"saasbecomes" should be "SaaS becomes"
"mifid ii" should be "MiFID II" throughout
"openai" should be "OpenAI" throughout
One structural note: The memo currently has no appendix. The assignment says to include one. A one-line appendix pointing to your Q3 cost tables is enough: "Appendix A: Full cost model and pricing assumptions available in docs/evidence/q3/a3.md."

Fix the dangling Copilot sentence, clean the lock-in prose, add the EC2 downtime sentence, add the DevOps FTE cost to the recommendation, add the appendix, and run a spell-check. Then this is done.

You said: ok apply all of those fixes , fix my typos etc and return to me the final text.
ok apply all of those fixes , fix my typos etc and return to me the final text.

16:54
markdown
TO: Chief Technology Officer
FROM: Carolina Kogan
DATE: May 2026
SUBJECT: Build vs Buy — AI Platform Decision

---

**TL;DR**
- Self-hosting saves $316,800 vs ChatGPT Enterprise and $100,800 vs Copilot over 3 years at 200 users, while keeping full control over data, audit trails, and model selection with no generic one-size-fits-all interface.
- MiFID II Article 16 requires client communications to remain under the firm's control. Using ChatGPT sends that data to OpenAI servers, which is a potential regulatory breach. Self-hosting eliminates that risk entirely.
- Self-hosting only makes economic sense if the firm commits to 100+ monthly active users and has DevOps capacity. At smaller scale the cost advantage disappears and SaaS becomes the rational choice.

---

**1. 3-Year TCO Comparison**

At 200 users over 3 years:
- Self-hosted: $16/user/month x 200 x 36 = **$115,200 total**
- ChatGPT Enterprise: $60/user/month x 200 x 36 = **$432,000 total**
- Copilot: $30/user/month x 200 x 36 = **$216,000 total**

Self-hosting saves $316,800 vs ChatGPT and $100,800 vs Copilot over 3 years at 200 users. The self-hosted figure includes infrastructure, LLM token costs, and 0.2 FTE DevOps labour at €40,000/year fully loaded. Full cost model in Appendix A.

---

**2. Lock-In Analysis**

**Data lock-in:** When self-hosting, MinIO files, Qdrant vectors, and the Postgres database all live on the firm's own infrastructure. Everything can be exported at any time without permission or egress fees beyond standard AWS data transfer costs. With ChatGPT Enterprise, conversation history and any fine-tuning data live on OpenAI servers. Export tools exist but the format is OpenAI-specific and depends on their export API remaining accessible. Copilot stores data in Microsoft 365 tenant storage, tightly coupled to the Microsoft ecosystem and subject to the same third-party control risks.

**Model lock-in:** When self-hosted, models can be switched via OpenRouter or direct API with a configuration change. If Anthropic raises prices or a competitor offers better performance, the switch requires no platform migration. With ChatGPT Enterprise you are locked to OpenAI's model roadmap with no alternatives within the platform. With Copilot you are locked to whatever Microsoft chooses to serve.

**Identity lock-in:** Self-hosting gives the firm complete control over authentication. Casdoor manages SSO and owns the identity store entirely. ChatGPT Enterprise identity may be federated with your IdP but remains dependent on OpenAI's auth layer staying compatible. Copilot identity runs on Azure AD, which is deeply integrated into Microsoft 365 and carries significant migration complexity.

**Tooling lock-in:** Self-hosted MCP tools, Hayhooks pipelines, and Qdrant embeddings are built on open standards. Switching hosting environments means redeploying the same containers, not rebuilding from scratch. Custom GPTs in ChatGPT Enterprise are built on OpenAI-specific APIs. Copilot extensions use Microsoft's Graph API and Power Platform, which are not portable outside the Microsoft ecosystem.

**Exit cost per option:**
- Self-hosted: low. Data is yours, tooling is open, switching means redeploying containers and redirecting DNS.
- ChatGPT Enterprise: moderate. Data export is possible but conversation history and embeddings require manual extraction and custom GPT logic must be rebuilt.
- Copilot: high. Azure AD dependency, Microsoft 365 integration, and Power Platform extensions create switching costs that extend well beyond the AI tool into core IT infrastructure.

The counter-intuitive finding here is that Copilot, the cheapest option at $30/user, carries the highest exit cost because lock-in extends into the firm's entire productivity stack. If the firm already runs on Microsoft 365 and has no intention of leaving that ecosystem, Copilot lock-in is largely irrelevant and the buy case strengthens considerably.

---

**3. Data Sovereignty and Compliance**

With self-hosted AI, data sovereignty stays with the firm. MiFID II Article 16 requires investment firms to retain client-related communications under their own control. If chat logs live on OpenAI servers, the firm may not have full retrieval control when a regulator demands it. GDPR Article 28 requires a Data Processing Agreement when client PII is sent to a third-party processor such as OpenAI. Most EU compliance teams at regulated firms will not approve this regardless of what the DPA says. DORA, in force since January 2025, requires EU financial entities to document, monitor, and maintain an exit plan for every critical ICT third-party dependency. If OpenAI changes its pricing, gets acquired, or goes down, the firm needs documented proof of continuous monitoring and a ready exit plan. Self-hosting eliminates OpenAI as a critical third-party entirely, so there is nothing to register, monitor, or exit.

---

**4. Capability Gap**

Self-hosting wins decisively on the capabilities that matter most for this firm. RAG over Qdrant makes the entire internal research corpus permanently searchable without ever entering a prompt. Ten years of investment memos, regulatory filings, and internal research notes become instantly queryable. ChatGPT has no equivalent for a continuously growing proprietary corpus. Per-assistant configuration means each persona gets a tailored assistant with its own default model, enabled tools, and system prompt. The analyst gets Sonnet with Qdrant and Hayhooks enabled, the RM gets Haiku with just the portfolio filesystem tool, and the compliance officer gets a read-only log view. ChatGPT gives everyone the same interface and the same model, full stop.

That said, SaaS wins on operational comfort. ChatGPT Enterprise and Copilot both offer 99.9% uptime SLAs. The self-hosted stack runs on a single EC2 instance with no redundancy, meaning any hardware failure or AWS availability zone outage causes full platform downtime until manually recovered. Both SaaS options also offer mobile apps, automatic model upgrades with no DevOps involvement, and 24/7 vendor support. For a firm with no internal DevOps capacity these are not minor conveniences, they are real operational advantages.

For a boutique fund under CNMV supervision the trade-off is clear. The RAG capability, audit trail ownership, and regulatory compliance requirements outweigh the SaaS operational convenience. A firm that cannot afford a MiFID II finding caused by an AI tool it does not control has limited room to choose otherwise. This stack makes the AI not just useful but auditable.

---

**5. Recommendation**

**Self-host if:** the firm commits to 100+ MAU from day one, has or can allocate DevOps capacity (0.2 FTE, approximately €8,000/year), and operates under MiFID II or similar regulation that makes sending client data to third-party servers legally risky. Self-host also if the firm requires model flexibility and custom RAG over internal documents that no SaaS tool can replicate.

**Buy if:** the firm wants a pilot under 50 users, has no DevOps capacity, or can obtain legal sign-off on a Data Processing Agreement with OpenAI. Also buy if the primary need is convenience, mobile access, and guaranteed uptime over compliance and customisation.

---

**6. Reversal Trigger**

If OpenAI or Anthropic launch an EU-sovereign deployment option with MiFID II-compliant audit logs and on-premise data residency, the regulatory argument for self-hosting collapses and SaaS becomes the dominant choice even at scale. Monitor this space actively, particularly given the pace of EU AI Act implementation and sovereign cloud investment in 2025-2026.

---

**Appendix A:** Full cost model, assumptions table, and line-item pricing breakdown available in docs/evidence/q3/a3.md.
You said: but wait, this is too polished and dsnt sound like me anymore.
but wait, this is too polished and dsnt sound like me anymore. can you take my ogtext and apply only the specific fixes you said without rewriting whole sentnces or adding new content that wasnt in my draft unless necessary? it has to be written by me , not fully ai

16:58
Claude responded: You are right, my bad.
You are right, my bad. Here is your original text with only the specific fixes applied: typos corrected, the dangling "This considered," completed, the EC2 downtime sentence added, the DevOps FTE cost added to the recommendation, and the appendix added. Nothing else rewritten.

TO: Chief Technology Officer
FROM: Carolina Kogan
DATE: May 2026
SUBJECT: Build vs Buy - AI Platform Decision

TL;DR

Self-hosting saves $316,800 vs ChatGPT Enterprise and $100,800 vs Copilot over 3 years at 200 users, while keeping full control over data, audit trails, and model selection with no generic one-size-fits-all interface.
MiFID II Article 16 requires client communications to remain under the firm's control. Using ChatGPT sends that data to OpenAI servers, which is a potential regulatory breach. Self-hosting eliminates that risk entirely.
Self-hosting only makes economic sense if the firm commits to 100+ monthly active users and has DevOps capacity. At smaller scale the cost advantage disappears and SaaS becomes the rational choice.
Body:

1. 3-year TCO comparison

At 200 users over 3 years:

Self-hosted: $16/user/month x 200 x 36 = $115,200 total
ChatGPT Enterprise: $60/user/month x 200 x 36 = $432,000 total
Copilot: $30/user/month x 200 x 36 = $216,000 total
Self-hosting saves $316,800 vs ChatGPT and $100,800 vs Copilot over 3 years at 200 users.

2. Lock-in analysis

Analyzing data locking, when self-hosting, as the name states MinIO files, Qdrant vectors, and your Postgres database are all hosted on your own infrastructure. So for information and context usage, this method is more efficient when iterating over years of data. Beyond AWS data transfer, one can also export anything at any moment without permission and without paying an egress fee. Where them not to self-host, the chat history and any fine-tuning data would be stored on OpenAI servers while using ChatGPT Enterprise. Although there are export tools, the format would still be unique to OpenAI, which might not satisfy the team's needs, and you have to rely on their export API staying accessible. Copilot keeps your data in Microsoft 365 tenant storage, which is closely linked to the Microsoft network, which raises the same issues of privacy and sensitive information leaking as stated before.

Then model locking means being dependent on one model provider. When self-hosting one alternates with the best model for each task, making it also more efficient token-wise. Models can be switched using OpenRouter, Bedrock or the direct API with a configuration update when self-hosted. So one can easily switch to Gemini or a local model if Anthropic or other competitors increase prices or lower quality. Using ChatGPT Enterprise you are restricted to OpenAI's model roadmap. There are no other options on the platform if GPT-5 performs worse than GPT-4 in your use case. And similar with Copilot, one would be restricted to anything Microsoft chooses to offer.

Identity locking refers to the control of authentication. Self-hosting allows the company more control user-wise. Casdoor controls SSO and gives you complete control over the identity store. When not self-hosting, OpenAI's platform is used to handle ChatGPT Enterprise identity; it may be federated with your IdP, but it still depends on OpenAI's auth layer being compliant. Similarly, Azure AD is a Copilot identity that is intricately linked to Microsoft 365 and difficult to disconnect from.

And tooling locking relates to custom integrations and how portable they are. Self-hosting allows us to have vendor-specific features so we give more tailored and accurate responses and actions for our task. Hayhooks pipelines, Qdrant embeddings, and self-hosted MCP tools are all based on open standards so redeploying the same containers rather than starting from scratch is necessary when switching to a new hosting environment. However, any custom GPTs or plugins created with ChatGPT Enterprise are based on APIs unique to OpenAI. Microsoft's Graph API and Power Platform, which are not transferable outside of the Microsoft ecosystem, are used by Copilot custom extensions.

Each option's exit cost:

Self-hosted: low. Your tooling is open, your data is yours, and moving entails redeploying and rerouting DNS.
ChatGPT Enterprise: moderate. Conversation history and any embeddings kept in OpenAI's systems must be manually extracted, however data export is feasible. Custom GPT logic needs to be rebuilt.
Copilot: high. Deep switching costs that extend beyond the AI tool itself into essential IT infrastructure are caused by Azure AD reliance, Microsoft 365 integration, and Power Platform extensions.
Copilot has the lowest headline pricing but the highest exit cost since lock-in extends beyond the AI layer into core IT infrastructure. ChatGPT Enterprise has the highest headline pricing despite having a more limited lock-in surface. Of the three, self-hosted offers the lowest exit cost since you have control over data, identity, models, and tooling. The least priced option in this situation has the strongest lock-in. Since the firm already utilizes Microsoft 365 and has no intention of leaving that ecosystem, Copilot lock-in is arguably negligible and in that scenario the buy case strengthens considerably.

3. Data sovereignty and compliance

With a self-hosted AI, data sovereignty stays with the company. With ChatGPT, OpenAI servers are responsible for it. MiFID II Article 16 requires investment firms to keep client-related communications under their own control. If chat logs are stored on OpenAI's servers, you may not have complete control over retrieval when a regulator requests it. GDPR Article 28 requires a DPA when client data goes to a third-party processor like OpenAI, and most EU compliance teams at regulated firms won't sign off on this regardless of what the DPA says. DORA, which came into force in January 2025, requires EU financial firms to document, monitor and have an exit plan ready for any critical third-party tech dependency. If OpenAI changes its pricing, gets acquired, or goes down, the firm needs proof of continuous monitoring and a documented exit plan.

4. Capability gap

Self-hosting wins on capability where it matters for this firm. RAG over Qdrant makes the entire internal research corpus permanently searchable without ever entering a prompt. You can't paste 10 years of memos into a context window each time and ChatGPT has no equivalent. Per-assistant configuration means each persona gets a tailored assistant with its own default model, enabled tools and system prompt. The analyst gets Sonnet with Qdrant and Hayhooks, the RM gets Haiku with just the portfolio tool, and the compliance officer gets a read-only log view. ChatGPT gives everyone the same interface and the same model, full stop.

That said, SaaS wins on operational comfort. ChatGPT Enterprise and Copilot both offer 99.9% uptime SLAs. The self-hosted stack runs on a single EC2 instance with no redundancy, meaning any hardware failure or AWS availability zone outage causes full platform downtime until manually recovered. Both SaaS options have mobile apps, automatic model upgrades with no DevOps involvement, and 24/7 vendor support. For a firm with no internal DevOps capacity these are not minor conveniences, they are real operational advantages.

For a boutique fund under CNMV supervision the trade-off is clear. The RAG capability, audit trail, and regulatory compliance requirements outweigh the SaaS operational convenience. A firm that cannot afford a MiFID II finding caused by an AI tool it doesn't control has no real choice here. This stack makes the AI not just useful but auditable.

5. Recommendation with explicit conditions

Self-host if: the firm commits to 100+ MAU from day one, has or can hire a DevOps engineer that can maintain the stack (0.2 FTE, approximately €8,000/year), and operates under MiFID II or similar regulation that makes sending client data to third-party servers legally risky. Self-host also if the firm needs model flexibility and custom RAG over internal documents that no SaaS tool can replicate.

Buy if: the firm wants a small pilot under 50 users, has no DevOps capacity, or can get legal sign-off on a data processing agreement with OpenAI. Also buy if the primary need is convenience and mobile access over compliance and customisation.

6. Reversal trigger

If OpenAI or Anthropic launch an EU-sovereign deployment option with MiFID II-compliant audit logs and on-premise data residency, the regulatory argument for self-hosting collapses and SaaS becomes the dominant choice even at scale.

Appendix A: Full cost model and pricing assumptions available in docs/evidence/q3/a3.md.

<!--
  Q4 — Build vs buy memo to the CTO.
  See docs/FINAL-PROJECT.md §3 Q4 for the full prompt and required sections.
  Length: ~1000 words (memo format, not academic prose).

  Required sections (use as headings below):
    - TL;DR
    - 3-year TCO comparison (200 users)
    - Lock-in analysis
    - Data sovereignty + compliance
    - Capability gap
    - Recommendation
    - Reversal trigger
    - Appendix

  Replace this placeholder content. Remove these HTML comments before
  submission.
-->

**To:** CTO
**From:** TODO
**Date:** TODO
**Subject:** Build vs buy — LobeChat self-hosted vs SaaS AI assistants

# TL;DR

- TODO
- TODO
- TODO

# 3-year TCO comparison (200 users)

TODO

# Lock-in analysis

TODO

# Data sovereignty + compliance

TODO

# Capability gap

TODO

# Recommendation

TODO

# Reversal trigger

TODO

# Appendix

TODO
 i need to complete this with what i just sent you, do it annd return it to me copy paste
Show more
17:02
markdown
**To:** CTO
**From:** Carolina Kogan
**Date:** May 2026
**Subject:** Build vs buy — LobeChat self-hosted vs SaaS AI assistants

# TL;DR

- Self-hosting saves $316,800 vs ChatGPT Enterprise and $100,800 vs Copilot over 3 years at 200 users, while keeping full control over data, audit trails, and model selection with no generic one-size-fits-all interface.
- MiFID II Article 16 requires client communications to remain under the firm's control. Using ChatGPT sends that data to OpenAI servers, which is a potential regulatory breach. Self-hosting eliminates that risk entirely.
- Self-hosting only makes economic sense if the firm commits to 100+ monthly active users and has DevOps capacity. At smaller scale the cost advantage disappears and SaaS becomes the rational choice.

# 3-year TCO comparison (200 users)

At 200 users over 3 years:
- Self-hosted: $16/user/month x 200 x 36 = $115,200 total
- ChatGPT Enterprise: $60/user/month x 200 x 36 = $432,000 total
- Copilot: $30/user/month x 200 x 36 = $216,000 total

Self-hosting saves $316,800 vs ChatGPT and $100,800 vs Copilot over 3 years at 200 users.

# Lock-in analysis

Analyzing data locking, when self-hosting, as the name states MinIO files, Qdrant vectors, and your Postgres database are all hosted on your own infrastructure. So for information and context usage, this method is more efficient when iterating over years of data. Beyond AWS data transfer, one can also export anything at any moment without permission and without paying an egress fee. Where them not to self-host, the chat history and any fine-tuning data would be stored on OpenAI servers while using ChatGPT Enterprise. Although there are export tools, the format would still be unique to OpenAI, which might not satisfy the team's needs, and you have to rely on their export API staying accessible. Copilot keeps your data in Microsoft 365 tenant storage, which is closely linked to the Microsoft network, which raises the same issues of privacy and sensitive information leaking as stated before.

Then model locking means being dependent on one model provider. When self-hosting one alternates with the best model for each task, making it also more efficient token-wise. Models can be switched using OpenRouter, Bedrock or the direct API with a configuration update when self-hosted. So one can easily switch to Gemini or a local model if Anthropic or other competitors increase prices or lower quality. Using ChatGPT Enterprise you are restricted to OpenAI's model roadmap. There are no other options on the platform if GPT-5 performs worse than GPT-4 in your use case. And similar with Copilot, one would be restricted to anything Microsoft chooses to offer.

Identity locking refers to the control of authentication. Self-hosting allows the company more control user-wise. Casdoor controls SSO and gives you complete control over the identity store. When not self-hosting, OpenAI's platform is used to handle ChatGPT Enterprise identity; it may be federated with your IdP, but it still depends on OpenAI's auth layer being compliant. Similarly, Azure AD is a Copilot identity that is intricately linked to Microsoft 365 and difficult to disconnect from.

And tooling locking relates to custom integrations and how portable they are. Self-hosting allows us to have vendor-specific features so we give more tailored and accurate responses and actions for our task. Hayhooks pipelines, Qdrant embeddings, and self-hosted MCP tools are all based on open standards so redeploying the same containers rather than starting from scratch is necessary when switching to a new hosting environment. However, any custom GPTs or plugins created with ChatGPT Enterprise are based on APIs unique to OpenAI. Microsoft's Graph API and Power Platform, which are not transferable outside of the Microsoft ecosystem, are used by Copilot custom extensions.

Each option's exit cost:
- Self-hosted: low. Your tooling is open, your data is yours, and moving entails redeploying and rerouting DNS.
- ChatGPT Enterprise: moderate. Conversation history and any embeddings kept in OpenAI's systems must be manually extracted, however data export is feasible. Custom GPT logic needs to be rebuilt.
- Copilot: high. Deep switching costs that extend beyond the AI tool itself into essential IT infrastructure are caused by Azure AD reliance, Microsoft 365 integration, and Power Platform extensions.

Copilot has the lowest headline pricing but the highest exit cost since lock-in extends beyond the AI layer into core IT infrastructure. ChatGPT Enterprise has the highest headline pricing despite having a more limited lock-in surface. Of the three, self-hosted offers the lowest exit cost since you have control over data, identity, models, and tooling. The least priced option in this situation has the strongest lock-in. Since the firm already utilizes Microsoft 365 and has no intention of leaving that ecosystem, Copilot lock-in is arguably negligible and in that scenario the buy case strengthens considerably.

# Data sovereignty + compliance

With a self-hosted AI, data sovereignty stays with the company. With ChatGPT, OpenAI servers are responsible for it. MiFID II Article 16 requires investment firms to keep client-related communications under their own control. If chat logs are stored on OpenAI's servers, you may not have complete control over retrieval when a regulator requests it. GDPR Article 28 requires a DPA when client data goes to a third-party processor like OpenAI, and most EU compliance teams at regulated firms won't sign off on this regardless of what the DPA says. DORA, which came into force in January 2025, requires EU financial firms to document, monitor and have an exit plan ready for any critical third-party tech dependency. If OpenAI changes its pricing, gets acquired, or goes down, the firm needs proof of continuous monitoring and a documented exit plan.

# Capability gap

Self-hosting wins on capability where it matters for this firm. RAG over Qdrant makes the entire internal research corpus permanently searchable without ever entering a prompt. You can't paste 10 years of memos into a context window each time and ChatGPT has no equivalent. Per-assistant configuration means each persona gets a tailored assistant with its own default model, enabled tools and system prompt. The analyst gets Sonnet with Qdrant and Hayhooks, the RM gets Haiku with just the portfolio tool, and the compliance officer gets a read-only log view. ChatGPT gives everyone the same interface and the same model, full stop.

That said, SaaS wins on operational comfort. ChatGPT Enterprise and Copilot both offer 99.9% uptime SLAs. The self-hosted stack runs on a single EC2 instance with no redundancy, meaning any hardware failure or AWS availability zone outage causes full platform downtime until manually recovered. Both SaaS options have mobile apps, automatic model upgrades with no DevOps involvement, and 24/7 vendor support. For a firm with no internal DevOps capacity these are not minor conveniences, they are real operational advantages.

For a boutique fund under CNMV supervision the trade-off is clear. The RAG capability, audit trail, and regulatory compliance requirements outweigh the SaaS operational convenience. A firm that cannot afford a MiFID II finding caused by an AI tool it doesn't control has no real choice here. This stack makes the AI not just useful but auditable.

# Recommendation

Self-host if: the firm commits to 100+ MAU from day one, has or can hire a DevOps engineer that can maintain the stack (0.2 FTE, approximately €8,000/year), and operates under MiFID II or similar regulation that makes sending client data to third-party servers legally risky. Self-host also if the firm needs model flexibility and custom RAG over internal documents that no SaaS tool can replicate.

Buy if: the firm wants a small pilot under 50 users, has no DevOps capacity, or can get legal sign-off on a data processing agreement with OpenAI. Also buy if the primary need is convenience and mobile access over compliance and customisation.

# Reversal trigger

If OpenAI or Anthropic launch an EU-sovereign deployment option with MiFID II-compliant audit logs and on-premise data residency, the regulatory argument for self-hosting collapses and SaaS becomes the dominant choice even at scale.

# Appendix

Appendix A: Full cost model and pricing assumptions available in docs/evidence/q3/a3.md.

---

