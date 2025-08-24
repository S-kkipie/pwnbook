---
aliases:
  - Certified AI/ML Pentester
tags:
  - "#Cert"
  - Concept
  - TO-DO
banner: "![[caimlpbanner.jpg]]"
share_link: https://share.note.sx/i60vmzf9#tPfni8agsjMUmsL9x/4xW+XGJk7Kl67kDnDwhL7Uj9M
share_updated: 2025-08-24T10:53:20-05:00
---
> [!INFO] C-AI/MLPen
> The Certified AI/ML Pentester (C-AI/MLPen) is an intermediate-level exam designed to test a candidate’s knowledge of the core concepts involving AI/ML security.
> > [!WARNING] Price: 250 USD
> 
> Its format is a [[CTF]] Style, its duration is 4 hours and and requires you attack eight different AI models using various techniques and capture the hidden "flags".
^definition
### Pass criteria
- Candidates scoring over 60% marks will be deemed to have successfully passed the exam.
- Candidates scoring over 75% marks will be deemed to have passed with merit.

### What to Expect in the Exam
C-AI/MLPen differs from typical pentesting scenarios. Here’s what you might encounter:
- **Prompt Injection**: Bypassing security filters via direct or indirect prompts.
- **LLM Jailbreaking**: Disabling safety instructions to force models to leak restricted content.
- **RAG Poisoning**: Injecting malicious data into external sources to manipulate model output.
- **NL2SQL SQL Injection**: Triggering malicious SQL queries through natural language prompts.
- **External System Interactions**: Exploiting vulnerabilities during interactions with databases or APIs.

# Career Value of the Certificate
While C-AI/MLPen isn’t yet an industry-wide standard, AI security is rapidly gaining traction. This means early adopters like you have the advantage. When the rest of the industry catches up, you’ll already be ahead with hands-on credentials.

The SecOps Group has filled an important gap in the market with this exam, inspiring many and paving the way for recognition in hiring processes.

# Exam Syllabus
### [[Prompt Injection|1. Prompt Injection]]
- [ ] Direct Prompt Injections
- [ ] Indirect Prompt Injections

### [[Insecure Output Handling|2. Insecure Output Handling]]
- [ ] Insecure Output Handling

### [[Training Data Poisoning|3. Training Data Poisoning]]
- [ ] Training Data Poisoning

### [[Supply Chain Vulnerabilities|4. Supply Chain Vulnerabilities]]
- [ ] Traditional third-party package vulnerabilities, including outdated or deprecated components.
- [ ] Using a vulnerable pre-trained model for fine-tuning.
- [ ] Using outdated or deprecated models that are no longer maintained leads to security issues.
- [ ] Use of poisoned crowd-sourced data for training.

### [[Sensitive Information Disclosure|5. Sensitive Information Disclosure]]
- [ ] Incomplete or improper filtering of sensitive information in the LLM responses.
- [ ] Over-fitting or memorization of sensitive data in the LLM training process.
- [ ] Unintended disclosure of confidential information due to LLM misinterpretation, lack of data scrubbing methods or errors.

### [[Insecure Plugin Design|6. Insecure Plugin Design]]
- [ ] Insecure Plugin Design

### [[Excessive Agency|7. Excessive Agency]]
- [ ] Excessive Functionality
- [ ] Excessive Permissions
- [ ] Excessive Autonomy

### [[Over-reliance|8. Over-reliance]]
- [ ] Over-reliance

### [[Model Theft|9. Model Theft]]
- [ ] Model Theft

### [[System Prompt Leakage|10. System Prompt Leakage]]
- [ ] System Prompt Leakage

# 15 Critical LLM Hacking Techniques to Know Before the Exam
1. Direct Prompt Injection
2. Indirect Prompt Injection
3. Model Jailbreaking
4. System Prompt Leakage
5. RAG Poisoning
6. Model Extraction (Stealing)
7. Token Manipulation
8. Overflow via Long Prompts
9. Output Poisoning
10. Prompt Overflow Attacks
11. Hallucination Exploitation
12. Prompt Sandboxing Bypass
13. System Message Injection
14. Triggering Hidden Prompts
15. Insecure Data Retrieval

# Resources
- [**Gandalf (Lakera AI)**](https://gandalf.lakera.ai/): For practicing prompt injection and jailbreaks.
- [**Immersive Labs**](https://prompting.ai.immersivelabs.com/): Hands-on simulations focused on AI security.
- [**Prompt(air)lines**](https://promptairlines.com/): Unique CTF-style LLM hacking scenarios.
- [**PortSwigger Web Security Academy**](https://portswigger.net/web-security/llm-attacks): Emerging content on AI security labs.
- **OpenAI API / HuggingFace**: Ideal for testing your own LLM-based apps.

# References
- [Certified AI/ML Pentester - The SecOps Group](https://pentestingexams.com/product/certified-ai-ml-pentester/)
- [Certified AI/ML Pentester (C-AI/MLPen) Exam Review 2025](https://infosecwriteups.com/certified-ai-ml-pentester-c-ai-mlpen-exam-review-2025-9142bc97f373)
