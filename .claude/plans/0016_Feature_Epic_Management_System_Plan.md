---
Ticket: 0016
Title: Epic Management System
Created: 2025-11-22
Updated: 2025-11-22
Status: Completed
---

## Overview

Implement a comprehensive epic management system within the backlog management skill that enables the Product Owner to organize tickets under high-level business objectives (epics), maintain automatic ticket-epic relationships, and navigate seamlessly between epics and their associated tickets.

## Analysis

### Problem Understanding

Currently, the backlog management system lacks the ability to group related tickets under higher-level business objectives or themes. This makes it difficult to:
- Understand strategic initiatives at a glance
- Track progress on larger features or projects
- Navigate between related tickets
- Maintain organization as the backlog grows

### Current State

The existing backlog management skill provides:
- Ticket CRUD operations (Initialize, Prepare, Update, Close)
- Template-based ticket creation
- Status-based folder structure (0_Done, 1_WIP, 2_To_Do, etc.)
- Ticket metadata including Epic field (currently just a text field with no enforcement or linking)

### Gaps to Address

1. No dedicated storage or structure for epic definitions
2. No workflows to create, update, delete, or list epics
3. Epic field in tickets is free-text with no validation or linking
4. No ability to view all tickets belonging to an epic
5. No automatic updates when tickets reference an epic
6. No clickable navigation from epics to tickets

## Solution Approach

### Design Philosophy

- **Lightweight**: Use markdown files with minimal overhead
- **Integrated**: Leverage existing backlog management skill structure
- **Automated**: Auto-update epic-ticket relationships
- **Navigable**: Enable VSCode-native navigation with clickable links

### Technical Approach

1. Create epic storage structure (`.claude/epics/`)
2. Define epic template with metadata and ticket listing
3. Implement epic CRUD workflows in backlog management skill
4. Enhance "Prepare Ticket" workflow to update epic when tickets are created
5. Update Product Owner agent documentation

### Key Design Decisions

- **Epic Storage Location**: `.claude/epics/` (separate from backlog for clarity)
- **Epic Filename Convention**: `{epic_name_snake_case}.md` (no IDs needed, epics are long-lived)
- **Epic-Ticket Linking**: Bidirectional - tickets reference epic in metadata, epics list tickets with clickable links
- **Auto-Update Strategy**: When creating/updating tickets, automatically update the referenced epic's ticket list
- **Link Format**: Use relative paths from root directory for VSCode compatibility

## Architecture

### Component Structure
```
.claude/
├── epics/                          # Epic storage
│   ├── project_management.md       # First epic
│   └── [other_epics].md
├── skills/
│   └── backlog-management/
│       ├── skill.md                # Enhanced with epic workflows
│       └── templates/
│           ├── ticket-template.md  # Existing
│           └── epic-template.md    # NEW
├── backlog/
│   ├── 0_Done/
│   ├── 1_WIP/
│   └── ...                         # Existing structure
└── agents/
    └── product-owner.md            # Updated documentation
```

### Workflow Integration

```
Create Ticket Flow:
1. User requests ticket creation
2. Product Owner asks clarifying questions (including Epic)
3. Ticket created in backlog with Epic metadata
4. Epic file automatically updated with new ticket reference ← NEW
5. Ticket confirmation returned

Epic Management Flow:
1. User requests epic operation (create/update/delete/list)
2. Product Owner executes epic workflow
3. Epic file created/modified/deleted in .claude/epics/
4. Confirmation returned

View Epic Progress:
1. User opens epic file in .claude/epics/
2. Epic shows metadata and clickable ticket list
3. User clicks ticket link → VSCode opens ticket file
```

### Data Flow

1. **Input**: User creates/updates ticket with Epic field populated
2. **Processing**:
   - Ticket saved to backlog with Epic metadata
   - Epic file located in `.claude/epics/`
   - Epic's ticket list section updated with new ticket reference
   - Link formatted as `[TICKET_ID: Title](.claude/backlog/{status}/{filename}.md)`
3. **Output**: Updated epic file with new ticket listed
4. **Storage**: Epic files in `.claude/epics/`, tickets in `.claude/backlog/`

## Tasks

### Phase 1: Foundation Setup
- [x] Task 1.1: Create epic template
  - Create `.claude/skills/backlog-management/templates/epic-template.md`
  - Include: Epic Name, Description, Related Tickets section
  - Use markdown with frontmatter for metadata
- [x] Task 1.2: Create epics storage folder
  - Create `.claude/epics/` directory
  - Add README.md explaining epic structure (optional but recommended)
- [x] Task 1.3: Create first epic file
  - Create `.claude/epics/project_management.md`
  - Use template with Epic Name: "Project Management"
  - Add description about backlog and project management system enhancements

### Phase 2: Epic CRUD Workflows
- [x] Task 2.1: Implement "Create Epic" workflow
  - Add workflow to `.claude/skills/backlog-management/skill.md`
  - Load template, replace placeholders
  - Save to `.claude/epics/{epic_name_snake_case}.md`
  - Include input validation (epic name uniqueness)
- [x] Task 2.2: Implement "Update Epic" workflow
  - Add workflow to locate and modify epic files
  - Support updating Name, Description, and manual ticket list adjustments
  - Update the "Updated" date in epic metadata
- [x] Task 2.3: Implement "Delete Epic" workflow
  - Add workflow to remove epic file
  - Include safety check: warn if epic has associated tickets
  - Optionally offer to unlink tickets or block deletion
- [x] Task 2.4: Implement "List Epics" workflow
  - Add workflow to scan `.claude/epics/` directory
  - Display all epics with names, descriptions, and ticket counts
  - Support filtering and sorting options

### Phase 3: Ticket-Epic Integration
- [x] Task 3.1: Enhance "Prepare Ticket" workflow
  - After creating ticket, check if Epic field is populated
  - If Epic exists, locate epic file in `.claude/epics/`
  - Append ticket reference to epic's "Related Tickets" section
  - Use format: `- [TICKET_ID: Title](.claude/backlog/{status}/{filename}.md)`
  - Update epic's "Updated" date
- [x] Task 3.2: Implement "List Tickets by Epic" functionality
  - Add workflow to read epic file
  - Parse and display all tickets listed in the epic
  - Show ticket ID, Title, Status, Priority
  - Provide clickable links to ticket files
- [x] Task 3.3: Handle ticket status changes
  - When tickets move between folders (e.g., 1_WIP → 0_Done)
  - Update ticket references in epic file to reflect new path
  - Ensure links remain functional after status changes
- [x] Task 3.4: Add epic validation on ticket creation
  - When user specifies Epic during ticket creation
  - Validate that epic exists in `.claude/epics/`
  - If epic doesn't exist, offer to create it or warn user
  - Prevent orphaned epic references

### Phase 4: Documentation and Testing
- [x] Task 4.1: Update Product Owner agent documentation
  - Add epic management responsibilities to `.claude/agents/product-owner.md`
  - Document when and how to use epic workflows
  - Include examples of epic creation and ticket linking
- [x] Task 4.2: Update backlog management skill documentation
  - Ensure all new workflows are clearly documented
  - Add usage examples for each epic workflow
  - Document epic template structure and placeholders
- [x] Task 4.3: Test epic creation workflow
  - Create test epic
  - Verify file created in correct location
  - Validate template placeholders replaced correctly
- [x] Task 4.4: Test ticket-epic integration
  - Create test ticket with epic reference
  - Verify epic file updated with ticket link
  - Click link to ensure navigation works
  - Move ticket to different status folder and verify link updates
- [x] Task 4.5: Test epic CRUD operations
  - Update epic (modify description)
  - List all epics
  - Delete test epic
  - Verify all operations work as expected

## Dependencies

### External Dependencies
- None (uses existing markdown and file system capabilities)

### Task Dependencies
- Task 1.1 must complete before Task 2.1 (template needed for create workflow)
- Task 1.2 must complete before Task 1.3 (folder needed for epic file)
- Phase 1 must complete before Phase 2 (foundation needed for workflows)
- Phase 2 must complete before Phase 3 (epic workflows needed before ticket integration)
- Task 2.1 must complete before Task 3.1 (create epic workflow needed for validation)

### Sequential Phases
1. Phase 1: Foundation Setup
2. Phase 2: Epic CRUD Workflows
3. Phase 3: Ticket-Epic Integration
4. Phase 4: Documentation and Testing

## Testing Strategy

### Unit Testing
- Test epic template creation with various epic names
- Test epic file creation with special characters in names
- Test ticket link formatting with different ticket statuses
- Test epic validation when ticket references non-existent epic

### Integration Testing
- Test full workflow: Create epic → Create ticket → Verify epic updated → Click link
- Test ticket status change: Create ticket → Move to Done → Verify epic link updated
- Test edge cases:
  - Epic with no tickets
  - Ticket with no epic
  - Multiple tickets referencing same epic
  - Epic deletion with associated tickets

### Validation Criteria
- [ ] All epic CRUD operations work correctly
- [ ] Tickets automatically update epic files upon creation
- [ ] Links from epic to tickets are clickable and functional
- [ ] Epic validation prevents orphaned references
- [ ] Documentation is clear and complete
- [ ] Product Owner agent can execute all epic workflows

## Rollout Considerations

### Implementation Order
1. Start with Phase 1 (minimal viable structure)
2. Add Phase 2 (core CRUD functionality)
3. Integrate Phase 3 (automatic ticket linking - the key value add)
4. Complete Phase 4 (polish with documentation and testing)

### Success Metrics
- Epic files created successfully in `.claude/epics/`
- Ticket creation automatically updates epic files
- Links are functional and navigate correctly in VSCode
- Product Owner can manage epics without manual file editing
- All acceptance criteria from ticket 0016 are met

### Future Enhancements (Out of Scope)
- Epic-level progress tracking (e.g., % complete based on ticket statuses)
- Epic hierarchy (parent-child epics)
- Epic archival workflow
- Epic templates for different project types
- Visualization of epic-ticket relationships (diagram generation)
- Search and filter capabilities across epics

## Notes

### Design Considerations

**Link Path Strategy**: Using relative paths from root directory (e.g., `.claude/backlog/1_WIP/0016_Feature_Epic_Management_System.md`) ensures compatibility with VSCode's markdown link navigation. This allows users to Cmd+Click (Mac) or Ctrl+Click (Windows) to open files directly.

**Epic Naming Convention**: Unlike tickets, epics don't need numeric IDs because they represent long-lived strategic themes. Using descriptive snake_case names (e.g., `project_management.md`) makes them more readable and meaningful.

**Auto-Update Trade-offs**: Automatically updating epic files when tickets are created/moved adds complexity but provides significant value by keeping epic-ticket relationships in sync. The alternative (manual updates) is error-prone and defeats the purpose of automation.

**Status Change Handling**: When tickets change status (and thus folder location), their links in epic files must update. This requires the "Update Ticket" or "Close Ticket" workflows to also update the epic file. This is critical for maintaining link integrity.

**Epic Validation**: When a user specifies an epic during ticket creation, we should validate that the epic exists. This prevents orphaned references and maintains data integrity. Offering to create the epic on-the-fly provides a good UX.

### References
- Related ticket: [.claude/backlog/1_WIP/0016_Feature_Epic_Management_System.md](.claude/backlog/1_WIP/0016_Feature_Epic_Management_System.md)
- Backlog management skill: [.claude/skills/backlog-management/skill.md](.claude/skills/backlog-management/skill.md)
- Product Owner agent: [.claude/agents/product-owner.md](.claude/agents/product-owner.md)
- Ticket template: [.claude/skills/backlog-management/templates/ticket-template.md](.claude/skills/backlog-management/templates/ticket-template.md)
