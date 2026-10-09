---
name: github
description: Preserves runtime identity, PR attribution, artifact reporting, and human-review handoff. Use before branch, commit, PR, CI, or requested PR-feedback operations.
---
# GitHub

## Identity and tools
- Prefer an available connected MCP operation with the necessary capability.
  Otherwise use noninteractive `GH_PAGER=cat gh` with explicit repository
  scope, and `git --no-pager`. Do not pass `--no-pager` to `gh`.
- Use provisioned git identity and GitHub credentials as-is. Never override
  `user.name`, `user.email`, author/committer fields, or authentication to make
  commits appear to come from a factory/agent display name.
- Use the repository's actual base branch, capture it once, and reuse it for
  checkout and PR `--base`. Use `factory/<issue-key>-<slug>` branches; revisions
  retain the same branch/PR. Never merge, approve, or force-push shared work.
- End each commit and PR description with
  `Co-Authored-By: Warp <agent@warp.dev>`.

## Create or adopt a PR
Use the repository's PR template and a compact behavioral summary, owning
issue URL, and verification results/gaps. Write multiline bodies to a temporary
file for CLI operations. Never commit that file or verification artifacts.
Create draft first; verify head, base, and a nonempty diff after creation.
An incorrect PR is not successful delivery: report/correct it.

Call `report_pr` as soon as the PR is created **or adopted**, with HTTPS URL and
head branch. Register it again in a new run that adopts it. Apply this factory's
label, currently `factory:example-tickets`, derived from its own `factory.yaml`
alias; keep the label aligned when changing the alias. Label failure does not
block hand-off but must be reported. Labels identify artifacts, not progress;
this factory has no GitHub lifecycle automation.

Assign a reviewer only from a supplied/resolved GitHub login. Never infer a
login from a name or email. Ask the requester for missing routing information.

## Managed attribution and evidence
- Obtain the PR-description artifact blocks through
  `get_artifacts_for_pull_request_description`; retain nonempty managed blocks
  verbatim when creating or refreshing the body. Preserve repository template
  sections; keep the prose proportional to the change.
- Ensure the managed attribution comment with both
  `<!-- warp:pr-artifacts-comment start -->` and
  `<!-- warp:pr-artifacts-comment end -->` exists. Check before posting:
  an existing marked comment is not duplicated or rebuilt.
- On creation, post the supplied managed comment promptly; on adoption, check
  before the first other PR write. Use the owning task/thread/run links from
  runtime or handback context, never an unrelated event session. Preserve the block; do not
  invent markup or URLs. If no block/tool is available, report the missing
  attribution rather than fabricate it. This does not block implementation.
- Managed attribution comments get no extra footer. Other necessary GitHub
  comments/replies identify the factory with `Responding as <factory name>`
  and the resolved session/factory links. Resolve the name from the factory's
  own `factory.yaml`, using the runtime skill catalog / `WARP_SKILL_DIRS`;
  omit unavailable links, but never post an unidentified factory comment.
- Put verification media in the PR, not Git. Use `get_media_artifact_links` for
  sharing this run's captures with the human, and native uploads when supported.

## Verification and requested follow-ups
Promote only when required local checks pass. CI is a point-in-time read:
report pending/failed checks and hand off promptly, without sleep-and-poll loops.
The implementer records the durable PR link and communicates the human hand-off.

Skipping autonomous review does not discard human feedback. On a requested
correction, read relevant conversation comments, top-level reviews, and
inline comments with pagination. Revise the existing PR and rerun affected
checks. Reply to an addressed thread with its fixing commit, then resolve only
that thread. Unaddressed findings stay open with an explanation; do not post
an additional recap or create a review agent. Use available tools, not helper
scripts assumed to exist in another factory.
