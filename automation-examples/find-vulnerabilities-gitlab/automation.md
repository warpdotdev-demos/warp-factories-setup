---
triggers:
  - provider: gitlab
    event: merge_request
    filter:
      actions: [open]
---
Review the pull request or merge request that triggered this automation for exploitable security vulnerabilities. Inspect the changed code and the relevant surrounding code. Report only findings that you can validate from the repository. For each finding, submit an actionable review comment that explains the impact, the evidence, and a concrete remediation. Do not report speculative findings and do not modify the change-request branch. If you find no validated vulnerability, leave the change request unchanged.
