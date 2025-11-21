# Summarize Meeting Command

Execute the "Meeting Transcript Summarization" workflow from the meeting-management skill to create a structured summary from a meeting transcript file.

## Purpose

This command provides a simple interface to automatically generate high-quality meeting summaries from transcript files. It leverages the meeting-management skill's Workflow 3 to create consistent, concise summaries using the standardized meeting summary template.

## Usage

```
/summarize-meeting <transcript_file_path>
```

**Parameters**:
- `<transcript_file_path>` (required): Path to the meeting transcript markdown file
  - Supports absolute or relative paths
  - Supports @file notation for IDE integration
  - Must be a markdown (.md) file

**Examples**:

```bash
# With direct file path
/summarize-meeting .claude/meetings/transcripts/20251121-143000 SteerCo Meeting-transcript.md

# With @file notation
/summarize-meeting @.claude/meetings/transcripts/20251121-143000 SteerCo Meeting-transcript.md
```

## What This Command Does

1. **Validates input**: Ensures a file path is provided and the file exists
2. **Checks file format**: Confirms the file is a markdown (.md) file
3. **Invokes meeting-management skill**: Triggers Workflow 3 (Meeting Transcript Summarization)
4. **Generates summary**: Creates a structured summary using the meeting summary template
5. **Saves output**: Stores the summary in `.claude/meetings/summaries/` with proper naming

## Expected Output

The command will create a summary file with:
- **Location**: `.claude/meetings/summaries/`
- **Naming**: Same as transcript filename with `-transcript` replaced by `-summary`
  - Example: `20251121-143000 SteerCo Meeting-transcript.md` → `20251121-143000 SteerCo Meeting-summary.md`
- **Format**: Structured markdown following the meeting summary template

## Instructions for Claude

When this command is invoked:

### Step 1: Validate Parameters

1. **Check if file path parameter is provided**
   - If missing: Display error message
     ```
     Error: Missing required parameter <transcript_file_path>

     Usage: /summarize-meeting <transcript_file_path>

     Example: /summarize-meeting .claude/meetings/transcripts/20251121-143000 Meeting-transcript.md
     ```

2. **Check if file exists**
   - Use the provided file path (handle @file notation if present)
   - If file not found: Display error message
     ```
     Error: Transcript file not found at path: <provided_path>

     Please verify:
     - The file path is correct
     - The file exists in .claude/meetings/transcripts/
     - You have permission to access the file
     ```

3. **Validate file extension**
   - Check if file has .md extension
   - If wrong extension: Display error message
     ```
     Error: Invalid file format. Only markdown (.md) transcript files are supported.

     Provided file: <filename>
     Expected format: *.md

     Please provide a markdown transcript file from .claude/meetings/transcripts/
     ```

### Step 2: Invoke Meeting Management Skill

If all validations pass:

1. **Use the Skill tool** to invoke the meeting-management skill
2. **Provide context** to the skill:
   ```
   Execute Workflow 3: Meeting Transcript Summarization

   Transcript file path: <validated_file_path>

   Instructions:
   - Read the transcript from the provided path
   - Load the summary template from .claude/skills/meeting-management/templates/meeting_summary_template.md
   - Follow all steps in Workflow 3 to generate a comprehensive summary
   - Save the summary to .claude/meetings/summaries/ with proper naming convention
   - Confirm completion and report summary location
   ```

3. **Let the skill handle all summarization logic**
   - The skill will read the transcript
   - Extract main topics, key takeaways, discussion points, action items
   - Populate the template
   - Save the summary file
   - Report completion

### Step 3: Confirm Completion

After the skill completes:

1. **Report success** to the user with summary location
2. **Highlight key information** if appropriate (optional)
3. **Suggest next steps** based on action items or extraction suggestions (optional)

## Error Handling

Handle these scenarios gracefully:

- **Missing parameter**: Provide usage help
- **File not found**: Give clear path information
- **Wrong file format**: Explain format requirements
- **Skill invocation failure**: Surface the error from the skill
- **Summary creation failure**: Display skill error message

## File Naming Convention

**Input (Transcript)**:
- Format: `YYYYMMDD-HHMMSS MeetingName-transcript.md`
- Location: `.claude/meetings/transcripts/`

**Output (Summary)**:
- Format: `YYYYMMDD-HHMMSS MeetingName-summary.md`
- Location: `.claude/meetings/summaries/`
- Note: The skill automatically handles the filename transformation

## Related Documentation

- Meeting Management Skill: [.claude/skills/meeting-management/skill.md](.claude/skills/meeting-management/skill.md)
- Meeting Summary Template: [.claude/skills/meeting-management/templates/meeting_summary_template.md](.claude/skills/meeting-management/templates/meeting_summary_template.md)
- Workflow 3 Details: See "Meeting Transcript Summarization" section in skill.md

## Notes

- This command is a lightweight interface to the meeting-management skill
- All summarization logic is handled by the skill (Workflow 3)
- The command focuses on parameter validation and skill invocation
- Summary quality follows the skill's guidelines: concise, synthetic, and structured
