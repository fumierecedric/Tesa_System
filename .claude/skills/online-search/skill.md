---
name: online-search
description: Provides web search capability for finding current information, documentation, and resources from external sources when local knowledge is insufficient
allowed-tools: [WebSearch, WebFetch]
---

# Online Search Skill

You are assisting with online search operations. This skill enables agents and users to search the web for information when local knowledge is insufficient or when current, external information is needed.

## Core Principle

**EXTERNAL INFORMATION ONLY**: This skill handles web queries exclusively. For local knowledge, use the knowledge-management skill instead. Maintain clear separation between online search results and local knowledge entries.

## When to Use This Skill

Use online-search when:
- Information is not available in the local knowledge base
- Current/recent information is needed (news, updates, latest documentation)
- External documentation or resources are required
- Researching new topics not yet documented locally
- Verifying or supplementing existing knowledge

Do NOT use online-search when:
- Information already exists in local knowledge base (search there first)
- Creating or updating knowledge entries (use knowledge-management skill)
- Information is available in project files or meeting transcripts

## Available Methods

---

### 1. Perform Web Search

Search the web for information using a query string.

**Purpose**: Find external information, documentation, and resources that aren't in the local knowledge base.

**When to use**:
- User explicitly requests web search
- Knowledge base search returns no results
- Current information is needed (news, updates, latest docs)
- Researching new methodologies, tools, or technologies

**Steps**:

1. **Parse search query**
   - Understand what information is requested
   - Formulate effective search query
   - Identify key terms and concepts
   - Consider search refinements (date, domain, etc.)

2. **Execute web search**
   - Use WebSearch tool with formulated query
   - Apply domain filters if specific sources needed
   - Handle search errors gracefully

3. **Process search results**
   - Review returned results for relevance
   - Extract key information from result snippets
   - Note source URLs and metadata
   - Filter out irrelevant or low-quality results

4. **Format and return results**
   - Present results in structured format
   - Include:
     - Brief description of each result
     - Source URL
     - Relevance to query
     - Date/recency if available
   - Limit to most relevant results (typically 5-10)
   - Clearly indicate these are external sources

5. **Suggest next steps**
   - Offer to fetch full content from specific URLs if needed
   - Suggest creating knowledge entry if information should be preserved
   - Recommend refining search if results are insufficient

**Inputs**:
- Search query string
- Optional: Domain filters (include/exclude specific domains)
- Optional: Date filters or recency requirements

**Outputs**:
- Structured list of search results with:
  - Title/description
  - Source URL
  - Relevance snippet
  - Metadata (date, source type)
- Clear indication that results are from external sources
- Suggestions for next steps

**Example**:
```markdown
User: "Search for SOSTAC framework documentation"
Steps:
1. Parse query: "SOSTAC framework documentation"
2. Execute: WebSearch with query "SOSTAC framework documentation"
3. Process results:
   - Result 1: "SOSTAC Marketing Planning Framework - SmartInsights"
   - Result 2: "SOSTAC Guide: The Ultimate Framework for Digital Marketing"
   - Result 3: "What is SOSTAC? Complete Guide to Strategic Planning"
4. Format results:
   **Search Results for "SOSTAC framework documentation"**

   1. **SOSTAC Marketing Planning Framework** - SmartInsights
      URL: https://www.smartinsights.com/sostac/
      Comprehensive guide to SOSTAC covering all six phases of the framework

   2. **SOSTAC Guide: The Ultimate Framework for Digital Marketing**
      URL: https://example.com/sostac-guide
      Detailed breakdown with examples and case studies

   3. **What is SOSTAC? Complete Guide**
      URL: https://example.com/what-is-sostac
      Introduction to SOSTAC methodology with templates

5. Suggest: "Would you like me to fetch the full content from any of these sources? Or create a knowledge entry with this information?"
```

---

### 2. Fetch Web Content

Retrieve and analyze full content from a specific URL.

**Purpose**: Get detailed information from a specific web page for deeper analysis or knowledge entry creation.

**When to use**:
- After web search to get full content from promising results
- User provides specific URL to analyze
- Creating knowledge entry from external documentation
- Need complete information beyond search snippets

**Steps**:

1. **Validate URL**
   - Ensure URL is properly formatted
   - Verify it's a reasonable source to fetch
   - Check for redirects or domain changes

2. **Fetch content using WebFetch**
   - Use WebFetch tool with URL and analysis prompt
   - Specify what information to extract
   - Handle redirects appropriately

3. **Process fetched content**
   - Extract relevant information based on query
   - Summarize key points
   - Note document structure and sections
   - Identify important details

4. **Return structured information**
   - Provide summary of content
   - Include URL and source metadata
   - Highlight key findings
   - Preserve context and structure
   - Clearly mark as external source

5. **Suggest knowledge entry creation**
   - If information is valuable for future use
   - Offer to create knowledge entry with fetched content
   - Include URL as source

**Inputs**:
- URL to fetch
- Analysis prompt (what to extract/analyze)
- Optional: Specific sections or topics to focus on

**Outputs**:
- Structured summary of content
- Key information extracted
- Source URL and metadata
- Suggestion to create knowledge entry if valuable

**Example**:
```markdown
User: "Fetch the SOSTAC framework guide from smartinsights.com"
Steps:
1. Validate URL: https://www.smartinsights.com/sostac/
2. Fetch: WebFetch with prompt "Extract the main components and phases of SOSTAC framework"
3. Process content:
   - SOSTAC phases: Situation, Objectives, Strategy, Tactics, Actions, Control
   - Each phase explained with examples
   - Implementation guidelines
   - Best practices
4. Return:
   **Content from SmartInsights - SOSTAC Framework**

   The SOSTAC framework consists of 6 phases:
   1. **Situation**: Analyze current position (SWOT, market research)
   2. **Objectives**: Define clear, measurable goals
   3. **Strategy**: Determine how to achieve objectives
   4. **Tactics**: Detail specific tools and channels
   5. **Actions**: Create implementation plan
   6. **Control**: Monitor, measure, and optimize

   Source: https://www.smartinsights.com/sostac/

5. Suggest: "This is comprehensive information. Would you like me to create a knowledge entry for the SOSTAC framework using this as a source?"
```

---

### 3. Domain-Specific Search

Search within specific domains or exclude certain domains.

**Purpose**: Focus search on authoritative sources or exclude low-quality sources.

**When to use**:
- Need information from specific authoritative sources
- Want to exclude certain domains (forums, low-quality sites)
- Searching for official documentation or academic sources
- User specifies desired source types

**Steps**:

1. **Identify domain requirements**
   - Determine which domains to include/exclude
   - Understand why domain filtering is needed
   - Note any user preferences for sources

2. **Formulate search with domain filters**
   - Use WebSearch tool with:
     - `allowed_domains`: List of domains to include
     - `blocked_domains`: List of domains to exclude
   - Combine with effective search query

3. **Execute and process results**
   - Same as standard web search
   - Note that results are domain-filtered
   - Handle cases where no results from specified domains

4. **Return filtered results**
   - Present results with domain context
   - Note which domains were included/excluded
   - Suggest removing filters if no results

**Inputs**:
- Search query
- Allowed domains list (optional)
- Blocked domains list (optional)

**Outputs**:
- Filtered search results
- Note about domain filtering applied
- Suggestion to broaden search if needed

**Example**:
```markdown
User: "Search for API best practices from official documentation sites only"
Steps:
1. Identify domains: Include official docs (github.com, developer.mozilla.org, etc.)
2. Formulate: WebSearch "API best practices" with allowed_domains filter
3. Execute: Get results only from specified domains
4. Return filtered results with domain context
5. Note: "Results filtered to official documentation sites. Would you like to broaden the search?"
```

---

## Integration with Other Agents and Skills

### Knowledge Management Skill Integration
**Separation of Concerns:**
- **online-search**: Finds external information
- **knowledge-management**: Stores and retrieves local information

**Workflow Pattern:**
1. User asks question
2. Knowledge Manager searches local knowledge base
3. If not found, trigger online-search skill
4. Online-search returns external results
5. Optionally: Create knowledge entry to preserve valuable findings

**Example:**
```markdown
User: "What is the SOSTAC framework?"
Knowledge Manager:
1. Searches .claude/knowledge/ for SOSTAC
2. No results found
3. Triggers online-search skill

Online-search:
1. Searches web for "SOSTAC framework"
2. Returns results from external sources
3. Suggests: "Create knowledge entry?"

Knowledge Manager:
1. Reviews search results
2. Creates knowledge entry using external sources
3. Saves to .claude/knowledge/sostac-framework.md
```

### Meeting Assistant Integration
Meeting Assistant may trigger online-search to:
- Research topics mentioned in meetings
- Find documentation for decisions being discussed
- Gather external context for meeting preparation

### HR Agent Integration
HR Agent may trigger online-search to:
- Research companies or stakeholders
- Find contact information or organizational details
- Gather industry context

### Other Agents
Any agent can use online-search when:
- Local knowledge is insufficient
- External validation needed
- Current information required
- Research is needed for task completion

## Search Quality Guidelines

### Effective Query Formulation
- **Be specific**: Use precise terms and phrases
- **Use keywords**: Focus on key concepts
- **Add context**: Include relevant modifiers (e.g., "2025", "official", "guide")
- **Refine if needed**: Adjust query based on initial results

### Result Evaluation
- **Relevance**: Does result address the query?
- **Authority**: Is source credible and authoritative?
- **Recency**: Is information current (if needed)?
- **Quality**: Is content comprehensive and well-written?

### Result Presentation
- **Structure**: Organize results clearly
- **Context**: Provide enough information to evaluate usefulness
- **Links**: Always include source URLs
- **Metadata**: Include date, source type, relevance indicators

## Error Handling

### No Results Found
- Clearly state no results were found
- Suggest query refinements
- Offer to search with different terms
- Consider if information might be too specific/obscure

### API Failures
- Inform user of search failure
- Suggest trying again
- Offer alternative approaches (manual search, different query)

### Irrelevant Results
- Filter out obvious mismatches
- Suggest refining query
- Ask user for more context
- Consider domain filtering

## Important Notes

### Boundaries
**DO:**
- Search web for external information
- Fetch content from URLs
- Return structured search results
- Cite sources with URLs
- Suggest creating knowledge entries for valuable findings

**DO NOT:**
- Store search results in knowledge base (that's knowledge-management's job)
- Mix search results with local knowledge
- Search when information already exists locally
- Make assumptions about result quality without analysis

### Quality Standards
- Always include source URLs
- Clearly mark results as external sources
- Filter for relevance and quality
- Provide context for results
- Suggest next steps

### Integration Principles
- Clear separation from local knowledge management
- Collaborate with knowledge-management skill
- Support all agents when external information needed
- Maintain source attribution

## References

- Knowledge Management Skill: `.claude/skills/knowledge-management/skill.md`
- Knowledge Manager Agent: `.claude/agents/knowledge-manager.md`
- Meeting Management Skill: `.claude/skills/meeting-management/skill.md`
