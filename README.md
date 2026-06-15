# PromptFGAD

PromptFGAD is a host-flow fusion graph framework for attack detection and
evidence-grounded explanation with large language models (LLMs). It connects
network communication evidence with host-level provenance evidence, performs
graph-based anomaly detection, and organizes localized evidence into
investigation-oriented attack-chain summaries.

This repository currently serves as the public project page and documentation
preview for the accompanying research paper.

> **Release statement:** The complete PromptFGAD implementation, experiment
> configurations, data-processing scripts, reproducibility artifacts, and
> agent-executable PromptFGAD skill will be released in this repository after
> the paper is formally accepted. Until then, this repository documents the
> framework design, public interfaces, execution workflow, and planned artifact
> structure.

## Main Contributions

1. **Host-flow fusion graph modeling.** PromptFGAD associates network flow
   events with host provenance entities through explicit cross-layer alignment,
   connecting host-internal causal activity with cross-host communication.
2. **Detection and evidence localization.** A graph neural network detector
   identifies suspicious entities and ranks a bounded set of high-confidence
   evidence edges for analyst investigation.
3. **Constrained LLM assistance.** LLMs are used only for schema-constrained
   completion and evidence-grounded explanation. Deterministic validation
   prevents unvalidated candidates from entering the fusion graph.
4. **Agent-executable workflow.** The end-to-end pipeline is packaged as a
   reusable skill with versioned configurations, validation policies, structured
   output contracts, and auditable run manifests.

## Pipeline

```text
Host logs and network flows
        |
        v
Telemetry normalization and structured triple extraction
        |
        v
Optional schema-constrained LLM completion
        |
        v
Deterministic validation and host-flow graph fusion
        |
        v
GNN-based attack detection
        |
        v
Bounded evidence localization and MITRE ATT&CK mapping
        |
        v
Evidence-grounded explanation
```

PromptFGAD reports investigation-oriented evidence localization rather than
claiming complete recovery of every attack edge under incomplete telemetry.

## Documentation

- [Pipeline](pipeline/README.md): method stages and deterministic/LLM boundaries.
- [Configuration](configuration/README.md): planned workflow configuration and
  reproducibility fields.
- [Running PromptFGAD](running/README.md): planned command-line interface,
  stages, and output artifacts.
- [PromptFGAD Skill](skill/README.md): agent-executable skill design and safety
  principles.

## Planned Repository Structure

```text
PromptFGAD/
├── README.md
├── pipeline/
├── configuration/
├── running/
├── skill/
├── workflow/                 # Released after paper acceptance
├── data_processing/          # Released after paper acceptance
├── detection/                # Released after paper acceptance
└── knowledge_mapping/        # Released after paper acceptance
```

## Availability

The documentation preview is available at:

<https://github.com/foresthao/PromptFGAD>

The complete reproducibility release will identify the frozen release tag,
commit identifier, required external datasets, and optional LLM endpoint
requirements after formal paper acceptance.

