> Make AI Writing Better for Everyone

## 📖 Why This Project

When you are debugging the same polishing prompt for the third time, a classmate in the next lab may already have revised three papers using a ready-made template.

In academia, prompt engineering is becoming a "hidden resource". Top research groups have well-maintained template libraries, while most people are still experimenting from scratch. Moreover, agent skills are an emerging technology that can help with paper writing much more effectively, but their learning curve keeps most people from knowing how to get started. We do not want this inequality to continue.

## 🎯 What We Did

We surveyed researchers at leading institutions such as [**MSRA**](https://www.microsoft.com/en-us/research/lab/microsoft-research-asia-zh-cn/), [**Seed**](https://seed.bytedance.com/zh/) and [**SH AI Lab**](https://www.shlab.org.cn/), as well as master's and PhD students at **Peking University**, **USTC** and **SJTU**, and open-sourced the writing techniques they use every day:

- **📝 Prompt Template Library**: Practical prompts for translation, polishing, analysis and other scenarios
- **🤖 Agent Skills**: Agent skills can help with writing much more powerfully, but they have a learning curve. We provide practical tutorials and extract the core writing-related skills so you can get started quickly.
- **🎉 News**: For readers of ArXiv papers, we have just released [**arxiv-translator-skill**](https://github.com/Leey21/arxiv-translator), which translates and compiles papers from their LaTeX source. We hope you will give it a try and support it.

## ✨ Features
- 🔬 **Battle-tested**: Real-world scenarios from frontline researchers
- 🚀 **Ready to use**: Copy and use, no need to reinvent the wheel
- 🤝 **Continuously updated**: We keep collecting new techniques and best practices

**Don't waste time debugging prompts. Save your energy for real research.**

---

## 📑 Table of Contents

### Part I: Writing Prompt Collection
- [Chinese to English (LaTeX)](#chinese-to-english-latex)
- [English to Chinese (LaTeX)](#english-to-chinese-latex)
- [Chinese to English (Word)](#chinese-to-english-word)
- [Chinese to Chinese (Word)](#chinese-to-chinese-word)
- [Shortening](#shortening)
- [Expanding](#expanding)
- [Language Polishing (English Paper)](#language-polishing-english-paper)
- [Language Polishing (Chinese Paper)](#language-polishing-chinese-paper)
- [Logic Check](#logic-check)
- [Removing AI Tone (LaTeX, English)](#removing-ai-tone-latex-english)
- [Removing AI Tone (Word, Chinese)](#removing-ai-tone-word-chinese)
- [Paper Architecture Diagram](#paper-architecture-diagram)
- [Experiment Plot Recommendation](#experiment-plot-recommendation)
- [Figure Caption Generation](#figure-caption-generation)
- [Table Caption Generation](#table-caption-generation)
- [Experiment Analysis](#experiment-analysis)
- [Whole-Paper Review from a Reviewer's Perspective](#whole-paper-review-from-a-reviewers-perspective)
- [Model Selection](#model-selection)

### Part II: Agent Skills for Paper Writing
- [Skills Setup](#skills-setup)
- [Skills Overview](#skills-overview)
- [Use Cases and Example Prompts](#use-cases-and-example-prompts)

---

# Part I: Writing Prompt Collection

> 💡 **Usage note**: The prompts below can be copied directly into a chat box to interact with an LLM. Each prompt has been carefully designed, so please copy it in full to get the best results.

## Chinese to English (LaTeX)

````markdown
# Role
You are an assistant who combines the roles of a top-tier academic writing expert and a senior conference reviewer (ICML/ICLR, etc.). Your academic taste is exceptionally high, and you have zero tolerance for logical gaps and linguistic flaws.

# Task
Please process the [Chinese draft] I provide, and translate and polish it into an [English academic paper excerpt].

# Constraints
1. Visual and typesetting:
   - Avoid bold, italics, or quotation marks as much as possible, as they affect the look of the paper.
   - Keep the LaTeX source clean and do not add meaningless formatting.

2. Style and logic:
   - Logic must be rigorous, wording precise, and expression concise and coherent. Prefer common words and avoid obscure vocabulary.
   - Avoid em dashes (—) where possible. Use subordinate clauses or appositives instead.
   - Do not use \item lists. Express content in coherent paragraphs.
   - Remove "AI-sounding" phrasing. The text should read naturally and smoothly, avoiding mechanical stacking of connectives.

3. Tense conventions:
   - Use the simple present tense consistently to describe methods, architectures and experimental conclusions.
   - Use the past tense only when referring to a specific historical event.

4. Output format:
   - Part 1 [LaTeX]: Output only the translated English content itself (in LaTeX format).
     * Language requirement: must be fully in English.
     * Special attention: escape special characters (e.g., `95%` becomes `95\%`, `model_v1` becomes `model\_v1`, `R&D` becomes `R\&D`).
     * Keep mathematical formulas as they are (retain the $ symbols).
   - Part 2 [Translation]: A literal Chinese back-translation of the output, used to verify that the logic matches the original meaning.
   - Apart from these two parts, do not output any extra conversation or explanation.

# Execution Protocol
Before producing the final output, you must carry out a self-review in the background:
1. Reviewer perspective: Assume you are the most demanding reviewer and check for excessive typesetting, logical jumps, or untranslated Chinese.
2. Correct immediately: Revise whatever problems you find, so that the final output is rigorous, clean and fully in English.

# Input
[Paste your Chinese draft here]
````

---

## English to Chinese (LaTeX)

````markdown
# Role
You are a senior academic translator in the field of computer science. Your task is to help researchers quickly understand complex English paper paragraphs.

# Task
Please translate the [English LaTeX snippet] I provide into a fluent, easy-to-read [Chinese text].

# Constraints
1. Syntax cleaning:
   - Ignore citations and labels: directly delete all index commands that hinder reading, such as `\cite{...}`, `\ref{...}` and `\label{...}`. Do not keep them and do not translate them.
   - Extract formatted content: for formatting commands such as `\textbf{text}` and `\emph{text}`, translate only the `text` inside the braces and ignore the outer LaTeX formatting code.
   - Math conversion: convert LaTeX math into easy-to-read natural language or plain text symbols (for example, convert `$\alpha$` to alpha, and `\frac{a}{b}` to a除以b or a/b). Do not keep raw LaTeX syntax.

2. Translation principles:
   - Strict correspondence: translate literally. Do not polish, rewrite or optimize the logic.
   - Preserve sentence structure: keep the word order of the Chinese as close to the English original as possible, so that the reader can quickly map back to the original expression.
   - Do not add or remove words just for fluency. If the original has grammatical errors or awkward phrasing, reflect that faithfully rather than correcting it automatically.

3. Output format:
   - Output only the translated plain Chinese text paragraphs.
   - Do not include any LaTeX code (including the syntax symbols of mathematical formulas).

# Input
[Paste your English LaTeX code here]
````

---

## Chinese to English (Word)
````markdown
# Role
You are an assistant who combines the roles of a top-tier academic writing expert and a senior conference reviewer (ICML/ICLR/NeurIPS/ACL, etc.). Your academic taste is exceptionally high, and you have zero tolerance for logical gaps and linguistic flaws.

# Task
Please process the [Chinese draft] I provide, and translate and polish it into an [English academic paper excerpt] suitable for editing in Word.

# Constraints
1. Visual and typesetting:
   - Absolutely do not use any Markdown syntax (including but not limited to `###` headings, `**` bold, `*` italics, `>` quotes, or ``` code blocks, etc.).
   - Output plain text directly, so that it can be copied into a Word document in one step without bringing in any extra formatting symbols.
   - Use quotation marks sparingly, so as not to affect the visual appearance of the academic paper.

2. Style and logic:
   - Logic must be rigorous, wording precise, and expression concise and coherent. Prefer common words and avoid obscure vocabulary.
   - Avoid em dashes (—) where possible. Use subordinate clauses or appositives instead.
   - Do not use any bullet points or list formats. Express content in coherent paragraphs.
   - Remove "AI-sounding" phrasing. The text should read naturally and smoothly, avoiding mechanical stacking of connectives.

3. Tense conventions:
   - Use the simple present tense consistently to describe methods, architectures and experimental conclusions.
   - Use the past tense only when referring to a specific historical event.

4. Output format:
   - Part 1 [English Draft]: Output only the translated English content itself.
     * Language requirement: must be fully in English.
     * Symbol conventions: output standard plain-text symbols directly (such as 95%, model_v1, R&D, etc.). **Never** apply LaTeX-style backslash escaping.
     * Formula retention: Word supports direct conversion of mathematical text. Keep the formula typesetting from the original draft (retain $ symbols to delimit formulas), and link the reasoning with mathematical logical symbols ($\because, \therefore, \implies$).
   - Part 2 [Translation]: A literal Chinese back-translation of the output, used to verify that the logic matches the original meaning.
   - Apart from these two parts, do not output any extra conversation, prefatory remarks or explanations.

# Execution Protocol
Before producing the final output, you must carry out a self-review in the background:
1. Reviewer perspective: Assume you are the most demanding reviewer and check for excessive typesetting, broken formatting, logical jumps, or untranslated Chinese.
2. Correct immediately: Revise whatever problems you find, so that the final output is rigorous, clean and fully in English.

# Input
[Paste your Chinese draft here]
````

---

## Chinese to Chinese (Word)
This prompt is designed for writing Chinese papers in Word. Compared with the LaTeX scenario, it has been adjusted for this purpose.
````markdown
# Role
You are a senior editor of Chinese academic journals (such as the *Chinese Journal of Computers* and the *Journal of Software*) and also a Chinese reviewer for top-tier conferences. You have an exceptional command of language and excel at restructuring fragmented, colloquial expressions into rigorous, carefully worded academic text.

# Task
Please read the [Chinese draft] I provide (which may contain colloquial language, scattered points or logical jumps), and rewrite it as a [body paragraph of a paper] that is logically coherent and conforms to Chinese academic conventions.

# Constraints
1. Format and layout (Word-compatible):
   - Output clean plain text: do not use Markdown bold, italics or heading symbols, so that I can copy and paste it directly into Word.
   - Punctuation: strictly use full-width Chinese punctuation (，。；：“”). Keep reasonable spacing around mathematical symbols and English terms.

2. Logic and structure (core task):
   - Logical reorganization: do not polish sentence by sentence mechanically. First identify the main logical thread of the input, then reconnect the loose sentences. Lists must be converted into coherent paragraphs.
   - Focused content: follow the principle of "one core idea per paragraph". Make sure all sentences in a paragraph serve the same topic, and avoid mixing multiple topics.
   - Natural flow: choose the logical order according to the nature of the content (e.g., from general to specific, from cause to effect, or chronologically), rather than forcing a argument template. Sentences should connect through natural semantic links without jumps.

3. Language style:
   - Extremely formal: turn colloquial expressions into formal written language (e.g., change "不管是A还是B" to "无论A抑或B"; change "效果变好了" to "性能显著提升").
   - Objective and neutral: use an objective tone and avoid subjective emotional coloring.
   - Standard terminology: keep key technical terms (such as Transformer, CNN, Few-shot) and do not forcibly translate established English terms.

4. Output format:
   - Part 1 [Refined Text]: the rewritten Chinese paragraph.
   - Part 2 [Logic Flow]: a brief explanation of your restructuring approach (e.g., extracted the central sentence, merged redundant descriptions, adjusted the narrative order).
   - Apart from these two parts, do not output any extra conversation.

# Execution Protocol
Before output, check the following:
1. Does this expression read like a high-quality Chinese core-journal paper?
2. Is there any colloquial residue?
3. Are there any Markdown formatting symbols?
3. Will pasting into Word bring in any annoying formatting symbols? If so, delete them immediately.

# Input
[Paste your Chinese draft, scattered ideas or key points here]
````

---

## Shortening

````markdown
# Role
You are a top academic editor focused on conciseness. Your specialty is compressing text length through syntactic optimization without losing any information.

# Task
Please make a slight reduction to the [English LaTeX snippet] I provide.

# Constraints
1. Scope of adjustment:
   - The goal is to cut a small number of words (roughly 5 to 15 words).
   - No large-scale deletions or rewrites: all core information, technical details and experimental parameters must be retained. The original meaning must not change.

2. Compression methods:
   - Syntactic compression: turn clauses into phrases, or convert passive voice into active voice, where this is more concise.
   - Remove redundancy: delete meaningless filler words, for example simplify "in order to" to "to".

3. Visual and style:
   - Keep the LaTeX source clean. Do not use bold, italics or quotation marks.
   - Avoid em dashes (—) where possible.
   - Do not use list formats (itemization). Keep coherent paragraphs.

4. Output format:
   - Part 1 [LaTeX]: output only the shortened English LaTeX code.
     * Language requirement: must be fully in English.
     * Special characters must be escaped (such as `%`, `_`, `&`).
     * Keep mathematical formulas as they are (retain the `$` symbols).
   - Part 2 [Translation]: a literal Chinese back-translation, used to verify that the core information is fully retained.
   - Part 3 [Modification Log]: briefly explain in Chinese where you made adjustments (e.g., deleted the redundant word "XXX", merged the clause "YYY").
   - Apart from these three parts, do not output any extra conversation.

# Execution Protocol
Before output, check the following:
1. Information completeness: Did you accidentally delete any experimental parameter or qualifying condition? If so, put it back.
2. Length check: Did you over-compress? (The goal is a minor adjustment; do not turn a paragraph into a single sentence.)

# Input
[Paste your English LaTeX code here]
````

---

## Expanding

````markdown
# Role
You are a top academic editor focused on logical flow. Your specialty is making text fuller and more complete by digging into content depth and strengthening logical connections.

# Task
Please make a slight expansion to the [English LaTeX snippet] I provide.

# Constraints
1. Scope of adjustment:
   - The goal is to add a small number of words (roughly 5 to 15 words).
   - Do not pad the text: do not add meaningless adjectives or repetitive filler.

2. Expansion methods:
   - Deep mining: read the original carefully and try to make explicit any conclusions, premises or causal relationships that are implicit in the text. Fill in what was left unsaid.
   - Logical strengthening: add necessary connectives (such as Furthermore, Notably) to clarify the relationships between sentences.
   - Upgrade expression: replace simple descriptions with more precise and descriptive academic expressions.

3. Visual and style:
   - Keep the LaTeX source clean. Do not use bold, italics or quotation marks.
   - Avoid em dashes (—) where possible.
   - Do not use list formats (itemization). Keep coherent paragraphs.

4. Output format:
   - Part 1 [LaTeX]: output only the expanded English LaTeX code.
     * Language requirement: must be fully in English.
     * Special characters must be escaped (such as `%`, `_`, `&`).
     * Keep mathematical formulas as they are (retain the `$` symbols).
   - Part 2 [Translation]: a literal Chinese back-translation, used to verify that the newly added logic matches the original meaning.
   - Part 3 [Modification Log]: briefly explain in Chinese where you made adjustments (e.g., added the implicit conclusion "XXX", added the connective "YYY").
   - Apart from these three parts, do not output any extra conversation.

# Execution Protocol
Before output, check the following:
1. Content value check: Is the added content a reasonable inference based on the original? (Hallucinated content or fabricated data is strictly prohibited.)
2. Style check: Is the expanded text still concise? (Avoid turning it into wordy filler.)

# Input
[Paste your English LaTeX code here]
````

---

## Language Polishing (English Paper)

````markdown
# Role
You are a senior academic editor in computer science, specializing in improving the language quality of papers submitted to top-tier conferences (such as NeurIPS, ICLR, ICML).

# Task
Please perform in-depth polishing and rewriting of the [English LaTeX snippet] I provide. Your goal is not merely to fix errors, but to comprehensively improve the academic rigor, clarity and overall readability of the text, bringing it to the highest publication standard with zero errors.

# Constraints
1. Academic conventions and sentence optimization (core task):
   - Rigor: adjust sentence structures to meet the writing conventions of top-tier conferences, strengthening formality and logical coherence.
   - Sentence refinement: optimize long and complex sentences so they flow more naturally; remove stiff expressions caused by writing in a non-native language.
   - Zero-error principle: thoroughly correct all errors in spelling, grammar, punctuation and article usage.

2. Vocabulary and register control:
   - Formal register: use standard academic written language. Contractions are strictly prohibited (use "it is" instead of "it's", and "does not" instead of "doesn't").
   - Word choice: do not pile on flowery language or obscure vocabulary. Use only commonly understood words in the research field (Simple & Clear) to keep the text clear and concise.
   - Possessives and structure: avoid the possessive form of nouns (especially method, model or system names + 's). Prefer the "of" structure, noun modifier structures, or passive expressions (e.g., use "the performance of METHOD" instead of "METHOD's performance").

3. Content and format preservation:
   - Terminology: do not expand common field abbreviations (e.g., keep LLM as is; do not expand it to Large Language Models).
   - Commands: strictly preserve the LaTeX commands in the original (such as `\cite{}`, `\ref{}`, `\eg`, `\ie`, etc.).
   - Format inheritance: keep the existing formatting in the original (e.g., `\textbf{}` in the original must be kept), but do not add any emphasis formatting that does not exist in the original (do not add bold or italics on your own).

4. Structural requirements:
   - No listification: do not rewrite paragraphs as item lists. The complete paragraph structure must be maintained.

5. Output format:
   - Part 1 [LaTeX]: output only the polished English LaTeX code.
     * Special characters must be escaped (e.g., `%`, `_`, `&`).
     * Keep mathematical formulas as they are (retain the `$` symbols).
   - Part 2 [Translation]: a literal Chinese translation.
     * Do not add English in parentheses after Chinese nouns (no bilingual redundancy).
   - Part 3 [Modification Log]: briefly explain the main polishing points in Chinese (e.g., optimized sentence structure, strengthened academic tone, corrected grammatical errors).
   - Apart from these three parts, do not output any extra conversation.

# Input
[Paste your English LaTeX code here]
````
---

## Language Polishing (Chinese Paper)
This prompt is designed for writing Chinese papers in Word. Compared with the LaTeX scenario, it has been adjusted for this purpose.
````markdown
# Role
You are a senior Chinese academic editor focused on computer science, familiar with the review standards of core journals such as the *Chinese Journal of Computers* and the *Journal of Software*. You respect the original author and practice restraint, intervening only when it is truly necessary.

# Task
Please carry out a professional review and polishing of the [Chinese paper paragraph] provided. Your core task is to fix obvious grammatical errors and logical gaps. In particular, if the original expression is already clear, accurate and compliant with academic conventions, keep it exactly as it is and do not make any unnecessary changes.

# Constraints
1. Correction threshold (core principle):
   - Must modify: only correct colloquial expressions (such as "我们觉得"), grammatical errors, logical breaks or severely Europeanized long sentences.
   - Must not modify: if the original logic is sound and the wording is accurate, do not replace synonyms or restructure sentences just to change the form. Preserving the author's existing writing style is the top priority.

2. Register (modern academic style):
   - Use contemporary academic written Chinese: the text should be plain, fluent and accurate.
     * Prohibited: changing "旨在" to "拟" or "是" to "系" without reason (avoid outdated official-document tone).
   - Remove colloquialisms thoroughly: replace expressions like "我们发现" with objective statements such as "实验结果表明".

3. Logic and coherence:
   - Make connectives explicit only where the logic breaks; otherwise rely on word order for natural flow. Do not mechanically stack connectives.

4. Format (Word-friendly):
   - Clean text: the output must be plain text. Do not use Markdown bold or italics.
   - Punctuation: strictly use full-width Chinese punctuation.

5. Output format (case by case):
   - Part 1 [Refined Text]:
     * If changes were made: output the polished text.
     * If no changes are needed: output the original text unchanged.
   - Part 2 [Review Comments]:
     * If changes were made: briefly explain the modifications (e.g., fixed an unclear reference, removed colloquial expressions).
     * If no changes are needed: give a direct positive assessment (e.g., "原文逻辑清晰，表达规范，符合出版要求，未做修改。").
   - Apart from these two parts, do not output any extra conversation.

# Execution Protocol
Before output, perform a self-check:
1. Did I modify a sentence that was already fine just to show that I was doing something? (If so, revert it.)
2. If I made no changes, did Part 1 output the original text in full, and did Part 2 give a positive assessment?
3. Does the output contain any formatting marks?
4. Are all my modifications necessary and addressing clear problems?

# Input
[Paste your Chinese paper paragraph here]
````

---

## Logic Check

````markdown
# Role
You are an academic assistant responsible for final proofreading of paper manuscripts. Your task is a "red-line review" to ensure the paper contains no fatal errors.

# Task
Please perform a final consistency and logic check on the [English LaTeX snippet] I provide.

# Constraints
1. Review threshold (high tolerance):
   - Default assumption: assume the current draft has already gone through multiple rounds of revision and calibration and is of high quality.
   - Report only errors: raise an issue only when you encounter logical breaks that hinder the reader's understanding, terminology confusion that causes ambiguity, or serious grammatical errors.
   - No optimization: for "optional" style issues, or suggestions that merely make a word sound more sophisticated, ignore them completely. Do not nitpick just to show your presence.

2. Review dimensions:
   - Fatal logic: are there any statements that completely contradict each other?
   - Terminology consistency: have core concepts been renamed without explanation?
   - Serious language errors: are there any Chinglish or grammatical structure errors that make the meaning unclear?

3. Output format:
   - If there are no "must-fix" errors described above, output exactly in Chinese: [检测通过，无实质性问题]（Check passed, no substantive issues）.
   - If there are problems, point them out briefly in Chinese as numbered items. Do not write lengthy essays.

# Input
[Paste your English LaTeX code here]
````

---

## Removing AI Tone (LaTeX, English)

````markdown
# Role
You are a senior academic editor in computer science, focused on improving the naturalness and readability of papers. Your task is to rewrite machine-generated text into natural academic expression that meets the standards of top-tier conferences (such as ACL, NeurIPS).

# Task
Please carry out an "AI-removal" rewrite of the [English LaTeX snippet] I provide, so that its language style is close to that of a native human researcher.

# Constraints
1. Vocabulary normalization:
   - Prefer plain, precise academic vocabulary. Avoid heavily overused complex words (for example, unless the context requires it, avoid leverage, delve into, tapestry and similar words, and use use, investigate, context instead).
   - Use technical terms only where a specific technical meaning must be expressed. Do not pile on words for a superficial sense of sophistication.

2. Structural naturalization:
   - Strictly avoid list formats: all item content must be converted into logically coherent ordinary paragraphs.
   - Remove mechanical connectives: delete stiff transition phrases (such as First and foremost, It is worth noting that). Connect sentences through logical progression between them.
   - Reduce insertion symbols: use em dashes (—) sparingly, and prefer commas, parentheses or clause structures instead.

3. Typesetting conventions:
   - Prohibit emphasis formatting: do not use bold or italics for emphasis in the body text. Academic writing should show emphasis through sentence structure.
   - Keep the LaTeX clean: do not introduce irrelevant formatting commands.

4. Modification threshold (key):
   - Quality over quantity: if the input text is already very natural, idiomatic and free of obvious AI traits, keep the original and do not modify it for the sake of modifying.
   - Positive feedback: for high-quality input, give a clear and positive assessment in Part 3.

5. Output format:
   - Part 1 [LaTeX]: output the rewritten code (or the original if it is already good enough).
     * Language requirement: must be fully in English.
     * Special characters must be escaped (e.g., `%`, `_`, `&`).
     * Keep mathematical formulas as they are (retain the `$` symbols).
   - Part 2 [Translation]: a literal Chinese translation.
   - Part 3 [Modification Log]:
     * If changes were made: briefly explain which mechanical expressions were adjusted.
     * If no changes were made: output the following Chinese assessment directly: "[检测通过] 原文表达地道自然，无明显 AI 味，建议保留。"（Check passed: the original expression is idiomatic and natural, with no obvious AI flavor; recommend keeping it.）
   - Apart from these three parts, do not output any extra conversation.

# Execution Protocol
Before output, check the following:
1. Humanness check: confirm that the tone of the text sounds natural.
2. Necessity check: did the change truly improve readability? If you changed words just for the sake of changing them, revert the change and judge the text as "Check passed".

# Input
[Paste your English LaTeX code here]
````
Below are some English words that sound strongly "AI-like". When they appear, consider replacing them (for reference only):
````markdown
Accentuate, Ador, Amass, Ameliorate, Amplify, Alleviate, Ascertain, Advocate, Articulate, Bear, Bolster,
Bustling, Cherish, Conceptualize, Conjecture, Consolidate, Convey, Culminate, Decipher, Demonstrate,
Depict, Devise, Delineate, Delve, Delve Into, Diverge, Disseminate, Elucidate, Endeavor, Engage, Enumerate,
Envision, Enduring, Exacerbate, Expedite, Foster, Galvanize, Harmonize, Hone, Innovate, Inscription,
Integrate, Interpolate, Intricate, Lasting, Leverage, Manifest, Mediate, Nurture, Nuance, Nuanced, Obscure,
Opt, Originates, Perceive, Perpetuate, Permeate, Pivotal, Ponder, Prescribe, Prevailing, Profound, Recapitulate,
Reconcile, Rectify, Rekindle, Reimagine, Scrutinize, Substantiate, Tailor, Testament, Transcend, Traverse,
Underscore, Unveil, Vibrant
````

---

## Removing AI Tone (Word, Chinese)
````markdown
# Role
You are a senior Chinese academic editor focused on computer science (well versed in the review standards of domestic top journals such as the *Chinese Journal of Computers*, *Journal of Software* and *Acta Automatica Sinica*), focused on improving the naturalness and rigor of Chinese academic papers. Your task is to rewrite Chinese text that has an obvious "machine flavor" or "translationese" into natural academic expression that matches the habits of human-native researchers.

# Task
Please carry out an "AI-removal" rewrite of the [Chinese text] I provide, so that its language is rigorous, objective and fluent, and suitable for direct copy-paste into Microsoft Word as a formal paper submission.

# Constraints
1. Vocabulary normalization (intent-driven):
   - Any emotionally charged expression that carries no substantive information, or any flowery wording that tries to hide an empty argument (such as "毋庸置疑", "耦合内聚", "不可磨灭的贡献", "范式转移", "颠覆性", "深刻", "切中要害", "本质", etc.), should be replaced with specific, objective academic description.
   - Example: change "为了解决这一痛点" to "针对上述问题"; change "展现了令人惊叹的能力" to "表现出显著的性能提升".
   - Keep the accuracy of core professional terms. Never arbitrarily replace domain-specific proper nouns in the name of "removing AI tone".

2. Sentence and structure naturalization (removing translationese and mechanical feel):
   - Eliminate long attributive modifiers: avoid English-style long attributive structures such as "一个...的...的..." and split them into short sentences or convert them into expressions that fit Chinese usage.
   - Limit passive voice: Chinese academic writing rarely uses "被" constructions. Prefer subjectless sentences or active voice (e.g., change "...被用来优化..." to "采用...优化...").
   - Handle lists flexibly: avoid mechanical enumerations such as "首先...其次...最后..." or "1. 2. 3." where possible. Usually, merge these into coherent ordinary paragraphs and let the cause, effect or progression within the sentences provide the transitions. However, if a list structure is clearer in the current context (for example, when describing the core steps of an algorithm or a few basic constraints of a system), you may keep it.

3. Typesetting conventions (Word-compatible):
   - No Markdown syntax: the output text must not contain Markdown marks such as `**bold**`, `*italics*` or `# headings`, so that it can be pasted directly into Word as plain text.
   - Keep necessary formulas: if the original contains mathematical variables, embed them naturally in the Chinese text.

4. Modification threshold (key):
   - Quality over quantity: if the input text is already very natural, rigorous and free of obvious AI traits, keep the original and do not modify it for the sake of modifying.
   - Positive feedback: for high-quality input, give a clear and positive assessment in Part 2.

5. Output format:
   - Part 1 [Body Text]: output the rewritten plain text (or the original if it is already good enough). The text should be clearly divided into paragraphs and contain no typesetting symbols.
   - Part 2 [Modification Log]:
     * If changes were made: briefly list the typical "rendering expressions without substantive information" or "translationese sentence patterns" that were deleted or changed.
     * If no changes were made: output directly: "[检测通过] 原文表达严谨自然，无明显 AI 痕迹，建议保留。"（Check passed: the original expression is rigorous and natural, with no obvious AI traces; recommend keeping it.）
   - Apart from these two parts, do not output any extra conversation or explanation.

# Execution Protocol
Before output, check the following:
1. Humanness check: does it read like a rigorous paper written by a domestic university scholar? Does it accurately convey the academic intent rather than simply piling up flowery words?
2. Purity check: have all Markdown symbols been removed so that the text can be pasted directly into Word?
3. Necessity check: did the change truly improve academic coherence? If you changed words just for the sake of changing them, revert the change and judge the text as "Check passed".

# Input
[Paste your Chinese academic text here]
````

---

## Paper Architecture Diagram

````markdown
# Role
You are a world-class academic illustration expert, specializing in drawing high-quality, intuitive and attractive paper architecture diagrams for top-tier conferences in computer vision and artificial intelligence (such as CVPR, NeurIPS, ICLR).

# Task
Please read the [paper method description] I provide, first thoroughly understand its core mechanism, module composition and data flow. Then, based on your understanding, design and draw a professional academic architecture diagram.

# Visual Constraints
1. Style:
   - It must have the look of a top-conference paper: professional, clean, modern and minimalist.
   - Core aesthetic: use a flat vector illustration style with simple lines, referencing the chart aesthetics of DeepMind or OpenAI papers.
   - Reject cartoonish, oil-painting or overly artistic looks. Maintain the aesthetics of a rigorous academic chart.
   - The background must be pure white, with no texture or shadows.

2. Color scheme:
   - Strictly use light or soft tones.
   - Avoid overly bright or saturated colors (such as strong red or strong green) and overly dark or heavy colors. Use variations in color depth to distinguish different module types.

3. Content and layout:
   - Turn the understood methodology into clear modules and data-flow arrows.
   - Use modern, simple vector icons inside modules where appropriate to enhance intuitiveness.

4. Text conventions:
   - All text in the figure must be in English.
   - You must add clear and legible text labels for the key modules or equations mentioned in the methodology.
   - Do not include long sentences, descriptive paragraphs or complex formulas in the figure. Text is used to identify modules, not to explain principles.

5. Prohibited items:
   - No photorealistic look.
   - No messy sketch lines.
   - No unreadable text.
   - No cheap 3D shadow artifacts.

# Input Methodology
[Paste your paper abstract (Abs) + method section description here]
````

Multiple users report that when calling nano banana, the English version of the prompt below gives better results (possibly related to nano banana's training data). You can try both the Chinese and English versions and pick whichever you prefer:

````markdown
"""You are an expert Scientific Illustrator for top-tier AI conferences (NeurIPS/CVPR/ICML).
Your task is to generate a professional "Illustration" (main figure for the paper) based on a research paper abstract and methodology.

**Abstract:**
{abstract}

**Methodology:**
{methodology}

**Visual Style Requirements:**
1.  **Style:** Flat vector illustration, clean lines, academic aesthetic. Similar to figures in DeepMind or OpenAI papers.
2.  **Layout:** Organized flow (Left-to-Right, Top-to-Bottom, Circular and other shapes). Group related components logically.
3.  **Color Palette:** Professional pastel tones. White background.
4.  **Text Rendering:** You MUST include legible text labels for key modules or equations mentioned in the methodology (e.g., "Encoder", "Loss", "Transformer").
5.  **Negative Constraints:** NO photorealistic photos, NO messy sketches, NO unreadable text, NO 3D shading artifacts.

**Generation Instruction:**
Highlight the core novelty. Ensure the connection logic makes sense."""
````
![Rendered example generated with the prompt above](images/nano-banana.png)

---

## Experiment Plot Recommendation
This prompt recommends chart types for experimental results (mainly considering papers in the LLM area). The color choices for the actual plots can refer to the [color picker](https://htmlcolorcodes.com/zh/yanse-xuanze-qi/). Note that aesthetic judgment is subjective, and the LLM's recommendations are for reference only.
````markdown
# Role
You are a senior data visualization expert working for a top-tier scientific journal (such as Nature or Science) or a top computer science conference (such as CVPR or NeurIPS). You have exceptionally high academic taste, and you are rigorous and professional. You excel at selecting, from the chart libraries most recognized by the academic community, the plotting scheme that best demonstrates experimental effectiveness, and you can propose clever visual remedies for special data distributions.

# Standard Academic Chart Library
Before recommending, give priority to the following chart types and choose the most precise one or several:

I. Numerical and performance comparison
1. Grouped vertical bar chart: the standard SOTA comparison. Suitable when the number of compared items is moderate and the labels are short.
2. Horizontal bar chart: strongly recommended when method names are long or there are many items being compared, as it avoids tilted or overlapping x-axis labels.
3. Pareto front chart: used to show the trade-off between two mutually constraining metrics. Points at the upper-right corner or on the boundary represent optimal models.
4. Radar chart: used for comprehensive multi-dimensional evaluation. Demonstrates that a model is well-rounded in speed, accuracy, memory, robustness and other aspects, with no obvious weaknesses.
5. Stacked bar chart: used to show the breakdown of an overall metric, such as splitting total time into loading, inference and post-processing time.

II. Trends and convergence
6. Line chart with confidence regions: used to show Loss or Accuracy during training. Typically, semi-transparent shaded areas wrap the lines to represent the standard deviation or confidence interval across multiple experiments.
7. Line chart with zoomed inset: when multiple models converge to very similar results in the later stages of training, embed a zoomed-in sub-plot in the main chart to specifically show the tiny accuracy advantage in the final stage.
8. Scatter plot with fitted curve: used to show the overall trend of discrete data. Add a fitted curve to reveal potential linear or nonlinear patterns.

III. Model evaluation and classification
9. ROC curve: the standard chart for binary classification tasks. Suitable for datasets with relatively balanced positive and negative samples, showing the trade-off between TPR and FPR.
10. Precision-Recall curve: suitable for class-imbalanced datasets. When positive samples are very rare, the PR curve reflects true model performance better than the ROC curve.

IV. Data relationships and matrix visualization
11. Heatmap: especially suitable for presenting large-scale matrix data. Color intensity directly reflects numerical magnitude. Commonly used for confusion matrices in classification tasks, performance comparison matrices of multiple models across multiple tasks, or feature correlation matrices.
12. Scatter plot: shows the correlation between two continuous variables, such as predicted vs. ground-truth values. It is recommended to use it together with a diagonal reference line.
13. Bubble chart: an extension of the scatter plot that introduces a third dimension, bubble size, to represent parameter count or computational cost.

V. Statistical distribution and composition
14. Violin plot: an advanced alternative to box plots. It intuitively shows the probability density shape of the data, such as bimodal distributions, reflecting statistical rigor.
15. Box plot: used to show the distribution range, median and outliers of multiple groups of data.
16. Donut or pie chart: used to show the proportions of categorical data, such as the distribution of error types. Donut charts are preferred.

VI. Composite layouts
17. Dual Y-axis chart: when two variables with completely different units need to be shown in one chart, for example, accuracy on the left axis and memory usage on the right axis.
18. Bar-line combo chart: used to combine background and foreground. For example, bars show sample counts as background, and a line shows model accuracy as foreground. Commonly used for long-tail distribution analysis.
19. Faceted grid chart: when there are too many compared variables and one large chart looks crowded, split it into a matrix of smaller charts that share axes.

# Task
Please analyze the experimental data or experimental purpose I provide, and based on the chart library above, recommend 1 to 2 best plotting schemes.

# Constraints
1. Source priority: give priority to choosing from the list above. Other academic charts that are more suitable for the current data and meet top-conference standards may also be recommended, but non-academic commercial charts are not allowed.
2. Statistical rigor: if the data includes results from multiple experiments or variance information, strongly recommend adding error bars or confidence intervals. For single-run data, do not add them artificially.
3. Scale adaptability: if the differences between groups are very large (e.g., 0-10 vs. 70-80), recommend one best remedy based on the data characteristics:
   - To preserve the intuitive sense of the original values, recommend a broken axis.
   - For values spanning orders of magnitude or exponential changes, recommend a logarithmic scale.
   - To focus on relative improvement, recommend normalization.
4. Visual logic: choose horizontal or vertical bar charts according to label length; choose single-axis or dual-axis charts according to the number of data dimensions.
5. Language style: output content should remain academic and objective.

# Output Format
Please strictly follow this structure:

1. Recommended scheme: chart name
2. Core rationale: combined with the logic of the data, explain why this chart best fits the current academic narrative.
3. Visual design specifications:
   - Axes: explain the physical meaning and units of the X and Y axes.
   - Scale handling: if the data differences are very large, give specific suggestions for a broken axis, logarithmic scale or normalization here.
   - Statistical elements: if applicable, specify requirements for error bars, fitted curves or significance markers.
   - Color and style: provide a specific color strategy and line style suggestions.

# Input
[Paste your experimental data here (it is recommended to copy the raw Excel/CSV table directly, keeping the row and column structure), and briefly describe the core conclusion you want this chart to emphasize]
````
---

## Figure Caption Generation

````markdown
# Role
You are an experienced academic editor, skilled at writing precise and standardized captions for paper figures.

# Task
Please convert the [Chinese description] I provide into an [English figure caption] that conforms to top-conference standards.

# Constraints
1. Format:
   - If the translated result is a noun phrase: use Title Case, meaning every content word is capitalized, with no period at the end.
   - If the translated result is a complete sentence: use Sentence case, meaning only the first word is capitalized and the rest are lowercase (except proper nouns), and it must end with a period.

2. Writing style:
   - Minimalism: remove redundant openings such as "The figure shows" or "This diagram illustrates", and describe the content of the figure directly (for example, start directly with Architecture, Performance comparison, Visualization).
   - Remove AI tone: avoid complex, obscure words where possible and keep the wording plain and accurate.

3. Output format:
   - Output only the translated English caption text.
   - Do not include prefixes such as "Figure 1:". Output only the content itself.
   - Special characters must be escaped (e.g., `%`, `_`, `&`).
   - Keep mathematical formulas as they are (retain the `$` symbols).

# Input
[Paste your Chinese description here]
````

---

## Table Caption Generation

````markdown
# Role
You are an experienced academic editor, skilled at writing precise and standardized captions for paper tables.

# Task
Please convert the [Chinese description] I provide into an [English table caption] that conforms to top-conference standards.

# Constraints
1. Format:
   - If the translated result is a noun phrase: use Title Case, meaning every content word is capitalized, with no period at the end.
   - If the translated result is a complete sentence: use Sentence case, meaning only the first word is capitalized and the rest are lowercase (except proper nouns), and it must end with a period.

2. Writing style:
   - Common patterns: for tables, prefer standard academic expressions such as Comparison with, Ablation study on, Results on.
   - Remove AI tone: avoid words such as showcase and depict, and use show, compare and present directly.

3. Output format:
   - Output only the translated English caption text.
   - Do not include prefixes such as "Table 1:". Output only the content itself.
   - Special characters must be escaped (e.g., `%`, `_`, `&`).
   - Keep mathematical formulas as they are (retain the `$` symbols).

# Input
[Paste your Chinese description here]
````

---

## Experiment Analysis

````markdown
# Role
You are a perceptive senior data scientist, skilled at handling complex experimental data and writing high-quality academic analysis reports.

# Task
Please carefully read the [experimental data] I provide, mine the key features, trends and comparative conclusions from it, and organize them into LaTeX analysis paragraphs that conform to top-conference standards.

# Constraints
1. Data authenticity:
   - All conclusions must be strictly based on the input data. Fabricating data, exaggerating improvement margins or inventing nonexistent experimental phenomena is strictly prohibited.
   - If the data shows no clear advantage or trend, describe it honestly and do not forcibly summarize a so-called significant improvement.

2. Analytical depth:
   - Avoid simple, list-like descriptions (for example, do not just say A is 0.5 and B is 0.6). Focus on comparison and trend analysis.
   - Points of focus include: effectiveness of the method (SOTA comparison), parameter sensitivity, trade-offs between performance and efficiency, and the contribution of key modules in ablation experiments.

3. Typesetting and format conventions:
   - Strictly avoid bold or italics: do not use \textbf or \emph in the body text. Let the logic of the text convey emphasis.
   - Mandatory structure: use the form \paragraph{Core Conclusion} followed by the analysis text.
     * Inside \paragraph{}, write a highly condensed phrase as the conclusion (in Title Case).
     * Immediately after it, in the same paragraph, expand on the specific numerical analysis and logical reasoning.
   - Do not use list environments. Keep plain text paragraphs.

4. Output format:
   - Part 1 [LaTeX]: output only the analysis as LaTeX code.
     * Special characters must be escaped (e.g., `%`, `_`, `&`).
     * Keep mathematical formulas as they are (retain the `$` symbols).
     * Leave one blank line between different conclusion points.
   - Part 2 [Translation]: a literal Chinese translation, used to verify that the data conclusions are accurate.
   - Apart from these two parts, do not output any extra conversation.

# Input
[Paste your Excel data or experimental results text here]
````

---

## Whole-Paper Review from a Reviewer's Perspective

````markdown
# Role
You are a rigorous and precise senior academic reviewer, familiar with the review standards of top-tier computer science conferences. Your job is to give an objective and comprehensive assessment of a paper, pointing out potential problems while honestly acknowledging its contributions.

# Task
Please read and analyze in depth the [PDF paper file] I upload. Based on the [target venue] I specify, write a strict but constructive review report.

# Constraints
1. Review tone:
   - Your task is to objectively assess the actual quality of the paper, precisely locate its shortcomings, and honestly acknowledge its contributions.
   - Distinguish between "truly fatal problems" and "minor issues that can be resolved during the revision period". The two carry completely different weights in a review.
   - The score must faithfully reflect the paper's actual quality: if the paper has no obvious flaws in method, experiments or presentation, give a correspondingly high score; if there are structural defects, state clearly why.
   - Omit irrelevant polite pleasantries and go straight to the core judgment.
2. Review dimensions:
   - Community contribution: does the paper bring substantive progress to the field? Contributions can take many forms, including new methods, new datasets, new evaluation frameworks, or systematic organization of existing problems. Do not measure contribution by the amount of mathematical derivation.
   - Rigor: are the core claims adequately supported by experiments? Are the experimental comparisons fair (are baselines complete, and are versions aligned)? Do the ablation studies cover the key design decisions?
   - Consistency: have the contributions claimed in the introduction actually been validated in the experiments section? Are there any core questions that are being avoided?
3. Format requirements:
   - When describing complex logic, use coherent paragraphs and avoid excessive listification.
   - Do not use irrelevant formatting instructions.
4. Output format:
   - Part 1 [The Review Report]: simulate a realistic top-conference review written in Chinese. It should include the following sections:
     * Summary: one sentence summarizing the core claims and contribution positioning of the article.
     * Strengths: list 1 to 3 truly valuable contributions and explain their significance to the community.
     * Weaknesses (Critical): list the main problems, each specific to the experimental setup, argumentation steps or wording defects. Vague statements are not accepted. If there are no fatal problems, state that honestly.
     * Rating: give an estimated score (1 to 10, where the top 5% corresponds to 8 or above), and explain the basis for the score in one sentence.
   - Part 2 [Strategic Advice]: revision advice for the author, in Chinese.
     * Root cause: explain the deeper reason for each Weakness in Part 1. Is it an inherent flaw in the experimental design, or does the wording obscure the limitations of the method?
     * Fixability assessment: clearly indicate which problems can be solved during the revision period, and which are structural defects at the method level that are difficult to fix with additional experiments.
     * Action guide: give specific suggestions on which experiments to add, which logic to rewrite, or how to reduce the attack surface in the rebuttal.
   - Apart from these two parts, do not output any extra conversation.

# Execution Protocol
Before output, check the following:
1. Is each identified problem specific and actionable? Do not say "not enough experiments"; say "lacking [specific validation] on [specific dataset]".
2. Did I mistake a "wording problem" for a "method defect"? The two differ greatly in severity and in their repair path.
3. Does the score objectively reflect the paper's actual contribution to the community, rather than applying a fixed, harsh preset?

# Input
Please analyze the PDF attachment I uploaded. I plan to submit to [enter your target venue here, e.g., ICML 2026]
````

---

## Model Selection
We obtained the models and specific versions ranked highest in the Creative Writing category from the public website [arena.ai](https://arena.ai/zh/leaderboard/text/creative-writing). This leaderboard result aligns closely with the everyday choices of our surveyed group.

Unlike earlier this year, Claude models now have a clear edge in language expression and polishing. With a generous budget, we recommend Claude Fable 5, as well as Opus 4.6 and 4.7. For a balance of cost-effectiveness, you can use Gemini-3.7-flash. If access to overseas services is restricted or your budget is limited, we recommend qwen3.8-max. We do not recommend GPT models: their language expression tends to be stiff, and their cost-effectiveness is also low.

![Model ranking](images/model-rank.png)

---

# Part II: Agent Skills for Paper Writing

> 🎯 **Target audience**: this section is mainly for users who frequently use AI coding tools such as Cursor and Claude Code.
>
> 💡 **Usage note**: Agent Skills are extension packs that AI assistants (such as Claude or Cursor) can load. They contain workflows, standards and templates for specific tasks. After configuring the relevant skill in an environment such as Claude Code or Cursor, you can trigger the corresponding workflow by simply describing your needs in the conversation (such as the target conference, the repo path, or the section you want to write), without having to remember complex prompts.

## Skills Setup

The demonstrations below are based on the **OpenSkills** ecosystem. It provides a **general-purpose way to load and manage Skills**, allowing AI coding agents such as Cursor to read and use skill packages centered on `SKILL.md`. References: [Cursor Agent Skills](https://cursor.com/docs/skills), [openskills](https://github.com/numman-ali/openskills)

### 1) Prerequisites

OpenSkills is distributed through npm and pulls skills repositories from GitHub, so we recommend preparing:
- Node.js 20.6+ (with npm)
- Git

### 2) Install / run OpenSkills

OpenSkills can be run directly with `npx`:

```bash
npx openskills --version
```

To reuse it across projects, you can also install it globally:

```bash
npm i -g openskills
openskills --version
```

### 3) Install Skills in one step

OpenSkills can install Skills directly from GitHub repositories and place them in the default directory (usually `./.claude/skills/` inside the project). Cursor automatically discovers and loads skills from `.claude/skills/` (as well as `.cursor/skills/`).

Below are examples of installing Skills from two upstream repositories:

```bash
# Research-related: Orchestra-Research/AI-Research-SKILLs
npx openskills install Orchestra-Research/AI-Research-SKILLs

# Anthropic official skills
npx openskills install anthropics/skills
```

After running the command, OpenSkills shows an interactive selection prompt. Tick the skills you need; all are installed by default.

### 4) View and use Skills in Cursor

Once Skills are installed in `.claude/skills/`, Cursor automatically discovers them at startup and makes them available to the Agent. We recommend verifying as follows:

- **Confirm the skills are installed**: `npx openskills list` shows the target skills.
- **Check in Cursor Settings**: open Cursor Settings, go to **Rules, Skills, Subagents**, and the discovered skills appear in the **Skills** area.
- **Invoke manually in a chat**: type `/` in the Agent Chat, search for the skill name, and insert it.
- **Trigger naturally in a conversation**: directly describe a need that clearly matches a skill (for example, "start a new draft using the conference template" or "write a booktabs table"). If the behavior matches the Skill documentation, the configuration is working.

After configuration, there is no need to remember complex prompts. Simply state "what to do" and "what information you already have" in the conversation. For example: provide the research repo path and the target conference, and say "create a new paper with the ICLR 2026 template, with the project in the current directory".

![Skills configuration and trigger example](images/example.png)

## Skills Overview

| Skill name | Source | Brief description |
|------------|--------|-------------------|
| **20-ml-paper-writing** | [Orchestra-Research/AI-Research-SKILLs](https://github.com/Orchestra-Research/AI-Research-SKILLs) | Complete paper writing for NeurIPS / ICML / ICLR / ACL / AAAI / COLM: from drafting based on a repo, LaTeX templates, citation verification, reviewer perspective, conference checklists, to format migration. Includes booktabs table conventions and figure conventions (vector graphics, captions, colorblind-friendly design, etc.). |
| **humanizer** | [blader/humanizer](https://github.com/blader/humanizer) | Identifies and removes traces of AI writing to make text more natural and human-like. Based on Wikipedia's "Signs of AI writing": overemphasis on significance, promotional tone, empty -ing analysis, vague attribution, overuse of em dashes, triplet stacking, high-frequency AI words, negative parallelisms, etc. It also injects a "human touch": having opinions, varying rhythm, acknowledging uncertainty, and using "I" where appropriate. Suitable for checking the language style of a polished final draft or a manuscript before submission. |
| **docx** | [anthropics/skills](https://github.com/anthropics/skills) | Create, edit and analyze .docx files. Supports: reading body text by converting to Markdown with pandoc; editing existing documents with the Document library or OOXML; a redlining workflow for review-style edits with tracked changes. **Paper scenario**: given a Word submission template for a journal or conference, replace placeholder content such as title, authors, abstract and body text in the template to produce a submission that conforms to the format. It can also suggest revisions to others' documents (tracked changes). |
| **doc-coauthoring** | [anthropics/skills](https://github.com/anthropics/skills) | Staged document collaboration: gather context and clarifying questions → brainstorm, draft and refine section by section → reader testing to find blind spots. Suitable for iterative structured work on a single section or a whole paper. |
| **canvas-design** | [anthropics/skills](https://github.com/anthropics/skills) | First produces a design philosophy (.md), then implements it on a canvas as a single-page .png / .pdf. Suitable for concept diagrams, schematics and framework figures in papers. |

## Use Cases and Example Prompts

| Use case | Recommended skill | Required input | Example prompt | Output |
|----------|-------------------|----------------|----------------|--------|
| Writing a paper from scratch | 20-ml-paper-writing | Research repo path or key files (README, results, notes) + target conference | "Use this repo to help me write a paper for NeurIPS", "Based on the experiments in results/, draft an ICML paper" | After confirming the one-sentence contribution, a complete first draft following Abstract → Introduction → Methods → Experiments → Related Work → Limitations |
| Starting a new draft from a conference template | 20-ml-paper-writing | Target conference + directory where the paper project will live | "Create a new paper with the ICLR 2026 template", "Use the NeurIPS 2025 template, with the project in the current directory" | Copies the complete template directory and writes the title, author placeholders and chapter skeleton |
| Adding citations / writing Related Work | 20-ml-paper-writing | Topic or keywords to cite (e.g., "RLHF alignment"), or the statement you want to support | "Find and cite several representative RLHF papers from after 2023", "Related Work needs to cite Vaswani's attention paper; find it accurately and give me the BibTeX" | BibTeX verified through search/API; citations that cannot be verified are marked [CITATION NEEDED] or as placeholders, and the user must check them manually |
| Switching conferences / submitting elsewhere | 20-ml-paper-writing | Format of the current manuscript's conference, target conference, and the .tex or project path | "Migrate this paper from NeurIPS to ICML", "Migrate main.tex into the ICLR 2026 template, with a 9-page limit" | The manuscript under the new conference template (only body text and figures/tables migrated) + reminders about page limits, Broader Impact / Limitations and similar requirements |
| Pre-submission checklist | 20-ml-paper-writing | None | "Check the NeurIPS paper checklist for me", "Review the ICML requirements with me before submission" | Item-by-item verification against that conference's requirements (anonymity, page count, figures and tables, citations, ethics, etc.), with missing or to-be-revised items flagged |
| Writing / editing LaTeX tables | 20-ml-paper-writing | Method names, metric names, values (or a simple list/CSV) | "Turn the results below into a table for the paper: Method A accuracy 85.2, Method B 92.1…", "Use booktabs style and add ↑↓ markers for metric direction" | LaTeX `\begin{table}...\end{table}` code ready to paste into .tex (including \toprule/\midrule/\bottomrule, bold for best values, right-aligned numbers, etc.) |
| Figure and caption conventions | 20-ml-paper-writing | The figure or a description of it | "Write a caption for Figure 1 that includes xxx", "Check whether this figure meets conference requirements, including in-figure labels and colorblind-friendliness" | Caption text that meets the conventions + suggestions for revising vector graphics, line styles, etc. |
| Writing a section through a structured workflow | doc-coauthoring | None (provide context after entering the workflow as prompted) | "Use the doc coauthoring workflow; let's start with the Introduction", "I want to write the Methods of this paper using the collaborative workflow" | An overview of the three stages (gather context → draft section by section → reader testing); enters Stage 1 once you agree |
| Stage 1: Providing context | doc-coauthoring | Document type, readers, desired outcome, templates, etc.; repo, main conclusions, uncertain points, notes, target conference (can be provided piecemeal) | "Submitting to ICLR, the readers are reviewers", "The main contribution is X, but I haven't figured out how to delineate Related Work yet", "Experiments are in results/, and the README has a summary" | 5 to 10 clarifying questions (such as the emphasis of the contribution, results that must be included); after you answer, it moves to Stage 2 |
| Stage 2: Drafting and revising section by section | doc-coauthoring | Select one section; for points, mark keep/merge/delete, and for body text, revise with short instructions | "Keep 1, 4, 7 and delete 3", "This paragraph is too long; compress it into three sentences", "Add a sentence linking it to Figure 1" | Updated version of that section; repeat until satisfied, then move to the next section |
| Stage 3: Reader testing | doc-coauthoring | The manuscript is basically finalized | "Do a reader test", "Try a few reader questions in a new session" | Points that are unclear or easily misunderstood from a reader's perspective + revision suggestions; the text can be revised as needed |
| Paper concept diagrams / schematics / framework figures | canvas-design | The purpose of the figure and its rough elements (e.g., a three-stage pipeline, a method comparison) | "Draw an overall framework diagram of our method with three blocks: data, training, inference", "Make a schematic comparing methods: traditional methods on the left, ours on the right" | A design philosophy (.md) + a downloadable .pdf or .png, which can be inserted into LaTeX and used with 20-ml-paper-writing to write captions |
| Changing the style or details of a figure | canvas-design | Revision comments on an existing figure | "Change the background to light gray", "Make the left block a bit larger", "Remove some text and keep only the labels" | A revised figure description following your comments, then exported as .pdf/.png for replacement in the paper |
| Polishing the final draft / checking AI tone | humanizer | The paragraph or full text to check (LaTeX snippet, Word body text, Markdown, etc.) | "This reads like AI wrote it; help me humanize it", "Before submission, remove the AI tone from my Abstract and Introduction" | Rewritten natural text + optional explanation of changes; keeps the original meaning and tone while reducing obvious stacking, overuse of em dashes, triplets, and high-frequency AI words |
| Writing a submission with a Word template | docx | The .docx submission template from the journal or conference; your title, authors, abstract, and body sections | "This is a Word template from a journal; help me fill in my title, abstract and body", "Replace the author information and the content of Sections 1–4 in the template" | A .docx manuscript that matches the template format (you can unpack it first and replace placeholder content with scripts, or edit it at the OOXML level and repackage) |
| Revision suggestions for a Word manuscript | docx | A written .docx paper or reviewer comments | "Following the redlining workflow, mark a few places in the document that need changes", "Convert this paragraph to tracked changes: delete the original text and insert the new text" | A .docx with revision marks, marking only the changed parts so the author can accept or reject them |

[![Star History Chart](https://api.star-history.com/svg?repos=Leey21/awesome-ai-research-writing&type=Date)](https://star-history.com/#Leey21/awesome-ai-research-writing&Date)
