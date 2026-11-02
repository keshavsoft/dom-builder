# json-instruction-contract

Defines the JSON shape shared by instruction producers, validators, and executors. It describes destinationPath, sourcePath, func, optional templateKey, and narration. It does not execute instructions.

## Role in the architecture

Contract → Guards → Single/Double Executors → Orchestrator → Consumer

## Instruction fields

- `sourcePath`: object containing `fileName` and `filePath`; the path identifies the input in the registry.
- `destinationPath`: object containing `fileName` and `filePath`; the path identifies where the result is written.
- `func`: registered function name.
- `templateKey`: optional template name used by template-based functions.
- `narration`: optional human-readable description for logs.

## Usage notes

This repository is one package in a multi-package workspace. Keep versioned implementation under `src/vN/` and expose the current version through `src/index.js`. Install the declared dependencies before running the package. The packages are separate repositories in the intended publishing model; placing them together in this ZIP does not publish them to npm or create GitHub repositories.

## Documentation

Open [`docs/index.html`](docs/index.html) for the architecture overview and examples.
