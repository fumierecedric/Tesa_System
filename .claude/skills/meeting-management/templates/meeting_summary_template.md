---
Meeting: {{MEETING_NAME}}
Date: {{MEETING_DATE}}
Transcript: {{TRANSCRIPT_PATH}}
Created: {{CREATED_DATE}}
---

# Meeting Summary: {{MEETING_NAME}}

## Main Topics Discussed

<!-- List 3-5 main topics with a few words each. Be concise. -->

1. {{TOPIC_1}}
2. {{TOPIC_2}}
3. {{TOPIC_3}}

## Key Takeaways

<!-- Synthetic bullet points capturing the essence of decisions and important information. Be concise and actionable. -->

- {{TAKEAWAY_1}}
- {{TAKEAWAY_2}}
- {{TAKEAWAY_3}}

## Discussion Points

<!-- Document who said what crucial information. Focus only on key contributors and important statements. Format: "**Name**: Statement or contribution" -->

- **{{PARTICIPANT_1}}**: {{CRUCIAL_INFO_1}}
- **{{PARTICIPANT_2}}**: {{CRUCIAL_INFO_2}}
- **{{PARTICIPANT_3}}**: {{CRUCIAL_INFO_3}}

## Action Points

<!-- Clear, actionable items with owner if identified. Format: "- Action description (Owner: Name)" or "- Action description" -->

- [ ] {{ACTION_1}}
- [ ] {{ACTION_2}}
- [ ] {{ACTION_3}}

## Suggestions for Information Extraction

<!-- Identify what information should be extracted from this meeting and which agent should handle it. This helps with systematic follow-up. -->

### Stakeholder Information (HR Agent)
<!-- List any new stakeholders mentioned or updates to existing stakeholder information -->
- {{STAKEHOLDER_EXTRACTION_1}}

### Knowledge Entries (Knowledge Manager Agent)
<!-- List important knowledge, decisions, or processes that should be documented -->
- {{KNOWLEDGE_EXTRACTION_1}}

### Meeting Preparation (Meeting Assistant Agent)
<!-- List any follow-up meetings that need preparation -->
- {{MEETING_PREP_1}}

---

## Instructions for Use

1. **Be concise and synthetic**: Summaries should capture essence, not transcribe everything
2. **Focus on crucial information**: Not every statement needs to be documented
3. **Main Topics**: 3-5 topics maximum, each described in a few words
4. **Key Takeaways**: Synthetic bullet points highlighting decisions and important information
5. **Discussion Points**: Only document crucial contributions that add context or drive decisions
6. **Action Points**: Clear, actionable items - use checkboxes for tracking
7. **Suggestions**: Identify extraction opportunities for systematic follow-up by specialized agents
8. **File naming**: Save as `YYYYMMDD-HHMMSS MeetingName-summary.md` (replace `-transcript` with `-summary`)
9. **Location**: Save to `.claude/meetings/summaries/`
