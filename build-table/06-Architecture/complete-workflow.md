# Complete Workflow — From Data to Browser DOM

1. **Describe the work.** An instruction object identifies source and destination paths and a transformation function/template.
2. **Validate the instruction.** The contract and guard packages define and check the instruction shape.
3. **Resolve source data.** The source-path and traversal utilities locate the data to process.
4. **Transform at the required dimension.** Primitive transformation handles one object; one-dimensional transformation handles a collection; two-dimensional transformation handles columns and rows.
5. **Write the result.** The write-path package stores the computed structure at the requested destination.
6. **Compose a table when needed.** The table builder creates the declarative table structure; the options package can add optional table features.
7. **Validate the tag description.** The validator checks the JSON tag tree against the shared specification catalog.
8. **Create native DOM nodes.** The JSON-to-tag package turns the declarative description into browser elements.
9. **Mount the nodes.** spec-to-dom places the nodes in the target browser container; the high-level json-to-dom package coordinates the last stages.

## Important boundary

A JSON table specification is not yet a browser DOM tree. Table composition and native DOM generation are separate stages. This distinction is central to understanding the package boundaries.
