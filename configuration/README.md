# PromptFGAD Configuration

PromptFGAD uses versioned workflow configurations to make inputs, model
settings, stage behavior, and output artifacts auditable.

> **Release statement:** Executable configuration files and frozen experiment
> snapshots will be released after the paper is formally accepted. The examples
> below describe the planned public interface.

## Configuration Categories

| Category | Purpose |
| --- | --- |
| `workflow_version` | Identifies the workflow contract |
| `project_root` | Resolves repository-relative paths |
| `random_seed` | Records the detector seed |
| `models` | Records completion, detection, and explanation models |
| `prompt_versions` | Identifies fixed prompt snapshots |
| `inputs` | Declares observed telemetry inputs |
| `stages` | Enables, skips, executes, or reuses pipeline stages |
| `artifacts` | Maps validated outputs into the run directory |
| `limitations` | Records scope and reproducibility limitations |

## Planned Example

```yaml
workflow_version: 1.0.0
random_seed: 42

models:
  completion: configured OpenAI-compatible endpoint
  detection: GCNAnomalyDetector
  explanation: configured OpenAI-compatible endpoint

stages:
  extract:
    enabled: true
  complete:
    enabled: false
    reason: Optional API stage
  validate:
    enabled: true
  fuse:
    enabled: true
  detect:
    enabled: true
  localize:
    enabled: true
  explain:
    enabled: true
```

## Reproducibility Records

Each execution will produce a `run_manifest.json` recording:

- workflow and prompt versions;
- model settings and random seed;
- input paths, sizes, and cryptographic hashes;
- deterministic validation results;
- executed, reused, skipped, or failed stages;
- generated artifact paths and hashes;
- known limitations.

## External Requirements

Some workflows require external resources:

- CREME telemetry must be obtained according to its original distribution
  terms.
- LLM completion and explanation require a separately configured compatible
  endpoint.
- API keys must be supplied through environment variables or a local,
  untracked configuration file.

No real API keys will be included in the public repository.

