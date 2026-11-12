# Changelog

All notable changes to Raven MCP are recorded here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and the app uses [semantic versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

**The initial scaffold.**

- `tools/manifest.py` — 7 tool(s), declared as the contract.
  Imports no Frappe, so the core can validate it on a machine with none of this
  app's dependencies installed.
- `agent.py` — persona, boundaries and prompts, as pure data.
- `tools/handlers.py` — a generic in-process CRUD backend over this
  extension's DocTypes.
- `hooks.py` — `frappe_mcp_tools` points at the manifest; `frappe_mcp_agent`
  points at the agent.
- `install.py` — creates the role and the Single settings row, idempotently.
- `tests/test_manifest.py` — the contract tests, run against the real core.

### The decisions it carries

- **A Frappe hook, not a Python entry point.** An entry point lives in the bench
  virtualenv every site shares, so its tools would appear on sites that do not
  have this app installed. A hook is site-scoped.
- **The tools run in-process.** A REST hop would run as a service principal and
  see Administrator's permissions.
- **No flows.** A flow is a genuine multi-step transaction, and that is a
  decision rather than a default.
