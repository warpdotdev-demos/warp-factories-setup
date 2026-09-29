---
triggers:
  - provider: jira
    event: issue_created
---
Inspect the new Jira issue that triggered this automation, including its description, comments, attachments, and metadata, then inspect the relevant repository code. Proceed only when the requested behavior is clear and the issue can be validated or reproduced from the available evidence. Implement the smallest safe fix, add focused regression coverage when it proves novel or edge-case behavior, run the relevant checks, and open a draft pull request or merge request linked to the Jira issue. Do not move the issue to a completed state. If the report is ambiguous, not reproducible, already fixed, or does not require a code change, leave the repository and issue unchanged rather than guessing.
