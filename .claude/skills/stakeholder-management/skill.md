# Stakeholder Management Skill

You are assisting with stakeholder management operations. This skill provides workflows for managing stakeholder information and interaction logs through structured markdown files.

## Directory Structure

Stakeholder files are stored in:
```
.claude/stakeholders/
```

Each stakeholder has a dedicated file named: `familyname_firstname.md` (lowercase with underscores)

Template available at: `.claude/skills/stakeholder-management/templates/stakeholder-template.md`

---

## Available Workflows

### 1. Create Stakeholder

Add a new stakeholder to the system.

**Steps:**
1. Gather required information from user:
   - Family Name (required)
   - First Name (required)
   - Company (required)
   - Role (required)
   - Email (optional)
   - Phone (optional)
   - LinkedIn (optional)
   - Location (optional)
2. Validate that required fields are provided
3. Generate filename: `[familyname]_[firstname].md` (lowercase)
4. Check if stakeholder file already exists
5. Load template from `.claude/skills/stakeholder-management/templates/stakeholder-template.md`
6. Replace placeholders with actual information
7. Create new file in `.claude/stakeholders/`
8. Confirm creation with user

**Example:**
```
User: Add a new stakeholder: John Doe, ABC Corp, CEO
HR Agent: Creates doe_john.md with the provided information
```

---

### 2. Update Stakeholder Information

Modify contact information for an existing stakeholder.

**Steps:**
1. Identify stakeholder by name
2. Locate stakeholder file in `.claude/stakeholders/`
3. Read current file contents
4. Update specified fields while preserving all other data
5. Maintain interaction log integrity (no changes to log entries)
6. Save updated file
7. Confirm update with user

**Example:**
```
User: Update John Doe's email to john.doe@newcompany.com
HR Agent: Updates the email field in doe_john.md
```

---

### 3. Log Interaction

Record a new interaction with a stakeholder.

**Steps:**
1. Identify stakeholder by name
2. Locate stakeholder file
3. Read current file contents
4. Check if today's date (YYYY-MM-DD) already exists as a heading
5. If date exists, append to that section
6. If date doesn't exist, create new H3 heading with date at the top of the Interaction Log
7. Add interaction notes below the date heading
8. Save updated file
9. Confirm log entry with user

**Example:**
```
User: Log interaction with John Doe: Discussed Q4 strategy and budget allocation
HR Agent: Adds entry under today's date in doe_john.md
```

---

### 4. List Stakeholders

Display all stakeholders in the system.

**Steps:**
1. Scan `.claude/stakeholders/` directory
2. Read all `.md` files (excluding README.md)
3. Extract key information from each file:
   - Name (from H1 heading or filename)
   - Company
   - Role
4. Format as a table or list
5. Display to user

**Output Format:**
```
Stakeholders:
1. Doe, John - CEO at ABC Corp
2. Smith, Jane - CTO at XYZ Inc
3. [...]
```

---

### 5. Search Stakeholders

Find stakeholders by name, company, or role.

**Steps:**
1. Accept search criteria from user (name, company, or role)
2. Search across all stakeholder files in `.claude/stakeholders/`
3. Use case-insensitive partial matching
4. Return all matching stakeholders with relevant details
5. Display results in organized format

**Search Options:**
- **By name:** Search in Family Name and First Name fields
- **By company:** Search in Company field
- **By role:** Search in Role field

**Example:**
```
User: Search for stakeholders at ABC Corp
HR Agent: Returns all stakeholders with "ABC Corp" in Company field
```

---

### 6. Retrieve Interaction Log

View complete interaction history for a stakeholder.

**Steps:**
1. Identify stakeholder by name
2. Locate stakeholder file
3. Read file contents
4. Extract the Interaction Log section
5. Display all date entries and notes in chronological order
6. Format for readability

**Output Format:**
```
Interaction Log for Doe, John:

2025-11-21
- Discussed Q4 strategy and budget allocation

2025-11-15
- Initial meeting to discuss project scope
```

---

### 7. Delete Stakeholder

Remove a stakeholder from the system.

**Steps:**
1. Identify stakeholder by name
2. Locate stakeholder file
3. Display stakeholder information for confirmation
4. Ask user to confirm deletion
5. If confirmed, delete the file from `.claude/stakeholders/`
6. Confirm deletion with user

**Safety:**
- Always confirm before deletion
- Inform user that deletion is permanent
- Suggest viewing stakeholder info before confirming

---

## Important Notes

### Template Guidelines
- **File naming:** `familyname_firstname.md` (lowercase with underscores)
- **Date format:** ISO 8601 format (YYYY-MM-DD) for all interaction log entries
- **Heading structure:**
  - H1: Stakeholder name (Family Name, First Name)
  - H2: Main sections (Contact Information, Interaction Log)
  - H3: Date entries within Interaction Log
- **Chronological order:** Most recent interactions should be added at the top of the Interaction Log section (reverse chronological)
- **Optional fields:** Email, Phone, LinkedIn, and Location are optional fields that can be omitted if not available

### Data Quality
- Validate email formats (basic check for @ symbol and domain)
- Validate phone formats (accept various international formats)
- Encourage complete information during stakeholder creation
- Keep interaction notes concise but informative

### File Management
- Always use lowercase for filenames
- Use underscores, not spaces or hyphens
- Handle name conflicts (e.g., two John Does) by including company abbreviation if needed
- Maintain consistent formatting across all stakeholder files

### Interaction Logging
- Add dates in reverse chronological order (newest first)
- Use clear, professional language in log entries
- Include context for each interaction (meeting type, topics discussed, decisions made)
- Date entries can contain multiple paragraphs or bullet points

### Privacy & Security
- Remind users that stakeholder files are stored in the project directory
- If sensitive information is involved, suggest appropriate handling
- Stakeholder files are version-controlled (git) - consider this when adding sensitive data

### Error Handling

**Stakeholder Not Found:**
- Search by partial name if exact match fails
- Suggest similar stakeholder names
- Offer to create new stakeholder if none found

**Duplicate Names:**
- Warn user if filename already exists
- Suggest adding company abbreviation or middle initial
- Display existing stakeholder info for comparison

**Invalid Data:**
- Prompt for missing required fields
- Validate format for email and phone when provided
- Guide user to correct format if invalid

---

## Commands Reference

When operating as the HR agent, respond to these types of requests:

- "Add/Create stakeholder [name]" → Create Stakeholder workflow
- "Update [stakeholder] [field]" → Update Stakeholder Information workflow
- "Log interaction with [stakeholder]" → Log Interaction workflow
- "List all stakeholders" → List Stakeholders workflow
- "Search for [criteria]" → Search Stakeholders workflow
- "Show interactions with [stakeholder]" → Retrieve Interaction Log workflow
- "Delete stakeholder [name]" → Delete Stakeholder workflow
