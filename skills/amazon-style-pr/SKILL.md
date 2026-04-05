---
name: amazon-pr
description: "Write Amazon-style Working Backwards press releases as polished Word documents. Use this skill whenever the user wants to write a press release for a new product, feature, or service using Amazon's Working Backwards methodology. Also trigger when the user mentions: 'PR/FAQ', 'working backwards', 'internal press release', 'Amazon-style PR', 'product press release', 'mock press release', 'launch announcement draft', or wants to articulate a product vision before building it. Even if the user just says 'I have a product idea' or 'help me think through this feature', this skill can help them crystallize it into a compelling press release. This skill produces a .docx file."
---

# Amazon-Style Press Release (Working Backwards)

## What This Skill Does

This skill helps users write an Amazon-style internal press release — the kind Amazon product managers write *before* building a product. The output is a professionally formatted Word document (.docx) that follows the proven structure from Amazon's Working Backwards methodology.

The press release isn't marketing copy — it's a thinking tool. It forces clarity on the customer problem, the proposed solution, and why it matters. If the press release isn't compelling, the product probably isn't worth building.

## Workflow

### Step 1: Interview the User

Before writing anything, gather the raw material through a short interview. Ask these questions one or two at a time (not all at once — that's overwhelming). Use the AskUserQuestion tool when available, otherwise ask conversationally.

**Required context (must have before drafting):**

1. **Who is the customer?** Be specific. Not "developers" but "backend engineers at mid-size SaaS companies who manage their own infrastructure." The sharper the customer definition, the better the PR.

2. **What is the problem?** This is the most important question. What pain does the customer experience today? How are they currently solving it (or failing to)? What's frustrating, slow, expensive, or broken? Push for concrete details — anecdotes, numbers, specific scenarios.

3. **What is the product/feature?** What does it do? Give it a working name if one doesn't exist yet.

4. **What is the key benefit?** If you could only tell the customer one thing about this product, what would it be? This becomes the subheading.

5. **What makes this different?** How is this better than existing alternatives? What's the unfair advantage or novel insight?

**Optional but valuable (ask if conversation allows):**

6. **Is there a specific metric or number that captures the improvement?** (e.g., "60 seconds" for Kindle downloads, "$0.15/GB" for S3). Concrete numbers are the difference between a forgettable PR and a memorable one.

7. **Who would the spokesperson be?** (CEO, VP of Product, CTO — needed for the internal quote)

8. **Can you describe a day-in-the-life scenario?** A moment where a customer would use this and feel relieved or delighted. This powers the customer quote.

If the user has already provided rich context in their initial message, skip questions they've already answered. Don't re-ask what you already know.

### Step 2: Write the Press Release

Once you have enough context, write the press release following this exact structure. Every section matters — don't skip any.

#### Structure

**HEADING**
The product name, written so the target customer immediately understands what it is. Not clever, not cute — clear. If a customer reads only this line, they should know what category of product this is.

**SUBHEADING**
One sentence: who the customer is + the single most important benefit. Format: "[City] — [Date] — [Company] today announced [Product], which [does what] for [whom]."

**SUMMARY PARAGRAPH**
2-3 sentences expanding on the subheading. Set the scene: what is the product, who is it for, what does it enable. Write it so someone skimming only this paragraph walks away with the core idea.

**PROBLEM PARAGRAPH**
This is the heart of the press release. Describe the customer's pain vividly and specifically. Use concrete scenarios, not abstractions. The reader should nod along thinking "yes, that's exactly my problem." If you have data (time wasted, money spent, failure rates), include it. The best problem paragraphs make the status quo feel almost absurd.

**SOLUTION PARAGRAPH**
Describe how the product solves the problem. Keep it simple — no architecture diagrams in prose form. Focus on what the customer experiences, not how the technology works under the hood. The solution should feel like the obvious, inevitable answer to the problem you just described.

**SPOKESPERSON QUOTE**
A quote from a company leader (use the spokesperson the user identified, or default to a generic "said [Name], [Title] at [Company]"). This quote should do one of two things: (a) articulate the vision — why this product exists and what future it's building toward, or (b) express the company's commitment to the customer. It should NOT just restate the product description.

Good pattern: "We built [Product] because we believe [big insight about the world]. [Aspirational statement about what this enables]."

**HOW IT WORKS**
Walk the customer through the experience. Use specific, sequential steps: "First, you... Then... Within minutes..." Make the experience feel effortless. If there's a "wow moment" (like Kindle's 60-second download), make sure it lands here.

**CUSTOMER QUOTE**
A hypothetical quote from a satisfied customer. This is NOT generic praise ("I love this product!"). The best customer quotes describe behavior change — what the customer used to do vs. what they do now. They reveal that the product solved a real problem in a way the customer finds almost surprising.

Good pattern: "I used to [painful old way]. Now I [easy new way]. [Specific delightful detail]."

**CALL TO ACTION**
One sentence: where and how the customer gets started. URL, waitlist, availability date — whatever applies.

### Step 3: Generate the .docx

Use the `docx` npm package (install with `npm install docx` if needed) to produce a professionally formatted Word document. Read the docx SKILL.md for syntax reference if needed.

**Formatting guidelines:**

- **Page size**: US Letter (12240 x 15840 DXA), 1-inch margins
- **Font**: Arial throughout
- **Title**: 28pt bold, dark color (#232F3E), centered
- **Subheading**: 13pt, Amazon orange (#FF9900), centered
- **Body text**: 12pt, left-aligned, comfortable line spacing (1.15-1.25)
- **Quotes**: Visually distinct — use a left-border callout style (a table cell with a colored left border and light background fill) or italics with attribution on a new line
- **Section labels** (like "Problem", "Solution"): Don't include them as visible headers. The press release should read as a flowing narrative, not a form. The structure is internal scaffolding — the reader experiences it as a compelling story.
- **Header**: Company name or "INTERNAL — DRAFT" in small gray text
- **Footer**: Page number, centered

The document should look like something you'd actually hand to an executive in a meeting — clean, professional, no visual clutter.

### Step 4: Save and Present

Save the .docx to the workspace folder so the user can access it. Provide a `computer://` link.

After sharing the file, offer to iterate: "Want me to sharpen any section? The problem statement and customer quote are usually worth a second pass."

## Writing Principles

These principles separate a great Amazon PR from a mediocre one. Keep them in mind throughout:

**The problem matters more than the solution.** Spend disproportionate effort on the problem paragraph. If the reader doesn't feel the pain, nothing that follows will land. Amazon PMs routinely rewrite the problem statement 10+ times.

**Replace adjectives with numbers.** "Fast" → "under 60 seconds." "Affordable" → "$9.99." "Reliable" → "99.99% uptime." Every adjective is a missed opportunity to be specific. If a number doesn't exist yet, help the user find one or acknowledge it as a gap.

**Write for a general audience.** No jargon. No acronyms (unless universally known). Jeff Bezos was famous for rejecting PR/FAQs that assumed domain expertise. Test: would a smart person outside the industry understand every sentence?

**The customer quote reveals behavior change.** "I love this product" is worthless. "I used to spend 3 hours every Friday reconciling invoices — now it's automatic" is proof the product works.

**Bold promises create productive tension.** The best PRs promise something the team isn't quite sure they can deliver yet. That's the point — the PR sets the bar, and the team rises to meet it. If the PR feels safe and achievable, the ambition is too low.

**Read it aloud.** If any sentence requires re-reading, it's too complex. Rewrite it. Press releases are meant to be instantly understood.

## Common Pitfalls to Avoid

- **Leading with the technology** instead of the customer problem. Nobody cares that you used machine learning — they care that the task that took 3 hours now takes 3 minutes.
- **Vague problem statements.** "Customers struggle with X" is weak. "A typical marketing manager spends 6 hours per week manually pulling data from 4 different dashboards, copy-pasting into spreadsheets, and reformatting for their Monday standup" is strong.
- **Spokesperson quotes that just restate the product.** The quote is a chance to share vision, not repeat features.
- **Customer quotes that sound like marketing copy.** Real people don't say "This revolutionary platform has transformed my workflow." They say "Honestly, I was skeptical, but last Tuesday it caught an error that would have cost us $40K."
- **Burying the lede.** The most exciting thing about the product should be in the first two paragraphs, not the fifth.
