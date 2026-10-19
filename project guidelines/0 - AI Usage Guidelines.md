# AI Usage Declaration Guidelines (All Project Milestones)

You may use generative AI tools in the term project, provided you declare that use fully. These rules apply to **every milestone (1–7)** and **every team member**.

## 1. Key Rules
- **Every milestone requires a declaration**, whether or not AI was used. **No declaration = 0** for the milestone.
- **Every member declares individually.** A missing member declaration = 0 for that member.
- **If you used AI, submit full evidence:** complete conversations and intermediate artifacts. Missing, partial, or summarized evidence is treated as no declaration (0).
- **If you did not use AI, declare it explicitly.** A false "No AI" declaration, or undeclared AI use, is treated as **plagiarism** under KFUPM regulations. Edited or fabricated logs are treated as falsification.
- **Declared use within the permitted scope is not penalized.** The work is graded with the milestone rubric. Use outside the permitted scope (Section 3) is graded on the team's own contribution only.
- **You own your work.** Any member may be asked to explain or modify their contribution, including AI-assisted parts. AI errors are not an excuse. AI-detection tools alone will not decide integrity cases.
- **Amendments:** forgotten AI use can be declared, with evidence, by email before the milestone's grades are released, without penalty.

## 2. What Counts as AI Use
When in doubt, declare it. This includes, but is not limited to:
- Chat assistants (e.g., ChatGPT, Claude, Gemini).
- Coding assistants and agents (e.g., GitHub Copilot, Cursor), **including accepted autocomplete suggestions**.
- UI and design generators (e.g., v0, Figma AI).
- Image, video, and voice generators.
- Writing, slide, and translation tools (e.g., Grammarly rewrite, Copilot in PowerPoint).
- AI-generated search answers (e.g., Google AI Overviews).

No declaration is needed for basic spell-check, non-AI linters and formatters, official documentation, or regular search results. Code reused from Stack Overflow, GitHub, or tutorials is not AI use, but must be acknowledged as reused code.

## 3. What Is Permitted
The project follows Level 3, "AI Collaboration", of the AI Assessment Scale [1]: AI may support idea generation, drafting, feedback, and debugging, but the team must direct, evaluate, and own the work.

**Not allowed, even if declared:**
- Generating a whole deliverable (slides, requirements, app) from a few prompts with little team work.
- Presenting AI-fabricated data, user research, or references as real.
- Submitting AI-produced work you cannot explain.
- Sharing secrets (API keys, `.env` content, database URIs, passwords) or other people's personal data with AI tools.
- Committing code on behalf of another member.

## 4. What to Submit
Submit on Blackboard with each milestone:

| File | Required | File name |
|------|----------|-----------|
| AI Declaration (PDF), using the [template](./0%20-%20AI%20Declaration%20Template.md) | Always | `Team [N] SWE 363-[SEC] - Phase [P] - AI Declaration.pdf` |
| AI Evidence (ZIP) | If any member used AI | `Team [N] SWE 363-[SEC] - Phase [P] - AI Evidence.zip` |

**Evidence requirements:**
- **Conversations:** every conversation, complete and unedited from first prompt to last response, including failed attempts. Export as PDF, Markdown, TXT, or JSON, and include the share link if available. Use screenshots only when the tool cannot export.
- **Artifacts:** what the AI produced before your edits (text, images, wireframes, code) and your final version. For design tools (e.g., Figma AI, v0), include screenshots of each prompt and generated version.
- **Redaction:** only secrets and personal data may be redacted, marked as `[REDACTED]`.
- **Organization:** put files in `conversations/` and `artifacts/` folders, named `[ID]_[Member]_[Tool]_[topic]`. Use IDs `C01, C02, ...` for conversations and `A01, A02, ...` for artifacts, matching the Usage Log in the declaration.

**Code milestones (4–6):** also keep an `AI_USAGE.md` file at the repository root, and append a section each milestone. Do **not** commit conversation logs or the ZIP; evidence goes to Blackboard only.

```markdown
## Phase 4 – Front-End
| ID  | Member | Tool (model)            | Purpose                 | Files affected            |
|-----|--------|-------------------------|-------------------------|---------------------------|
| C01 | Ahmed  | ChatGPT (GPT-x)         | Login form validation   | src/pages/Login.jsx       |
| C02 | Sara   | GitHub Copilot (inline) | Navbar styling          | src/components/Navbar.css |

No AI used: Omar, Fatimah.
```

**Milestone 7:** the final report must include an "AI Usage Statement" summarizing AI use across the whole project. Also declare any AI used for the demo video.

## 5. Exporting Conversations
- Use the tool's **Share** or **Export** option. For example: ChatGPT, Claude, and Gemini provide share links and can be saved as PDF from the browser; VS Code Copilot Chat has **"Chat: Export Chat..."**; Cursor has **Export** in the chat menu.
- If a tool has no export option, copy the full conversation, in order, into a document.
- Log as you go, and do not delete conversations until final grades are released.

## 6. Citing AI in Deliverables
- When you quote or paraphrase AI-generated text, cite it using APA [2] or MLA [3] format.
- Caption AI-generated images, e.g., *"Image generated with [tool]."*
- Credit AI in the commit message of any commit containing AI-assisted code, by adding a last line such as `Assisted-by: ChatGPT (GPT-x)`.

## References
1. Perkins, M., Roe, J., & Furze, L. (2025). *Reimagining the Artificial Intelligence Assessment Scale.* https://doi.org/10.53761/rrm4y757
2. APA Style. *AI references.* https://apastyle.apa.org/style-grammar-guidelines/references/examples/AI-references
3. MLA Style Center. *How do I cite generative AI in MLA style?* https://style.mla.org/citing-generative-ai-updated-revised/
4. KFUPM. *Code of Conduct (IS FAIR) and Key Rules for Students.* https://studentaffairs.kfupm.edu.sa/docs/default-source/default-document-library/is-fair-and-kfupm-key-rules-for-students.pdf
