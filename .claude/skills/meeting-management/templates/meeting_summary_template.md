---
Meeting: {{MEETING_NAME}}
Date: {{MEETING_DATE}}
Transcript: [{{MEETING_NAME}}-transcript.md](.claude/meetings/transcripts/{{TRANSCRIPT_FILENAME}})
Created: {{CREATED_DATE}}
---

# {{MEETING_NAME}}

## {{TOPIC_1_TITLE}}

### Takeaways

<!-- Short, crisp bullet points capturing the essence of this topic -->

- {{TOPIC_1_SUMMARY_POINT_1}}
- {{TOPIC_1_SUMMARY_POINT_2}}

### Details

<!-- Key contributions and details from participants, maintaining chronological order within this topic -->

- **{{PARTICIPANT_1}}**: {{TOPIC_1_DETAIL_1}}
- **{{PARTICIPANT_2}}**: {{TOPIC_1_DETAIL_2}}

### Action Points

<!-- Clear, actionable items with owner assignments -->

- [ ] {{TOPIC_1_ACTION_1}} (Owner: {{OWNER_1}})
- [ ] {{TOPIC_1_ACTION_2}} (Owner: {{OWNER_2}})

### Suggestions for Information Extraction

<!-- Identify what information should be extracted and which agent should handle it -->

- **Stakeholder Information (Stakeholder Manager Agent)**
  - {{TOPIC_1_STAKEHOLDER_INFO}}
- **Knowledge Entries (Knowledge Manager Agent)**
  - {{TOPIC_1_KNOWLEDGE_INFO}}
- **Other Agent Information**
  - {{TOPIC_1_OTHER_INFO}}

## {{TOPIC_2_TITLE}}

### Takeaways

<!-- Short, crisp bullet points capturing the essence of this topic -->

- {{TOPIC_2_SUMMARY_POINT_1}}
- {{TOPIC_2_SUMMARY_POINT_2}}

### Details

<!-- Key contributions and details from participants, maintaining chronological order within this topic -->

- **{{PARTICIPANT_1}}**: {{TOPIC_2_DETAIL_1}}
- **{{PARTICIPANT_2}}**: {{TOPIC_2_DETAIL_2}}

### Action Points

<!-- Clear, actionable items with owner assignments -->

- [ ] {{TOPIC_2_ACTION_1}} (Owner: {{OWNER_1}})
- [ ] {{TOPIC_2_ACTION_2}} (Owner: {{OWNER_2}})

### Suggestions for Information Extraction

<!-- Identify what information should be extracted and which agent should handle it -->

- **Stakeholder Information (Stakeholder Manager Agent)**
  - {{TOPIC_2_STAKEHOLDER_INFO}}
- **Knowledge Entries (Knowledge Manager Agent)**
  - {{TOPIC_2_KNOWLEDGE_INFO}}
- **Other Agent Information**
  - {{TOPIC_2_OTHER_INFO}}

## {{TOPIC_3_TITLE}}

### Takeaways

<!-- Short, crisp bullet points capturing the essence of this topic -->

- {{TOPIC_3_SUMMARY_POINT_1}}
- {{TOPIC_3_SUMMARY_POINT_2}}

### Details

<!-- Key contributions and details from participants, maintaining chronological order within this topic -->

- **{{PARTICIPANT_1}}**: {{TOPIC_3_DETAIL_1}}
- **{{PARTICIPANT_2}}**: {{TOPIC_3_DETAIL_2}}

### Action Points

<!-- Clear, actionable items with owner assignments -->

- [ ] {{TOPIC_3_ACTION_1}} (Owner: {{OWNER_1}})
- [ ] {{TOPIC_3_ACTION_2}} (Owner: {{OWNER_2}})

### Suggestions for Information Extraction

<!-- Identify what information should be extracted and which agent should handle it -->

- **Stakeholder Information (Stakeholder Manager Agent)**
  - {{TOPIC_3_STAKEHOLDER_INFO}}
- **Knowledge Entries (Knowledge Manager Agent)**
  - {{TOPIC_3_KNOWLEDGE_INFO}}
- **Other Agent Information**
  - {{TOPIC_3_OTHER_INFO}}

---

## Instructions for Use

1. **Be synthetic and structured**: Keep summaries short and organized by main topics
2. **Chronological topic order**: Topics should be ordered as they were discussed (Topic 1 = first discussed, etc.)
3. **Short better than long**: Focus on essence, not exhaustive details
4. **Main Topics**: Organize content by 3-5 main topics discussed in the meeting
5. **For each topic include**:
   - **Summary**: Short, crisp bullet points (2-4 points maximum)
   - **Details**: Key participant contributions with attribution (format: "**Name**: detail")
   - **Action Points**: Clear, actionable items with owner assignments (use checkboxes)
   - **Suggestions for Information Extraction**: Identify what should be extracted by which agent (Stakeholder Manager Agent, Knowledge Manager Agent, Meeting Assistant Agent, or any other relevant agent)
6. **Action Point format**: "- [ ] Action description (Owner: Name)" - include owner when known
7. **Information Extraction**: Be specific about what information is relevant for each agent type
8. **Add/remove topics**: Use as many topic sections as needed (not limited to 3)
9. **File naming**: Save as `YYYYMMDD-HHMMSS MeetingName-summary.md` (replace `-transcript` with `-summary`)
10. **Location**: Save to `.claude/meetings/summaries/`
11. **Links**: Use repository-root-relative paths (e.g., `.claude/meetings/transcripts/...`) for clickability
