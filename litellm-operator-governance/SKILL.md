---
name: litellm-operator-governance
description: Route LiteLLM administration requests to first-party skills, assess capability coverage and compatibility, and safely escalate unsupported actions. Use for LiteLLM administration routing, coverage assessment, version review, unsupported actions, and safe escalation.
license: MIT
compatibility: Requires access to the applicable first-party LiteLLM skills and official documentation.
metadata:
  author: Turbo Crowd
  version: "1.0.0"
---

# LiteLLM Operator Governance

Use this governance skill to assess a LiteLLM administration request before selecting an execution path. It complements the first-party skills in this repository and never replaces them.

## Routing Rules

1. Identify the requested LiteLLM surface and review the applicable first-party skill first.
2. Review official LiteLLM documentation when version or compatibility affects the request.
3. Do not issue arbitrary HTTP or `curl` commands from this skill.
4. Do not accept, request, store, or expose secrets. Use placeholders only, such as `<LITELLM_BASE_URL>` and `<LITELLM_ADMIN_KEY>`.
5. Do not implement, duplicate, or infer CRUD procedures that are absent from a first-party skill.

## Capability Routes

Classify every request using exactly one of these routes:

- `first-party skill available`
- `official API documented but no first-party skill`
- `UI/manual only`
- `config/deployment owned`
- `Enterprise/license verification required`
- `unknown - stop and escalate`

Treat model deployments owned by configuration or deployment systems as `config/deployment owned`; do not assume they are automatically mutable through LiteLLM administration.

The MCP Gateway governs downstream MCP tools. It is not a LiteLLM management API.

## Required Capability Assessment

Return a structured assessment before proposing an execution path:

```text
Request: <requested outcome>
Surface: <LiteLLM surface>
Compatibility reviewed: <version or documentation evidence>
Capability route: <one exact route from Capability Routes>
First-party skill: <path or none>
Constraints: <non-secret constraints>
Escalation: <required owner or none>
```

For any route other than `first-party skill available`, do not invent a command. Explain the supported escalation path and stop when ownership, entitlement, or documentation is unclear.
