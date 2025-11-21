# Execution Plan: Rename HR To Stakeholder Manager

**Ticket ID**: 0015
**Type**: Improvement
**Epic**: Project Management
**Priority**: Low
**Created**: 2025-11-21
**Status**: In Progress

---

## Overview

This plan outlines the systematic renaming of the HR agent to "Stakeholder Manager" across the entire codebase. The exploration phase identified 26 files containing HR agent references across agent definitions, documentation, skills, backlog items, logs, and meeting summaries.

---

## Scope Analysis

### Files Requiring Updates (26 total)

**Category 1: Agent Definition & Core Files (3 files)**
1. `.claude/agents/hr.md` - Agent definition file (needs rename + content update)
2. `.claude/agents/solution-designer.md` - References HR in coordination section
3. `.claude/agents/meeting-assistant.md` - References HR for stakeholder extraction

**Category 2: Documentation (2 files)**
4. `.claude/agents/README.md` - HR Agent section documentation
5. `.claude/stakeholders/README.md` - References HR agent usage

**Category 3: Skills (2 files)**
6. `.claude/skills/stakeholder-management/skill.md` - Main skill definition
7. `.claude/skills/README.md` - Stakeholder Management section

**Category 4: Backlog & Historical Records (2 files)**
8. `.claude/backlog/0_Done/0006_Feature_HR_Agent_Stakeholder_Management.md` - Original feature ticket
9. `.claude/backlog/1_WIP/0015_Improvement_Rename_HR_To_Stakeholder_Manager.md` - Current ticket

**Category 5: Implementation History (2 files)**
10. `.claude/plans/0006_Feature_HR_Agent_Stakeholder_Management_Plan.md` - Original execution plan
11. `.claude/logs/0006_Feature_HR_Agent_Stakeholder_Management_Log.md` - Original development log

**Category 6: Meeting References (1 file)**
12. `.claude/meetings/summaries/20251120-160000 Call Antoine-summary.md` - Meeting summary

**Category 7: Related Agent Files (3+ files)**
13. `.claude/agents/knowledge-manager.md` - References HR integration
14. Additional coordination references in other agents

---

## Implementation Phases

### Phase 1: Rename Core Agent File ✓ Rename File
- [ ] Rename `.claude/agents/hr.md` to `.claude/agents/stakeholder-manager.md`
- [ ] Update frontmatter and all internal content references from "HR" to "Stakeholder Manager"
- [ ] Update role title, responsibilities, and working style sections
- [ ] Verify skill reference remains correct (stakeholder-management)

**Deliverable**: `.claude/agents/stakeholder-manager.md`

---

### Phase 2: Update Agent Documentation ✓ Update References
- [ ] Update `.claude/agents/README.md`:
  - Rename "HR Agent" section to "Stakeholder Manager Agent"
  - Update all references in purpose, skills, use cases
  - Update example interactions and command references
- [ ] Update `.claude/agents/solution-designer.md`:
  - Rename "HR Agent" subsection in Agent Coordination
  - Update recommendation guidelines and task examples
- [ ] Update `.claude/agents/meeting-assistant.md`:
  - Update stakeholder extraction delegation references
  - Change "HR agent" to "Stakeholder Manager agent"
- [ ] Update `.claude/agents/knowledge-manager.md`:
  - Update integration references to Stakeholder Manager

**Deliverables**: Updated agent documentation files

---

### Phase 3: Update Skills & Templates ✓ Update Skill References
- [ ] Update `.claude/skills/stakeholder-management/skill.md`:
  - Update agent name references in overview
  - Update workflow descriptions mentioning HR
  - Verify all 7 workflows reference Stakeholder Manager
- [ ] Update `.claude/skills/README.md`:
  - Rename section from HR-focused to Stakeholder Manager
  - Update workflow descriptions and agent references
- [ ] Review `.claude/skills/stakeholder-management/templates/stakeholder-template.md`:
  - Check for any HR references (likely none, but verify)
- [ ] Update `.claude/stakeholders/README.md`:
  - Update agent name references

**Deliverables**: Updated skill documentation and templates

---

### Phase 4: Update Historical Records ✓ Update Backlog & Logs
- [ ] Update `.claude/backlog/0_Done/0006_Feature_HR_Agent_Stakeholder_Management.md`:
  - Add note at top indicating historical reference
  - Optionally update title to reflect current naming
- [ ] Update `.claude/plans/0006_Feature_HR_Agent_Stakeholder_Management_Plan.md`:
  - Add historical note
  - Optionally update agent references
- [ ] Update `.claude/logs/0006_Feature_HR_Agent_Stakeholder_Management_Log.md`:
  - Add historical note
  - Optionally update agent references
- [ ] Leave current ticket (0015) as-is until completion

**Deliverables**: Updated historical records with notes

---

### Phase 5: Update Meeting References ✓ Update Meeting Summaries
- [ ] Update `.claude/meetings/summaries/20251120-160000 Call Antoine-summary.md`:
  - Change "Stakeholder Information (HR Agent)" to "Stakeholder Information (Stakeholder Manager Agent)"
  - Update all 3 references (lines 34, 70, 103)

**Deliverables**: Updated meeting summary

---

### Phase 6: Verification & Testing ✓ Comprehensive Verification
- [ ] Search for remaining "HR agent" references:
  - Case-insensitive grep for "HR agent", "hr agent", "HR Agent"
  - Check for "HR" in isolation that might be missed
- [ ] Verify file paths are consistent:
  - Check all imports/references to agent file
  - Verify no broken links in documentation
- [ ] Functional verification:
  - Confirm stakeholder management workflows still function
  - Test agent invocation with new name
  - Verify slash commands and skills work correctly
- [ ] Review acceptance criteria:
  - All agent code/implementation files updated
  - All documentation updated
  - All configuration files updated
  - Meeting notes updated
  - Test files updated (if any exist)
  - File paths consistent
  - Agent functions correctly
  - No broken references

**Deliverables**: Verification report, all acceptance criteria met

---

## Technical Considerations

### Search Patterns to Use
- "HR agent" (case variations)
- "HR Agent"
- "hr.md"
- File path references to `agents/hr.md`

### Naming Conventions
- **Old**: HR, HR Agent, hr
- **New**: Stakeholder Manager, Stakeholder Manager Agent, stakeholder-manager

### File Naming
- **Agent file**: `hr.md` → `stakeholder-manager.md`
- **Skill**: Remains `stakeholder-management` (already correctly named)
- **Folder**: `.claude/stakeholders/` (no change needed)

### Backward Compatibility
- No backward compatibility needed (internal project)
- Historical records will be updated with notes for context
- Old ticket/log titles can reference original naming for historical accuracy

---

## Risk Assessment

**Low Risk Factors**:
- Internal project with no external API
- Clear, systematic renaming pattern
- Comprehensive search identified all references
- No complex dependencies or imports

**Mitigation**:
- Thorough grep verification after changes
- Test agent functionality after rename
- Preserve historical context in old tickets/logs

---

## Dependencies

- None identified
- Can be executed independently

---

## Estimated Effort

- **Phase 1**: 10 minutes (1 file rename + content updates)
- **Phase 2**: 15 minutes (4 documentation files)
- **Phase 3**: 15 minutes (4 skill-related files)
- **Phase 4**: 10 minutes (3 historical files with notes)
- **Phase 5**: 5 minutes (1 meeting summary)
- **Phase 6**: 15 minutes (verification and testing)

**Total**: ~70 minutes

---

## Success Criteria

- ✓ Agent file renamed from `hr.md` to `stakeholder-manager.md`
- ✓ All 26 identified files updated with new agent name
- ✓ No remaining "HR agent" references in active codebase
- ✓ All documentation consistent with new naming
- ✓ Agent functions correctly with new name
- ✓ All acceptance criteria from ticket 0015 met
- ✓ Historical records preserved with contextual notes

---

## Notes

- This is a straightforward refactoring task with clear scope
- The exploration phase was comprehensive and identified all references
- Historical accuracy is maintained through contextual notes
- The skill name (stakeholder-management) is already appropriate and won't change
