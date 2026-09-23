# AI-SOLUTIONS-PS

A shared repository of MRI product reference material and AI agent documentation.
It brings together table schemas, business rules, and agent-specific instructions
so multiple AI solutions can use consistent product definitions without duplicating
them.

This root README is the repository overview. It is **not an agent orchestrator**:
each agent has its own instructions and entry point in its dedicated folder.

## Repository structure

```text
AI-SOLUTIONS-PS\
|-- README.md
|-- COMMON\
|   |-- Angus\
|   |   |-- Schema\
|   |   `-- Rules\
|   |-- EVO\
|   |   |-- Schema\
|   |   `-- Rules\
|   |-- PLE\
|   |   |-- Schema\
|   |   `-- Rules\
|   `-- PMX\
|       |-- Schema\
|       `-- Rules\
|-- DATA MANAGER\
|   |-- README.md
|   `-- AGENT_SETUP.md
`-- TDD Spec Generation Agent\
    `-- .gitkeep
```

## COMMON: shared MRI product reference material

[`COMMON`](COMMON/) holds reusable definitions for tables in different MRI
products. It currently covers **Angus, EVO, PLE, and PMX**. Each product has two
complementary sets of files:

| Location | Purpose |
| --- | --- |
| `COMMON/{Product}/Schema/{Table}.json` | Structural table definitions, including fields, data types, lengths, precision, nullability, keys, and relationships where documented. |
| `COMMON/{Product}/Rules/{Table}.md` | Business and intake requirements, including mandatory fields, allowed values, formats, validation rules, and reference-data requirements. |

Schemas describe the table structure; rules explain how data should be populated
and validated. Agents performing validation must consult both, rather than treating
either file as a complete substitute for the other.

Product context matters: an Angus `Tenant` table is not the same definition as a
PLE `Tenant` table. Keep references product-specific and use only the information
actually documented. These files are reference definitions, not live database
access or client data.

## Agent folders: instructions, skills, and workflows

Each agent has a dedicated top-level folder for its own orchestration, setup
guidance, and any supporting skill or Markdown files. Agent-specific behaviour
belongs there; reusable product definitions belong in `COMMON`.

| Agent | Folder and documentation | Current purpose or status |
| --- | --- | --- |
| Data Manager | [`DATA MANAGER`](DATA%20MANAGER/), [orchestrator](DATA%20MANAGER/README.md), [setup guide](DATA%20MANAGER/AGENT_SETUP.md) | Validates MRI integration files, applies supported corrections, and produces cleaned data, a change log, and a validation report. |
| TDD Spec Generation Agent | [`TDD Spec Generation Agent`](TDD%20Spec%20Generation%20Agent/) | Reserved for the agent's future instructions and supporting files. Currently contains only `.gitkeep`; no workflow is implemented here yet. |

**Data Manager starts from `DATA MANAGER/README.md`, not this root README.**
Its setup guide contains the instructions to paste into Microsoft Copilot Studio.
One agent's orchestration must not be treated as another agent's instructions.

## Extending the repository

- Add shared table definitions and associated rules under the appropriate product
  in `COMMON`. Preserve canonical product and table names and update affected
  agents' registries or references.
- Give each new agent its own top-level folder with a README explaining its
  purpose, entry point, required shared references, and current capabilities.
- Keep setup instructions, skill files, and workflow-specific Markdown within the
  owning agent's folder. Reference `COMMON` rather than copying schemas or rules.
- Add new agents to the directory above and keep links and startup paths current
  when files move.
- Keep client uploads, generated deliverables, credentials, and secrets out of
  this reference repository.

GitHub connector paths are relative to the repository root. Use literal spaces
in tool paths such as `DATA MANAGER/README.md`; the encoded spaces in this
document's clickable links are for Markdown navigation only.
