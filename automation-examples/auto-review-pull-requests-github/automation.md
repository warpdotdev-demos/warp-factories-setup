---
triggers:
  - provider: github
    event: pull_request_ready
---
Review the pull request or merge request that triggered this automation. Inspect the changed code and relevant surrounding code for correctness, security, maintainability, and missing focused tests. Follow the repository instructions and report only findings that you can validate from the code. Submit a formal review with inline comments for actionable findings and a concise top-level verdict. Approve only when repository policy explicitly permits automated approval and you find no blocking issue; otherwise comment or request changes as appropriate. Do not modify the change-request branch.
