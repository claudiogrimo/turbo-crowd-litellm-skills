# Repository Governance

This is a public repository. Do not commit secrets, credentials, tokens, key hashes, environment-specific URLs, identifiers, raw API or gateway output, logs, traces, backups, or environment files. Use neutral placeholders such as `<LITELLM_BASE_URL>`, `<LITELLM_ADMIN_KEY>`, and `<GITHUB_OWNER>`.

## Role Separation

- GitHub is the versioned source of truth for this repository.
- LiteLLM Skills Gateway is the future registry and discovery layer.
- OpenCode is a future consumer of distributed skills.

First-party LiteLLM skills are copied and pinned from upstream. They are not locally rewritten. The sole local `litellm-operator-governance` skill provides routing and safe escalation only: it is non-CRUD and does not replace upstream skills.

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
