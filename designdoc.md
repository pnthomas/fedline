# Goal
Take as input the language of a congressional bill and output a redlined version of effects on the underlying statutory.

# Why
The format of congressional bills show what changes, but they don't show the changes in context, meaning that they don't provide -- and even actively obfuscate -- the effect of the changes. This problem is well known to lawyers, who insist on "redlines" of edits, which show -- in line and in context -- what changed.

# What and How
- Bills are presented in XML, TXT, PDF, at a URL with a standardized format: E.g. https://www.congress.gov/bill/119th-congress/house-bill/10453/text
- US Code is presented in standardized format, typically HTML: https://uscode.house.gov/browse.html or https://www.govinfo.gov/app/collection/uscode

## Given a URL for a Bill
1. Step through each section of the bill, finding the full text of the cited statutory section
2. Copy the relevant portion of the statutory text into the deliverable doc
3. Apply the transformations as noted in the bill
4. For each redline, add a footnote citing to the relevant section number and subsection of the bill (e.g. § 2(a)(1)). When a section results in multiple edits, footnote each instance of the edit separately.

## Deliverables format:
- Document each affected statutory section as its own set of pages (section break ends page)
- The relevant text of the statutory section is reproduced faithfully and then edited
- Each edit is formatting in accordance with the following redlining format conventions: green for added, red and struckthrough for deleted, purple for moved)
- Undecided on whether the document should be .docx, .html, .md or something else. Probabloy .docx to start off with.

# Future work
- One click re-run when a bill is updated.
- Support for other government entities: States legislatures, Federal agencies
