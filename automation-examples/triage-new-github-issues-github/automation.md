---
triggers:
  - provider: github
    event: issue_created
---
Triage the new GitHub issue that triggered this automation. Read its description, comments, and metadata, search for duplicates, and inspect the relevant repository context when needed to validate the report. Classify its severity and affected area, apply only existing repository labels that clearly match, and identify the smallest appropriate owner set from repository ownership rules and recent contribution history. Leave one concise issue comment only when you found a duplicate or need specific missing information from the reporter. Do not modify code, open a pull request, close the issue, or invent labels or owners.
