---
name: knowledge-management
description: Manages a local knowledge base for storing, retrieving, updating, and organizing structured knowledge entries about methodologies, client systems, tools, and other topics with zero hallucinations
allowed-tools: [Read, Write, Edit, Glob, Grep]
---

# Knowledge Management Skill

You are assisting with knowledge management operations. This skill provides methods to manage a local knowledge base stored as markdown files, ensuring accurate, well-organized information is accessible without relying on online searches or risking hallucinations.

## Core Principle

**ZERO HALLUCINATIONS**: Only use information present in the local knowledge base. Never make up information, never search online, never infer beyond what is explicitly documented.

## Directory Structure

Knowledge-related files are organized as follows:
- `.claude/knowledge/` - Knowledge entry files (markdown)
- `.claude/skills/knowledge-management/templates/` - Template for knowledge entries
- `.claude/epics/` - Epic files (future) referenced in knowledge entries

## File Naming Conventions

- **Knowledge entries**: Title with dashes instead of spaces (e.g., `SOSTAC-Framework.md`, `Tesa-Client-System.md`)
- **Use descriptive, clear titles**: Make it easy to find entries by filename
- **Lowercase recommended**: For consistency (e.g., `sostac-framework.md`)

## Knowledge Entry Structure

All knowledge entries follow a standardized template with these sections:

### YAML Frontmatter
- **Title**: Clear, descriptive title of the knowledge entry
- **Epic**: Epic(s) this knowledge relates to (can be a list)
- **Date Added**: When the entry was created (YYYY-MM-DD)
- **Date Updated**: When the entry was last updated (YYYY-MM-DD)

### Content Sections
- **Quick Summary**: Brief 1-2 sentence overview
- **Source(s)**: Links to source materials (meeting transcripts, external docs, URLs)
- **Details**: Comprehensive information about the topic

## Available Methods

---

### 1. Add New Knowledge Entry

Create a new knowledge entry in the knowledge base.

**Purpose**: Document new information about methodologies, client systems, tools, processes, or decisions for future reference.

**When to use**:
- After learning important information from meetings, documents, or discussions
- When documenting a decision or process
- When creating reference material for methodologies or tools
- When triggered by other agents (e.g., Meeting Assistant after transcript extraction)

**Steps**:

1. **Gather information**
   - Understand the topic to be documented
   - Collect all source materials (meeting transcripts, docs, URLs)
   - Identify relevant epic(s) if applicable

2. **Determine entry title**
   - Create clear, descriptive title
   - Convert to filename format: lowercase with dashes (e.g., `sostac-framework.md`)
   - Check if entry already exists using Glob

3. **Load the template**
   - Read template from `.claude/skills/knowledge-management/templates/knowledge-entry-template.md`

4. **Populate the template**
   - **Title**: Clear, descriptive title
   - **Epic**: List relevant epic(s) or "General" if none
   - **Date Added**: Current date (YYYY-MM-DD)
   - **Date Updated**: Same as Date Added for new entries
   - **Quick Summary**: Synthesize 1-2 sentence overview
   - **Source(s)**: List all sources with proper links
     - Meeting transcripts: `[Meeting Name](.claude/meetings/transcripts/YYYYMMDD-HHMMSS MeetingName-transcript.md)`
     - External docs: `[Doc Title](URL or path)`
     - URLs: `[Description](URL)`
   - **Details**: Comprehensive, synthetic information
     - Be precise and concise
     - Organize with headers/lists as needed
     - Only include factual information from sources
     - NO HALLUCINATIONS

5. **Create the knowledge entry**
   - Save to `.claude/knowledge/{title-with-dashes}.md`
   - Use Write tool to create file
   - Verify file created successfully

6. **Confirm completion**
   - Report entry location to user/agent
   - Provide link to entry
   - Suggest related entries if applicable

**Inputs**:
- Topic title
- Source materials (transcripts, docs, URLs)
- Epic assignment (optional)
- Content/information to document

**Outputs**:
- New knowledge entry file in `.claude/knowledge/`
- Confirmation of creation
- Link to created entry

**Example**:
```markdown
Agent trigger: "Document SOSTAC framework from training meeting"
Steps:
1. Gather info from meeting transcript
2. Title: "SOSTAC Framework" → filename: `sostac-framework.md`
3. Check if .claude/knowledge/sostac-framework.md exists (use Glob)
4. Load template from .claude/skills/knowledge-management/templates/knowledge-entry-template.md
5. Populate:
   - Title: SOSTAC Framework
   - Epic: Marketing Strategy
   - Date Added: 2025-11-21
   - Date Updated: 2025-11-21
   - Quick Summary: "Strategic planning framework covering Situation, Objectives, Strategy, Tactics, Actions, and Control phases"
   - Source: [Training Meeting](.claude/meetings/transcripts/20251121-100000 Training-transcript.md)
   - Details: [Detailed breakdown of each phase...]
6. Save to .claude/knowledge/sostac-framework.md
7. Confirm: "Knowledge entry created: .claude/knowledge/sostac-framework.md"
```

---

### 2. Search Knowledge Base

Search for information in the knowledge base based on queries.

**Purpose**: Find relevant knowledge entries to answer questions or provide context.

**When to use**:
- When user asks a question that might be in knowledge base
- When other agents need information from knowledge base
- Before creating new entry to check for duplicates
- When looking for related knowledge entries

**Steps**:

1. **Parse search query**
   - Understand what information is being requested
   - Identify key terms and concepts
   - Determine search strategy (filename vs. content)

2. **Search by filename first**
   - Use Glob to find entries matching title patterns
   - Pattern: `*.claude/knowledge/*{keyword}*.md`
   - Quick way to find entries with known titles

3. **Search by content if needed**
   - Use Grep to search within knowledge entry content
   - Search in Quick Summary section first (faster)
   - Search in Details section for comprehensive results
   - Pattern: keyword or phrase to find

4. **Read matching entries**
   - Read files that match search criteria
   - Extract relevant information
   - Note source references from entries

5. **Return results**
   - Provide information from matching entries
   - Include entry titles and links
   - Cite sources from within entries
   - If no matches: clearly state "No knowledge entries found for [query]"

6. **NO HALLUCINATIONS**
   - Only return information that exists in knowledge entries
   - If information is not found, say so explicitly
   - Never infer or make up information

**Inputs**:
- Search query or keywords
- Optional: Epic filter
- Optional: Date range filter

**Outputs**:
- Matching knowledge entries with relevant excerpts
- Links to full entries
- Source citations from entries
- Clear "not found" message if no matches

**Example**:
```markdown
User: "What is the SOSTAC framework?"
Steps:
1. Parse query: Looking for "SOSTAC framework"
2. Search filenames: Glob for *.claude/knowledge/*sostac*.md
3. Found: .claude/knowledge/sostac-framework.md
4. Read entry
5. Return: "SOSTAC Framework: Strategic planning framework covering Situation, Objectives, Strategy, Tactics, Actions, and Control phases. [Full entry](.claude/knowledge/sostac-framework.md). Source: Training Meeting transcript."

User: "Tell me about API authentication"
Steps:
1. Parse query: "API authentication"
2. Search filenames: No match
3. Search content: Grep for "API authentication" in .claude/knowledge/
4. No matches found
5. Return: "No knowledge entries found for 'API authentication'. Consider searching online with the online-search skill or documenting this as a new knowledge entry."
```

---

### 3. Update Existing Knowledge Entry

Update an existing knowledge entry with new information.

**Purpose**: Keep knowledge entries current by adding new information, correcting errors, or expanding details.

**When to use**:
- When new information becomes available about an existing topic
- When correcting or clarifying existing entries
- When adding additional sources to an entry
- When triggered by other agents with updates

**Steps**:

1. **Locate the entry**
   - Search for entry using Glob or Grep
   - Confirm correct entry found
   - Read current entry content

2. **Identify what to update**
   - Determine which sections need changes:
     - Quick Summary (if overview changes)
     - Sources (if adding new sources)
     - Details (if adding/modifying information)
   - Note what information is being added/changed

3. **Update Date Updated field**
   - Change Date Updated to current date (YYYY-MM-DD)
   - Keep Date Added unchanged

4. **Apply updates using Edit tool**
   - Update Quick Summary if needed
   - Add new sources to Source(s) section
   - Add/modify Details section
   - Preserve existing information unless replacing
   - Maintain structure and formatting

5. **Verify update**
   - Read updated entry to confirm changes
   - Ensure no information was lost
   - Check formatting is correct

6. **Confirm completion**
   - Report what was updated
   - Provide link to updated entry
   - Note new sources if added

**Inputs**:
- Entry title or filename
- New information to add
- New sources (if applicable)
- Sections to update

**Outputs**:
- Updated knowledge entry
- Confirmation of updates
- Summary of changes made

**Example**:
```markdown
Agent trigger: "Add new source to SOSTAC framework entry from today's strategy meeting"
Steps:
1. Locate: .claude/knowledge/sostac-framework.md
2. Read current entry
3. Identify updates:
   - Add new source: Strategy meeting transcript
   - Update Details with new insights from meeting
   - Update Date Updated to 2025-11-21
4. Use Edit tool:
   - Update Date Updated field
   - Add new source link
   - Add new details from meeting
5. Verify changes by reading entry
6. Confirm: "Updated .claude/knowledge/sostac-framework.md with information from Strategy meeting. Added new source and expanded Details section."
```

---

### 4. Delete Outdated Knowledge Entry

Remove knowledge entries that are no longer relevant or accurate.

**Purpose**: Maintain knowledge base quality by removing obsolete or incorrect information.

**When to use**:
- When information is confirmed to be outdated
- When entry is superseded by a newer, better entry
- When information is discovered to be incorrect
- When consolidating duplicate entries

**Steps**:

1. **Locate the entry**
   - Search for entry using Glob
   - Confirm correct entry found
   - Read entry to verify it should be deleted

2. **Verify deletion is appropriate**
   - Confirm information is outdated/incorrect
   - Check if information should be moved to another entry instead
   - Ensure no other entries depend on this one

3. **Check for references**
   - Search for links to this entry in other knowledge entries
   - Search for references in meeting summaries or other docs
   - Note any references that need updating

4. **Delete the entry**
   - Use Bash tool: `rm .claude/knowledge/{filename}.md`
   - Confirm deletion successful

5. **Update references (if applicable)**
   - Update other entries that referenced deleted entry
   - Add notes about why entry was removed if needed

6. **Confirm deletion**
   - Report entry deleted
   - Note any references updated
   - Suggest replacement entry if applicable

**Inputs**:
- Entry title or filename to delete
- Reason for deletion (optional)
- Replacement entry (optional)

**Outputs**:
- Confirmation of deletion
- List of updated references (if any)
- Link to replacement entry (if applicable)

**Example**:
```markdown
User: "Delete the outdated API v1 documentation entry"
Steps:
1. Locate: .claude/knowledge/api-v1-documentation.md
2. Read entry to verify
3. Verify: Confirmed outdated, replaced by api-v2-documentation.md
4. Check references: Grep for "api-v1-documentation" in .claude/knowledge/
5. Delete: rm .claude/knowledge/api-v1-documentation.md
6. Update references: No references found
7. Confirm: "Deleted .claude/knowledge/api-v1-documentation.md (outdated). Replaced by .claude/knowledge/api-v2-documentation.md"
```

---

## Integration with Other Agents

### Meeting Assistant Integration
Meeting Assistant may trigger knowledge-management skill to:
- Document decisions from meetings
- Create knowledge entries from extracted information
- Provide transcript links as sources

**Example trigger**:
```markdown
From Meeting Assistant:
"Document SOSTAC framework decision from strategy meeting"
Context:
- Decision: Adopt SOSTAC for all marketing planning
- Rationale: Structured approach, proven methodology
- Source: [Strategy Meeting](.claude/meetings/transcripts/20251121-140000 Strategy-transcript.md)
```

### Stakeholder Manager Agent Integration
Stakeholder Manager Agent may trigger knowledge-management skill to:
- Document client-specific processes
- Create entries about organizational structures
- Store important procedural information

### Other Agents
Any agent can:
- **Search** knowledge base for information
- **Request** new entries be created
- **Provide** updates to existing entries
- **Reference** knowledge entries in their work

## Important Notes

### Zero Hallucinations Policy
- **NEVER** make up information
- **NEVER** infer beyond what is documented
- **NEVER** search online (use online-search skill instead)
- **ONLY** use information from local knowledge entries
- If information doesn't exist, say so clearly

### Knowledge Entry Quality
- **Be concise**: Capture essence, not everything
- **Be precise**: Accurate and factual only
- **Be synthetic**: Summarize, don't transcribe
- **Be structured**: Use headers, lists, clear organization
- **Cite sources**: Always link back to source materials

### File Management
- Use consistent naming: lowercase with dashes
- Keep entries focused: One topic per entry
- Link related entries: Reference other relevant entries
- Maintain templates: Follow structure consistently

### Search Strategy
- **Filename search first**: Faster for known titles
- **Content search second**: When keyword searching needed
- **Be specific**: Use precise search terms
- **Return links**: Always provide links to full entries

### Maintenance
- Update Date Updated field when modifying entries
- Keep Date Added unchanged
- Remove outdated information promptly
- Consolidate duplicates when found

## Template Location

Knowledge entry template: `.claude/skills/knowledge-management/templates/knowledge-entry-template.md`

## References

- Knowledge Manager Agent: `.claude/agents/knowledge-manager.md` (future)
- Meeting Management Skill: `.claude/skills/meeting-management/skill.md`
- Stakeholder Manager Agent: `.claude/agents/hr.md`
