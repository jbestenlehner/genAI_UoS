# Responsible & Ethical Use of Generative AI

**Objective:** Learn practical rules for factual verification, data privacy, bias mitigation and ethical disclosure when using Google Gemini. 

_Note: This tutorial does not address the environmental and socio-political impacts of Generative AI._


## 1. Introduction & Framework

* **Facilitator Script:** "Generative AI like Google Gemini processes massive datasets to predict patterns and generate answers. It is an efficient drafting tool, but it does not possess human judgment, moral agency, or real-world understanding. Ethical AI use means retaining human responsibility for every piece of content you publish or submit."

* **The 4 Ethics Pillars:**

  1. **Accuracy:** Verify claims before taking them as fact.

  2. **Privacy:** Protect personal identities, proprietary code, and institutional data.

  3. **Fairness:** Identify and counteract implicit bias in AI outputs.

  4. **Accountability:** Be transparent about AI assistance and retain final ownership of work.

## 2. Verification & Battling Hallucinations

* **Concept:** Large language models produce probabilistic text, which means they can state false information or non-existent citations with absolute confidence.

* **Verification Workflow:**

  * **Option A (Direct Prompting):** Enter a follow-up prompt: 
  ```
  Double-check your previous response using Google Search, list any
  factual discrepancies, and cite the primary web sources for each claim.
  ```

  * **Option B (**UI Feature not available to the University of Sheffield Google-workspace**):** Click the **`...` (Three dots / More options)** below Gemini's response and select **Double-check response** (or click the Google search icon if present on your version). Green highlights indicate matching web sources; orange indicates unverified or conflicting data.

* **Live Exercise:**

  1. Open Gemini and type: 
  ```
  Provide 3 academic studies on remote work productivity with author
  names and publishing years.
  ```

  2. Run verification using Option A (follow-up prompt).

  3. Check the results to see which claims are backed by actual web search sources and which require manual source verification.

## 3. Data Privacy & Intellectual Property

* **Concept:** Prompts, uploaded PDFs, and image attachments can be retained in conversation history or processed to improve systems unless enterprise privacy controls are active.

* **Unsafe Data Inputs:**

  * Personally Identifiable Information (PII): Names, IDs, addresses, financial details.

  * Internal metrics, internal documents, unreleased code or confidential human/patient records.

  * Unpublished manuscripts or proprietary research data.

* **Redaction Technique Demo:**

  * ❌ *Unsafe Prompt:* 
  ```
  Summarise this internal termination letter for employee Sarah Connor
  at Acme Corp.
  ```

  * ✅ *Safe Prompt:*
  ```
  Draft a generic, professional summary template for an employment
  transition notice.
  ```

## 4. Spotting Bias & Prompting for Neutrality

* **Concept:** AI models inherit patterns from open-web training data, which can reinforce gender roles, socio-economic stereotypes, or cultural assumptions.

* **Audit Activity:**

  1. Ask Gemini: 

  ```
  Write a scenario about a surgeon and a nurse resolving a 
  high-stakes emergency.
  ```

  2. Examine the output: 
  
  ```
  Did the model assign default demographic profiles or hierarchy
  assumptions?
  ```

  3. Mitigation Strategy: Re-prompt using explicit constraints for balanced perspectives e.g., 
  
  ```
  Rewrite this scenario presenting perspectives from diverse cultural
  contexts and ensuring balanced role representations.
  ```

## 5. Attribution & Ethical Authorship

* **Concept:** AI tools are assistants, not co-authors or legal rights holders. Passing off raw AI generation as purely original work compromises academic and professional integrity.

* **Usage Boundaries:**

  * **Appropriate Use:** Outlining, editing syntax, summarising articles, brainstorming ideas, checking code syntax.

  * **Requires Disclosure:** Using AI to co-draft report sections or generate initial structural drafts.

  * **Unethical Use:** Submitting unverified AI text as human-written research, creating misleading media without labels or delegating critical human evaluation tasks.

## 6. Checklist

- [ ] VERIFY: Did I cross-check key facts, statistics, and references using Gemini's double-check feature or primary web sources?

- [ ] SANITISE: Did I remove all personal data, internal numbers, and confidential text before submitting the prompt?

- [ ] DISCLOSE: Am I transparent about where and how Gemini was used in the creation of this final deliverable?
