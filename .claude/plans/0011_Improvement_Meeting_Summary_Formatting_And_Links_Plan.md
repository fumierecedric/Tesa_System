---
Epic: Project Management
Id: 0011
Title: Meeting Summary Formatting And Links
Type: Improvement
Created: 2025-11-21
Status: In Progress
---

# Execution Plan: Meeting Summary Formatting And Links

## Overview

This plan addresses two improvements to the meeting summary functionality:
1. **Formatting**: Alternate takeaways and discussion points instead of grouping them
2. **Links**: Fix relative links to work from the root folder

## Analysis

### Current State

**Meeting Summary Template** ([.claude/skills/meeting-management/templates/meeting_summary_template.md](.claude/skills/meeting-management/templates/meeting_summary_template.md)):
- Lines 19-24: Key Takeaways section (grouped together)
- Lines 26-32: Discussion Points section (grouped together)
- Currently structured as separate sections

**Link Issue**:
- Example from [20251120-160000 Call Antoine-summary.md](.claude/meetings/summaries/20251120-160000 Call Antoine-summary.md):
- Line 4: `Transcript: [20251120-160000 Call Antoine-transcript.md](.claude/meetings/transcripts/20251120-160000 Call Antoine-transcript.md)`
- Uses relative path from summary location, but user works from root folder
- Need absolute path from repository root

### Target State

**Formatting**:
- Merge Key Takeaways and Discussion Points into a single section
- Alternate between synthetic takeaways and specific discussion points
- Maintain context and flow of the meeting narrative

**Links**:
- All links should use paths relative to repository root
- Example: `/Users/fumierecedric/Library/CloudStorage/Dropbox/Work/Clients/Tesa/202511_Tesa_MA/Tesa_System/.claude/meetings/transcripts/20251120-160000 Call Antoine-transcript.md`
- Or cleaner: `/.claude/meetings/transcripts/20251120-160000 Call Antoine-transcript.md`

## Implementation Phases

### Phase 1: Update Meeting Summary Template ✓

**Objective**: Modify the template to support alternating takeaways and discussion points

**Tasks**:
- [x] Read current template structure
- [x] Design new section that combines takeaways and discussion points
- [x] Update template with new "Key Points and Discussion" section
- [x] Add instructions for alternating format
- [x] Update placeholder examples to show alternating pattern
- [x] Fix transcript link to use absolute path from root

**Files to modify**:
- `.claude/skills/meeting-management/templates/meeting_summary_template.md`

**Changes**:
1. Replace separate "Key Takeaways" and "Discussion Points" sections with unified section
2. New section: "## Key Points and Discussion"
3. Format: Alternate between synthetic takeaways (bullets) and specific quotes (with names)
4. Update template instructions to reflect new format
5. Change line 4 transcript link from relative to absolute path format

### Phase 2: Update Skill Documentation ✓

**Objective**: Update skill.md to reflect the new template structure

**Tasks**:
- [x] Read skill.md workflow descriptions
- [x] Update Workflow 3 (Meeting Transcript Summarization) instructions
- [x] Modify step 4-5 to describe alternating format instead of separate sections
- [x] Update examples to show new format
- [x] Ensure consistency across all workflow references

**Files to modify**:
- `.claude/skills/meeting-management/skill.md`

**Changes**:
1. Update step descriptions for extracting takeaways and discussion points
2. Explain alternating pattern in workflow steps
3. Update example outputs to match new format

### Phase 3: Update Existing Meeting Summaries ✓

**Objective**: Retroactively update existing meeting summaries to new format

**Tasks**:
- [x] Identify all existing summary files
- [x] For each summary:
  - [x] Read current content
  - [x] Merge takeaways and discussion points into alternating format
  - [x] Fix transcript link to absolute path
  - [x] Preserve all information (no data loss)
- [x] Verify all summaries are updated

**Files to modify**:
- `.claude/meetings/summaries/20251120-160000 Call Antoine-summary.md`
- `.claude/meetings/summaries/20251121-120000 Onboarding Hugues-summary.md`

**Changes**:
1. Replace separate sections with unified "Key Points and Discussion"
2. Interleave takeaways and discussion points chronologically
3. Update transcript links to absolute paths

### Phase 4: Test and Validate ✓

**Objective**: Verify the changes work as expected

**Tasks**:
- [x] Test link clickability from root folder
- [x] Verify new template structure is clear and usable
- [x] Review updated summaries for readability
- [x] Ensure no information was lost in restructuring
- [x] Confirm alternating format improves flow and context

**Validation Criteria**:
1. Links are clickable from repository root
2. Alternating format maintains meeting narrative flow
3. Template instructions are clear
4. Skill documentation accurately describes new format
5. Existing summaries are correctly updated

## Technical Considerations

### Link Path Format

**Option 1**: Absolute filesystem path
```markdown
[transcript](/Users/fumierecedric/Library/CloudStorage/Dropbox/Work/Clients/Tesa/202511_Tesa_MA/Tesa_System/.claude/meetings/transcripts/20251120-160000 Call Antoine-transcript.md)
```

**Option 2**: Repository-root-relative path (PREFERRED)
```markdown
[transcript](.claude/meetings/transcripts/20251120-160000 Call Antoine-transcript.md)
```
- Simpler, cleaner
- Works when VSCode workspace is at repository root
- More portable across environments

### Alternating Format Pattern

**Strategy**: Chronological flow
- Follow the meeting timeline
- Interleave synthetic summaries with specific attributions
- Example pattern:
  ```markdown
  - JMP specializes in marketing transformation (takeaway)
  - **Antoine**: Explained JMP's mission - created 5 years ago... (discussion)
  - Workshop scheduled for November 3-4 (takeaway)
  - **Cédric**: Confirmed availability for workshop dates (discussion)
  ```

**Benefits**:
- Better narrative flow
- Context preservation
- Easier to follow meeting progression
- Connects decisions to discussions

## Risks and Mitigations

| Risk | Impact | Mitigation |
|------|--------|-----------|
| Breaking existing workflows that rely on separate sections | Medium | Review skill.md and commands that reference these sections |
| Information loss during restructuring | High | Carefully preserve all content, verify each update |
| Link format incompatibility with IDE | Medium | Test link clickability in VSCode before finalizing |
| Confusion about new format for future summaries | Medium | Clear template instructions and examples |

## Success Criteria

- [x] Meeting summary template uses alternating format
- [x] Template uses absolute paths for transcript links
- [x] Skill documentation reflects new structure
- [x] All existing summaries updated to new format
- [x] Links are clickable from repository root
- [x] No information lost in restructuring
- [x] Format improves readability and context

## Implementation Notes

- Prioritize Phase 1 and 2 (template and docs) before updating existing summaries
- Test link format early to avoid rework
- Maintain backup mindset: all original information must be preserved
- Consider adding migration notes to skill.md for historical context

---

**Plan Status**: ✅ Completed
**Estimated Complexity**: Low-Medium
**Key Dependencies**: None

## Implementation Summary

All phases completed successfully:
1. ✅ Template updated with alternating format and corrected link paths
2. ✅ Skill documentation updated to reflect new workflow
3. ✅ Both existing meeting summaries migrated to new format
4. ✅ All changes validated and tested
