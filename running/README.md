# Running PromptFGAD

The released PromptFGAD workflow will expose one command-line entry point for
executing or inspecting the end-to-end pipeline.

> **Release statement:** The executable workflow runner, environment files, and
> example artifacts will be released after the paper is formally accepted.
> Commands shown here document the planned public interface.

## Planned Quick Start

```bash
python workflow/run_promptfgad.py \
  --config workflow/configs/synthetic.yaml \
  --stages all \
  --output-dir runs/synthetic-demo
```

## Supported Stages

```text
extract
complete
validate
fuse
detect
localize
explain
all
```

Individual stages may be selected when resuming or diagnosing a prior run:

```bash
python workflow/run_promptfgad.py \
  --config workflow/configs/synthetic.yaml \
  --stages validate,fuse,detect \
  --output-dir runs/synthetic-validation
```

A dry run will inspect configured commands without executing them:

```bash
python workflow/run_promptfgad.py \
  --config workflow/configs/creme.yaml \
  --stages all \
  --output-dir runs/creme-dry-run \
  --dry-run
```

## Planned Outputs

```text
runs/<run-name>/
├── run_manifest.json
├── validated_graph/
│   ├── nodes.csv
│   └── edges.csv
├── detection_results.json
├── ranked_evidence.json
├── attack_chain.json
├── explanation.md
└── logs/
```

## Completion Conditions

A run is complete only when:

- deterministic graph validation has completed;
- rejected completion candidates do not appear in the graph;
- detection and evidence artifacts reference the validated graph;
- every requested stage is represented in the run manifest;
- reported conclusions are supported by generated artifacts.

Evidence outputs represent bounded investigation evidence and should not be
interpreted as guaranteed recovery of the complete attack lifecycle.

