# TIA Authority Gate (optional harness)

**Opt-in** dual gate for MCP tool calls. Default TIA behavior is unchanged until you wrap a bridge.

## Rules

1. **Capability (OCap-style)** — Worker holds an unforgeable handle for `tool:<name>` + task. No ambient tool rights. Attenuation only (child ⊆ parent).
2. **Hybrid human record** — Same semantics as [hivemind](https://github.com/miigwech-potato/hivemind): Act requires `AUTHORIZED` with non-empty `authorized_by` and `what_was_seen`, future `ttl`, and single-use `proposal_hash` (process-local spent set).
3. **Order** — Check capability → `mayAct` → `consume` → execute. Either failure → HOLD, no side effect.
4. **A capability never replaces the human record.**

## Usage

See repository README and `test/authority-gate.test.js`.

Speech is not permission. Capability is not authority.
