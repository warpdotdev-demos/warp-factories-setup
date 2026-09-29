---
triggers:
  - provider: linear
    event: issue_created
---
Read the new Linear issue and search across visible teams for the same underlying problem or requested outcome. Keep the search lightweight: use one primary query and at most one fallback query, inspect at most 20 candidates total, and exclude the triggering issue and archived issues. Inspect candidate descriptions rather than matching on broad keywords. Read this factory’s UID from WARP_FACTORY_ID; if absent, stop without commenting. Use a receipt of the form factory-duplicate-check:<this factory UID>:<new issue ID> in your own comment on the new issue. Read all its comments before investigating and again immediately before posting; if the exact receipt is already present, stop without commenting. If credible matches exist, post one comment with at most five matches, links, a short rationale for human review, and that receipt. If comments cannot be read, do not post. Do not change issue state, close issues, create duplicate relationships, or modify titles, owners, or labels. If no credible match exists, leave the issue unchanged.
