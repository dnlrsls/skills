# Compatibility Policy

This repository adopts the [Agent Skills specification](https://agentskills.io/specification) as the normative format for its canonical skills. The policy keeps skill definitions portable; it does not promise support from any specific client.

## Scope

This policy governs canonical skills in this repository. It distinguishes their portable definition from client-specific discovery, installation, metadata, and invocation behavior.

## Canonical format

Each canonical skill **MUST** be a directory at `skills/<skill-name>/` with its entry point at:

```text
skills/<skill-name>/SKILL.md
```

`SKILL.md` **MUST** follow the Agent Skills format: YAML frontmatter followed by Markdown instructions. Its required `name` and `description` fields **MUST** meet the specification's constraints, including matching the parent directory name.

## Portable core

Canonical skills:

- **MUST** describe capabilities and required outcomes rather than proprietary tool names or client commands.
- **MUST** use paths relative to the skill root for local files.
- **MUST** declare any external or environment requirements, including required executables, network access, credentials, or OS assumptions. Use the standard `compatibility` field when its concise form is sufficient; otherwise document the detail in a local reference.
- **MUST NOT** use the experimental `allowed-tools` field in the portable core.
- **SHOULD** keep instructions agent-, model-, and OS-agnostic when the task allows it.
- **SHOULD** keep the main instructions focused and place optional detail in local references, assets, or scripts.
- **MAY** include scripts, references, and assets permitted by the specification, provided their requirements are declared.

## Integrations and distribution

The portable definition is the canonical `skills/<skill-name>/` directory and its behavior. Platform-specific discovery locations, installation steps, manifests, metadata, tool mappings, or invocation conventions are integrations or distribution concerns.

An integration **MUST** remain a thin adapter outside the portable core when one is needed. It **MUST NOT** redefine the canonical skill behavior. Distribution **MAY** package, copy, link, or register a canonical skill for a client, but distribution mechanics do not change the skill definition.

## Compatibility claims

Use only these claim levels:

| Level | Meaning | Evidence required |
| --- | --- | --- |
| Specification-conformant | A named canonical skill passes the Agent Skills format validator. | Recorded `skills-ref validate` result for that skill. |
| Client-verified | A specification-conformant skill has been tested in a named client and version using a documented integration path. | Date, client and version, skill, test scope, and result. |

Specification conformance is not a claim of client support. A client-verification claim **MUST NOT** be made until the test has occurred and its evidence is recorded. This repository currently makes no client-verified compatibility claims.

## Validation and verification

When validation tooling is added, canonical skills **MUST** be validated with the [Agent Skills `skills-ref` reference library](https://github.com/agentskills/agentskills/tree/main/skills-ref):

```text
skills-ref validate skills/<skill-name>
```

Record client checks using this matrix. Do not replace `Not yet verified` with a compatibility claim without the required evidence.

| Client | Version | Skill | Integration path | Status | Evidence |
| --- | --- | --- | --- | --- | --- |
| — | — | — | — | Not yet verified | — |

## Primary references

- [Agent Skills specification](https://agentskills.io/specification)
- [Agent Skills documentation](https://agentskills.io/)
- [Agent Skills reference implementation and validator](https://github.com/agentskills/agentskills)
