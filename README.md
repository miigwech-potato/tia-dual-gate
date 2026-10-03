# tia-dual-gate

Optional **authority gate** for [danja/tia](https://github.com/danja/tia): OCap-style capabilities + hybrid human authorization on MCP tool calls.

Proposed upstream path: copy `src/harness/` and `test/authority-gate.test.js` into a TIA checkout; wire only when opted in.

## Why

TIA is a strong multi-agent chat + MCP runtime. Without an Act boundary, tool calls are capability without authority. This package (and the matching PR to TIA) adds:

- process-local capabilities (issue / attenuate / check)
- hybrid seal aligned with [hivemind](https://github.com/miigwech-potato/hivemind) (`authorized_by` + `what_was_seen` + ttl + single-use proposal)
- dual gate: both must pass before `execute`

Default TIA behavior stays unchanged until you use `invokeWithDualGate` or `createGatedBridge`.

## Layout (as would appear in TIA)

```text
src/harness/
  caps.js
  hybrid.js
  authority-gate.js
  index.js
  README.md
test/authority-gate.test.js
```

## Test

```bash
# from a TIA tree with these files at src/harness and test/
node --test test/authority-gate.test.js
```

## Upstream PR target

https://github.com/danja/tia — optional module under `src/harness/`, no change to default `McpClientBridge.callTool` unless callers opt in.

Maintainer: miigwech-potato (hivemind hybrid authorization experiment).
