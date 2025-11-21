# Ticket 0007: Add Project Stakeholders and Enhance Template

**Epic:** Stakeholder Management
**Type:** Improvement
**Priority:** Medium
**Sprint:** None
**Status:** 0_Done
**Created:** 2025-11-21
**Updated:** 2025-11-21

---

## User Story

As an HR agent, I want to add the five project stakeholders and enhance the stakeholder template with LinkedIn and Location fields so that I can maintain comprehensive stakeholder information for the Tesa project.

---

## Description

This ticket covers two related improvements to the stakeholder management system:

1. **Add five new project stakeholders** with their complete information
2. **Enhance the stakeholder template** to include LinkedIn profile URLs and Location fields

These enhancements will provide more complete stakeholder profiles and better support for managing the project team and client contacts.

---

## Initial Request

Original requirements from note file `.claude/backlog/2_To_Do/info_stakeholders.md`:

### Stakeholders to Add:

1. **Philippe, Antoine**
   - Phone: +32 479 19 55 74
   - Email: antoine@ajmp.be
   - Role: Client Partner
   - Company: AJMP
   - LinkedIn: https://www.linkedin.com/in/apjm55/
   - Comments: Handles the relationship with the client (Tesa)

2. **Villeret, Hugues**
   - Email: hvilleret@gmail.com
   - Phone: +32 488 58 60 73
   - Role: Subject Matter Expert
   - Company: AJMP
   - LinkedIn: https://www.linkedin.com/in/marketinghvilleret/
   - Comments: Was initially involved in project as main consultant, has deep expertise in marketing automation and CRM

3. **de Backer, Jonas**
   - Company: Tesa
   - Phone: +32 (0)499 31 44 12
   - Email: Jonas.DeBacker@tesa.com
   - Role: Digital Campaign Performance Manager
   - LinkedIn: https://www.linkedin.com/in/jonas-de-backer/
   - Location: Belgium
   - Comments: Day-to-day contact, collaborates with Cédric on setting up the workshop

4. **Schneider, Klara**
   - Company: Tesa
   - Email: klara.schneider@tesa.com
   - Role: Head of Digital Marketing & Communications
   - Comments: Main decision maker on the client side, sponsor

5. **Fumière, Cédric**
   - Company: AJMP
   - Email: cedric@ajmp.be
   - Phone: +32 479779909
   - Role: Consultant
   - LinkedIn: https://www.linkedin.com/in/fumierecedric/
   - Comments: Main consultant on the project, collaborates with Jonas on setting up the workshop

### Template Enhancements:
- Add **LinkedIn** field to the stakeholder template
- Add **Location** field to the stakeholder template

### Additional Note:
- Consider adding a new ticket type: "Info" (to be addressed separately)

---

## Acceptance Criteria

### 1. Add New Stakeholders
- [x] Create stakeholder file for Philippe Antoine (AJMP - Client Partner)
- [x] Create stakeholder file for Villeret Hugues (AJMP - Subject Matter Expert)
- [x] Create stakeholder file for de Backer Jonas (Tesa - Digital Campaign Performance Manager)
- [x] Create stakeholder file for Schneider Klara (Tesa - Head of Digital Marketing & Communications)
- [x] Create stakeholder file for Fumière Cédric (AJMP - Consultant)
- [x] All files created in `.claude/stakeholders/` directory
- [x] Files named using format: `familyname_firstname.md`

### 2. Enhance Stakeholder Template
- [x] Add LinkedIn field to the stakeholder-management skill template
- [x] Add Location field to the stakeholder-management skill template
- [x] Update the skill documentation to reflect the new fields
- [x] Ensure HR agent can populate these new fields when creating/updating stakeholders

### 3. Data Quality
- [x] All stakeholder information accurately transcribed from the note file
- [x] Contact information (email, phone) correctly formatted
- [x] LinkedIn URLs are valid and working
- [x] Comments/notes properly captured for each stakeholder

---

## Technical Notes

- **Family name clarification**: Philippe is the family name, Antoine is the first name (file should be `philippe_antoine.md`)
- LinkedIn and Location fields should be optional (not all stakeholders have this information)
- Location field can be as specific or general as needed (city, country, region)
- The HR agent's stakeholder-management skill needs to be updated to handle the new fields

---

## Dependencies

- Existing stakeholder-management skill (from ticket 0006)
- Existing HR agent implementation

---

## Related Tickets

- **0006**: HR Agent Stakeholder Management (parent feature)

---

## Future Considerations

- Adding "Info" as a new ticket type (separate ticket may be needed)
- Standardizing location format (e.g., City, Country)
- Adding profile photos or other visual elements to stakeholder files
