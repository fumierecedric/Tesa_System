---
Ticket: 0007
Title: Add Project Stakeholders and Enhance Template
Created: 2025-11-21
Updated: 2025-11-21
Status: In Progress
---

## Overview

Enhance the stakeholder management system by adding LinkedIn and Location fields to the stakeholder template, then create stakeholder files for five project team members and client contacts (Philippe Antoine, Villeret Hugues, de Backer Jonas, Schneider Klara, and Fumière Cédric).

## Analysis

### Problem Understanding

The current stakeholder template lacks two important fields:
1. **LinkedIn profiles** - Essential for professional networking and researching stakeholder backgrounds
2. **Location information** - Important for understanding geographical context, time zones, and planning in-person meetings

Additionally, five key project stakeholders need to be added to the system with their complete information.

### Current State

**Existing Infrastructure:**
- Stakeholder management skill at [.claude/skills/stakeholder-management/skill.md](.claude/skills/stakeholder-management/skill.md)
- HR agent at [.claude/agents/hr.md](.claude/agents/hr.md)
- Stakeholder template at [.claude/skills/stakeholder-management/templates/stakeholder-template.md](.claude/skills/stakeholder-management/templates/stakeholder-template.md)
- Stakeholder files directory at [.claude/stakeholders/](.claude/stakeholders/)

**Current Template Fields:**
- Family Name
- First Name
- Company
- Role
- Email
- Phone
- Interaction Log section

### Gaps to Address

1. **Template Enhancement**: Add LinkedIn and Location fields to the stakeholder template
2. **Skill Documentation**: Update the stakeholder-management skill documentation to reflect new fields
3. **Stakeholder Data**: Create five new stakeholder files with complete information
4. **Data Quality**: Ensure all information is accurately transcribed and properly formatted

## Solution Approach

### Design Philosophy

- **Backwards compatible**: New fields should be optional to not break existing workflows
- **Minimal changes**: Add fields in a logical position without disrupting existing structure
- **Consistent**: Maintain existing naming conventions and formatting patterns
- **Complete**: Ensure all stakeholder data is accurately captured

### Technical Approach

1. Update the stakeholder template to include LinkedIn and Location fields
2. Update the stakeholder-management skill documentation to reference new fields
3. Create five stakeholder files using the enhanced template
4. Verify all data accuracy and formatting consistency

### Key Design Decisions

- **Field positioning**: Add LinkedIn and Location after Phone field, before the Interaction Log separator
- **Optional fields**: LinkedIn and Location are optional (like Email and Phone), allowing flexibility
- **Location format**: Accept any format (city, country, region) to accommodate varying levels of detail
- **Template-only update**: No changes needed to HR agent logic since it uses the template

## Architecture

### Component Structure
```
.claude/
├── agents/
│   └── hr.md (no changes required)
├── skills/
│   └── stakeholder-management/
│       ├── skill.md (update documentation)
│       └── templates/
│           └── stakeholder-template.md (add LinkedIn & Location)
└── stakeholders/
    ├── philippe_antoine.md (new)
    ├── villeret_hugues.md (new)
    ├── de_backer_jonas.md (new)
    ├── schneider_klara.md (new)
    └── fumiere_cedric.md (new)
```

### Workflow Integration

This enhancement integrates seamlessly into existing HR agent workflows:
1. HR agent loads template when creating stakeholders
2. Template now includes LinkedIn and Location fields
3. HR agent populates new fields if provided
4. No changes to core HR agent logic required

### Data Flow

1. **Input**: Stakeholder information from ticket (5 stakeholders with varying data completeness)
2. **Processing**:
   - Update template with new fields
   - For each stakeholder, populate template with available data
   - Save as individual markdown files
3. **Output**: Five new stakeholder files in `.claude/stakeholders/`
4. **Storage**: All files stored in git-versioned directory

## Tasks

### Phase 1: Enhance Template and Documentation
- [x] Update stakeholder template to add LinkedIn field after Phone
- [x] Update stakeholder template to add Location field after LinkedIn
- [x] Update stakeholder-management skill.md to document new fields in "Create Stakeholder" workflow
- [x] Update skill.md "Template Guidelines" section to mention new fields

### Phase 2: Create AJMP Stakeholders
- [x] Create philippe_antoine.md (Client Partner, AJMP)
  - Include: Phone, Email, Role, Company, LinkedIn, Comments
- [x] Create villeret_hugues.md (Subject Matter Expert, AJMP)
  - Include: Email, Phone, Role, Company, LinkedIn, Comments
- [x] Create fumiere_cedric.md (Consultant, AJMP)
  - Include: Company, Email, Phone, Role, LinkedIn, Comments

### Phase 3: Create Tesa Client Stakeholders
- [x] Create de_backer_jonas.md (Digital Campaign Performance Manager, Tesa)
  - Include: Company, Phone, Email, Role, LinkedIn, Location, Comments
- [x] Create schneider_klara.md (Head of Digital Marketing & Communications, Tesa)
  - Include: Company, Email, Role, Comments

### Phase 4: Quality Assurance
- [x] Verify all filenames follow lowercase_underscore convention
- [x] Verify all contact information is correctly formatted
- [x] Verify all LinkedIn URLs are complete and valid
- [x] Verify comments/notes are accurately transcribed
- [x] Verify template structure is consistent across all files

## Dependencies

### External Dependencies
- Existing stakeholder-management skill (ticket 0006)
- Existing HR agent implementation
- Stakeholder template file

### Task Dependencies
- Phase 1 must complete before Phases 2 and 3 (template must be updated first)
- Phases 2 and 3 can be executed in parallel (independent stakeholder creation)
- Phase 4 depends on completion of all previous phases

### Sequential Phases
1. Phase 1: Enhance Template and Documentation
2. Phase 2 & 3: Create Stakeholder Files (parallel)
3. Phase 4: Quality Assurance

## Testing Strategy

### Unit Testing
- Verify template has correct field structure
- Verify each stakeholder file follows template format
- Verify filename conventions are followed

### Integration Testing
- Test that HR agent can read all new stakeholder files
- Test that new fields are properly positioned in the file structure
- Test that optional fields (LinkedIn, Location) work when missing

### Validation Criteria
- [ ] All 5 stakeholder files created in `.claude/stakeholders/`
- [ ] All filenames use format: `familyname_firstname.md` (lowercase)
- [ ] Template includes LinkedIn and Location fields
- [ ] Skill documentation updated to reflect new fields
- [ ] All contact information accurately transcribed
- [ ] All LinkedIn URLs are valid and accessible
- [ ] Comments/notes properly captured for each stakeholder

## Rollout Considerations

### Implementation Order
1. Update template first (ensures all new files use enhanced template)
2. Create AJMP stakeholders (team members first)
3. Create Tesa stakeholders (client contacts)
4. Quality check all files

### Success Metrics
- All 5 stakeholder files successfully created with complete data
- Template enhanced with 2 new optional fields
- Skill documentation accurately reflects new capabilities
- Zero errors in contact information or URLs

### Future Enhancements (Out of Scope)
- Adding "Info" ticket type to backlog management system
- Standardizing Location format (e.g., enforcing "City, Country")
- Adding profile photos or avatars to stakeholder files
- Implementing stakeholder categorization (internal/external, primary/secondary)
- Adding timezone information alongside Location

## Notes

### Design Considerations

**Important Name Clarification:**
- For Philippe Antoine: "Philippe" is the **family name**, "Antoine" is the **first name**
- File should be named: `philippe_antoine.md`
- Heading should be: `# PHILIPPE, Antoine`

**Field Optionality:**
- LinkedIn and Location are optional fields (not all stakeholders have this info)
- Schneider, Klara: Missing phone and LinkedIn
- Several stakeholders missing Location data

**Location Format:**
- No strict format enforced
- Jonas de Backer has "Belgium" (country level)
- Others may have city-level or no location data
- Accept whatever level of detail is available

### References

- Related ticket: [0006_Feature_HR_Agent_Stakeholder_Management.md](.claude/backlog/0_Done/0006_Feature_HR_Agent_Stakeholder_Management.md)
- Stakeholder template: [stakeholder-template.md](.claude/skills/stakeholder-management/templates/stakeholder-template.md)
- HR Agent: [hr.md](.claude/agents/hr.md)
- Stakeholder Management Skill: [skill.md](.claude/skills/stakeholder-management/skill.md)
