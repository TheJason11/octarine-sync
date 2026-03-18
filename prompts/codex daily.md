```plaintext
```

```plaintext
```

### import

```plaintext
Run the incremental Capacities import pass on the files currently in 00_Inbox/Import.

Context:
- This is a fresh Capacities export batch
- Some imported notes may already exist in the vault
- Some may be new
- The import subfolders may include:
  - JobNotes
  - Notes
  - Processes
  - Projects
  - ResearchNotes

Routing rules:
- project related notes go to 01_Projects
- research notes go to 07_Research/ResearchNotes
- questions go to 07_Research/Questions if the imported file is clearly a question
- zettels go to 07_Research/Zettels if the imported file is clearly a zettel
- weekly notes go to 06_Journal/Weekly
- weekly summaries and rollups go to 06_Journal/Weekly_Summaries
- job notes go to 02_Areas/JobNotes
- process notes go to 02_Areas/Processes
- everything else goes to the best matching folder under 02_Areas

Rules:
- compare imported files against existing destination notes when a likely match already exists
- if the import contains new or changed information, update the destination note
- if the destination note is already equivalent or stronger, keep the destination note unchanged
- if the note is new, move it to the correct destination
- clean metadata during import when needed
- fix obvious links when needed
- after successful reconciliation, delete the import copy
- remove the Import folder if it is fully drained
- do not touch Personal_Scratchpad
- do not touch .agent
- do not touch .trash
- be aggressive on obvious cases
- stop only for real ambiguity

Workflow:
1. First list the files in 00_Inbox/Import and where each one will go
2. Show which ones are merge targets versus simple moves
3. Then proceed immediately
4. After execution, report exactly what was moved, merged, updated, kept unchanged, and deleted
```

### daily rollup

```plaintext
Act as my Obsidian vault assistant.

Goal
Create today’s Jason Log by searching my Obsidian vault and using only vault note content.

Operating rules
- Use only vault note content.
- Do not run Python.
- Do not execute scripts.
- Do not use web content, memory, or inference beyond what is explicitly supported by today’s notes.
- If something is ambiguous, say so before drafting the log.
- Do not edit any file until I approve the draft in chat.

Primary workflow
1. Search the vault for notes created or modified today.
2. Read only notes that are relevant to today’s work.
3. Draft today’s log in chat first.
4. Before the draft, list:
   - source notes you used
   - exact date range used
   - ambiguous items or excluded notes
5. Wait for my approval.
6. After approval, update today’s daily note by replacing the entire body of the `### Daily Log` section.
7. The replacement boundary is strict:
   - start at the first line after the `### Daily Log` header
   - delete everything from there to the end of the file
   - paste the approved log in its place
8. Do not preserve any old condensed notes, transcript text, raw notes, or other content that appears below `### Daily Log`.
9. Do not change anything above the `### Daily Log` header.
10. After editing, report exactly what changed.

Daily note path
- Today’s daily note path is `06_Journal/Daily/YYYY/MM/YYYY-MM-DD.md`

Missing header rule
- If the `### Daily Log` header is missing, stop and ask me before editing anything.

Search scope
Search the entire vault for notes created or modified today.

Include when relevant
- daily notes
- meeting notes
- job notes
- project notes
- research notes
- experiment notes
- transcripts
- scratch notes created today
- agent session notes only if they contain same day work details or answers I asked for today

Ignore these folders completely
- `Personal_Scratchpad`
- `.agent`
- `.trash`

Evidence rules
- Use only notes created or modified today as primary sources.
- If a note was only modified today but clearly contains older context, include only the parts that directly support work done today.
- Do not invent anything.
- Do not infer unstated actions, decisions, or outcomes.
- Deduplicate overlapping items.
- Preserve original wording whenever possible.
- Fix only obvious spelling mistakes.
- Use plain language.
- No emojis.
- Avoid hyphenated words in sentences.

Units rule
- Always write measurements in empirical units when the notes provide them.
- Prefer inch, foot, feet, pound, lb, °F, fpm, mL, and similar shop units exactly as used in the notes.
- Do not convert values to metric unless the source note itself uses metric.
- If both unit systems appear in the source, lead with the empirical value first.

Voice and naming rules
- Write in first person perspective.
- Do not start every sentence with “I”.
- Do not include the name Jason anywhere in the body of the log.
- Do not mention VP or VP 101.

Common transcript corrections
If these appear in transcripts, correct them.

dealer -> annealer
kneeler -> annealer
veneer -> anneal
large dial -> large payoff
large pail -> large payoff
Keyance -> Keyence
road cutter -> roll cutter
open too -> oven two
Z block -> Zumbach
Zenblock -> Zumbach
Zenblock repairs -> Zumbach
Z box -> Zumbach
Z boxrepairs -> Zumbach
Zin Walker repairs -> Zumbach
Captain Green -> CathX Green
coke ovens -> coat ovens
micro emulsion -> MicroVention
recipe has it set at .057 -> recipe has it set at 0.0573 inch
part is 0.055 -> part is 0.055 inch
GVP -> BBP
VDP -> BBP
BVP -> BBP
suits -> ZEUS
cat colored blades -> cat cutter blades
cut resistance glove -> cut resistant glove
sisters -> scissors
scheduled hearance -> scheduled adherence
make rain -> make rate
active cut he is still above rate -> active cutter is still above rate
meld -> melt
grader -> braider
raider -> braider

Numbers rule
When the notes provide numbers, include the exact values with units.

Include
- ID
- OD
- counts
- temperatures
- speeds
- pass counts
- sample quantities

If shop shorthand appears, write the full value first, then the shorthand in parentheses.

Example
- `0.0277 inch (o 27)`

Systems work rule
Include systems work that directly supports production, quality, training, or reporting.

Examples
- database work
- formulas
- prompts
- templates
- trackers
- document structures

Deliverables rule
- Do not mention any model, AI tool, or chat.
- If an output was created with assistance, log only the deliverable.

Blocker clarity rule
- For each blocker, include the stated cause when it is explicitly in the notes.

Research rule
- Use a dedicated research section when research was done that day.
- Include the note topic and the main finding in plain language.
- Do not include research that was not actually reviewed or used that day.

Idea tracker rule
- Include 2 to 5 bullets only.
- These must be grounded in today’s notes.
- Use this for useful ideas, follow ups, or opportunities that are supported by today’s work but are not already formalized as a project.
- Do not invent anything unsupported.

Output structure
Return the log in this exact structure.

# YYYYMMDD Jason Log

### Fast timeline
Each entry is one line only.
Each entry starts with HH:MM then a single action line.
Add one blank line between each entry.
Do not wrap entries onto multiple lines.

### Completed Today
Each item is one short line only.
Use `- [x]` for each item.
Add one blank line between each item.

### In Progress
Each item is one short line only.
Use `- [ ]` for each item.
Add one blank line between each item.

### Research Done
Use bullets only.
Each bullet is one short line only.
Summarize the research actually done today and the main finding from each note.
Add one blank line between each bullet.

### Decisions Made
Bullets only.
Add one blank line between each bullet.

### Risks and Blockers
Bullets only.
Add one blank line between each bullet.

### Deadlines and Cues
Bullets only.
Add one blank line between each bullet.

### Idea Tracker
Use 2 to 5 bullets only.
Add one blank line between each bullet.

Before writing the draft
1. List the source notes you will use.
2. Confirm the exact date range used.
3. List any ambiguous items or notes that might be excluded.
4. Draft the log in chat.
5. Ask for approval.

After approval
1. Replace the entire body of the `### Daily Log` section in today’s daily note.
2. The `### Daily Log` section owns everything after that header through the end of the file.
3. Delete all old content in that section before pasting the approved log.
4. Preserve everything above the `### Daily Log` header exactly as is.
5. Report exactly what was updated, including the file path and the section boundary used.
6. Verify that the last line of the file is the last line of the approved log.
```