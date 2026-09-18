# Repository Governance

This is a public repository. Do not commit secrets, credentials, tokens, key hashes, environment-specific URLs, identifiers, raw API or gateway output, logs, traces, backups, or environment files. Use neutral placeholders such as `<LITELLM_BASE_URL>`, `<LITELLM_ADMIN_KEY>`, and `<GITHUB_OWNER>`.

## Role Separation

- GitHub is the versioned source of truth for this repository.
- LiteLLM Skills Gateway is the future registry and discovery layer.
- OpenCode is a future consumer of distributed skills.

First-party LiteLLM skills are copied and pinned from upstream. They are not locally rewritten. The sole local `litellm-operator-governance` skill provides routing and safe escalation only: it is non-CRUD and does not replace upstream skills.

## Agent Push Consent

`main` is the published channel read by LiteLLM Skills Gateway.

Agents may prepare changes and report the proposed diff. An agent may push only after explicit human consent in the active conversation for that proposed change. Silence, a previous general authorization, or an inferred preference is not consent for a future push.

Before an agent push, inspect repository status, the proposed diff, and recent commits; scan added or changed content for public-data and secret risks; and stage only the intended files.

After an agent push, read back the commit and report the repository URL, commit SHA, changed files, and scan result.

Humans may push directly. Formal branch protection and pull-request review may be added later.

## Updates And Rollback

Update the upstream pin by reading release notes, selecting an immutable commit SHA, reviewing the diff, testing, and then publishing through approved distribution workflows. Roll back by reverting to a prior Git commit.

Agents do not require direct LiteLLM CLI access to use this repository. This repository does not claim that every LiteLLM surface is fully covered.

## Excluded Future Phases

The following are excluded from this commit:

- Skills Gateway registration
- OpenCode distribution
- `litellm-operator` implementation
- MCP onboarding
- LiteLLM CLI removal
