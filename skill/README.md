# PromptFGAD Agent-Executable Skill

The PromptFGAD skill packages the paper-described pipeline as a reusable
agent-executable workflow. It allows an AI agent or automation system to invoke
PromptFGAD stages while preserving the method's validation and evidence
boundaries.

> **Release statement:** The complete `SKILL.md`, workflow runner, reference
> contracts, example configurations, and validation tests will be released in
> this repository after the paper is formally accepted. This page documents the
> intended behavior of the forthcoming skill.

## Intended Uses

Use the PromptFGAD skill to:

- construct or inspect a host-flow fusion graph;
- reproduce the PromptFGAD workflow;
- validate completed telemetry before graph construction;
- detect suspicious graph entities;
- retrieve bounded, ranked evidence;
- generate evidence-grounded security explanations.

## Required Principles

The released skill will enforce the following rules:

1. Treat observed telemetry as immutable evidence.
2. Never inject an LLM-generated candidate unless it passes deterministic
   validation.
3. Never allow the LLM to create alignment edges, labels, GNN scores, or
   evidence ranks.
4. Report evidence localization as bounded top-k retrieval, not complete
   attack-chain recovery.
5. Record every requested stage and configuration in `run_manifest.json`.

## Skill Workflow

```text
Inspect configuration and inputs
        |
Normalize telemetry into the Common Data Schema
        |
Optionally request schema-constrained completion
        |
Validate candidates and graph integrity
        |
Construct the host-flow fusion graph
        |
Run graph-based detection
        |
Localize and rank evidence
        |
Map security semantics and explain retrieved evidence
        |
Save artifacts, provenance, and limitations
```

## Planned Skill Structure

```text
skill/
├── README.md
├── SKILL.md
├── references/
│   ├── common-data-schema.md
│   ├── validation-policy.md
│   └── output-contract.md
└── examples/
    ├── creme-workflow.yaml
    └── synthetic-workflow.yaml
```

## Portability

The skill is designed as a general `SKILL.md + CLI` workflow rather than a
single-platform integration. Agents may use the instructions and structured
contracts, while deterministic scripts remain responsible for validation,
fusion, detection, and evidence ranking.

