# PromptFGAD Pipeline

PromptFGAD combines heterogeneous telemetry, graph-based detection, bounded
evidence localization, and evidence-grounded explanation in one auditable
workflow.

> **Release statement:** This page documents the paper-level pipeline. The
> complete implementation and reproducibility artifacts will be published after
> the paper is formally accepted.

## Stage I: Host-Flow Fusion Graph Construction

Raw network flows and host logs are normalized into structured node and edge
tables under a Common Data Schema. Host-side entities include processes, files,
users, and network endpoints. Traffic-side entities represent communication
endpoints and flow relations.

When observations are incomplete, an optional LLM completion stage proposes
missing fields or records under a fixed schema. Every candidate must pass
deterministic checks before graph construction.

Cross-layer fusion uses:

- IP-based alignment between host network entities and traffic endpoints.
- Time-window alignment between host events and related flow intervals.
- Explicit `aligned_with` and `aligned_with_flow` relations.

## Stage II: Fusion Graph Detection

PromptFGAD applies a GNN-based node detector to the validated fusion graph. The
detector produces:

- predicted node classes;
- anomaly scores;
- suspicious node candidates for downstream evidence localization.

The reported PromptFGAD configuration uses GCN by default. Relation-aware and
other graph backbones can be evaluated under the same graph and data protocol.

## Stage III: Evidence Localization and Explanation

PromptFGAD extracts suspicious graph context, scores candidate edges, and
retrieves a bounded top-k evidence set. Retrieved evidence is ordered using
graph structure and timestamps, then mapped to MITRE ATT&CK semantics.

The final explanation summarizes already-localized evidence for analyst triage.
The explanation module does not replace detection and cannot alter graph edges,
anomaly scores, or evidence ranks.

## Deterministic and LLM-Assisted Boundaries

Deterministic components include:

- schema, type, range, timestamp, and semantic validation;
- graph fusion and alignment-edge construction;
- GNN detection and anomaly scoring;
- evidence ranking and top-k retrieval;
- known MITRE ATT&CK mappings.

LLM-assisted components are limited to:

- proposing missing records or fields under schema constraints;
- bounded fallback mapping for ambiguous security semantics;
- post-hoc, evidence-grounded explanation.

Observed telemetry is treated as immutable evidence. Unvalidated LLM candidates
are rejected and never injected into the fusion graph.

