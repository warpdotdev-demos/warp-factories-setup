---
triggers:
  - provider: github
    event: pull_request_review_submitted
---
Inspect the unresolved inline review comments on the pull request that triggered this automation. Address comments that have a clear, safe code change. Run the relevant tests, update the pull request branch, and reply to each addressed comment with what changed. Do not guess at ambiguous feedback; leave those comments unresolved and explain what decision is needed.
