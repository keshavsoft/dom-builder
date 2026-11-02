# json-instruction-guards

Validates instruction objects against the shared contract before execution. It returns a result with valid and errors, allowing callers to report invalid instructions without silently dispatching unknown functions.

## Role in the architecture

Consumes the contract; used before either executor dispatches a function.

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
