# Goal
Take as input the language of a congressional bill and output a redlined version of effects on the underlying statutory.

# Why
The format of congressional bills show what changes, but they don't show the changes in context, meaning that they don't provide -- and even actively obfuscate -- the effect of the changes. This problem is well known to lawyers, who insist on "redlines" of edits, which show -- in line and in context -- what changed.

# What and How
- Bills are presented in XML, TXT, PDF, at a URL with a standardized format: E.g. https://www.congress.gov/bill/119th-congress/house-bill/10453/text
- US Code is presented in standardized format, typically HTML: https://uscode.house.gov/browse.html or https://www.govinfo.gov/app/collection/uscode

## Interface
- Minimalist is fine and desired for now. As simple as a terminal command with arguments. Ideally as direct as e.g. % fedline https://www.congress.gov/bill/119th-congress/house-bill/10453/text. Remember this has to work natively on windows/powershell.

## Function
Given a URL for a Bill:
0. Validate that the URL is accessible
1. Step through each section of the bill, finding the full text of the cited statutory section
2. Copy the relevant portion of the statutory text into the deliverable doc, prefaced by the name of the bill and hyperlinked URL of the source
3. Apply the transformations as noted in the bill (this likely requires LLM to parse)
4. For each redline, add a footnote citing to the relevant section number and subsection of the bill (e.g. § 2(a)(1)). When a section results in multiple edits, footnote each instance of the edit separately.
5. Emit the deliverable document into a folder on the local machine.

## Deliverable format:
- Filename reflects the bill number, year, and amendment number. E.g. HR10453_2026 (unclear how amendments are serialized; propose a format).
- Document each affected statutory section as its own set of pages (section break ends page)
- The relevant text of the statutory section is reproduced faithfully and then edited
- Each edit is formatting in accordance with the following redlining format conventions: green for added, red and struckthrough for deleted, purple for moved)
- Undecided on whether the document should be .docx, .html, more than one of these, or something else. Probably a .docx available to start off with.

# Tech Stack
- Must work on Windows or be system agnostic
- Python? (only because I'm most familiar with it and it has lots of libraries)
- LLM for the text evaluation and generation (Probably Claude to start, but bring our own key later)

# Future work
- Mac or multisystem support
- Web or intra-net visible interface for making available to other users. Hosted on GitHub or similar lightweight hosting is fine.
- Automatically start a new folder for each bill, store the deliverable into the correct folder.
- One click re-run when a bill is updated.
- Support for other government entities: States legislatures, Federal agencies (e.g. FCC and support for CFR edits)
