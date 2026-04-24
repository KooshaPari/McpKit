# McpKit

Polyglot MCP (Model Context Protocol) framework SDK for the Phenotype ecosystem. Provides idiomatic client and server primitives in Go, Rust, TypeScript, and Python from a single registry-driven source of truth.

**Part of the [Phenotype org](https://github.com/KooshaPari) ecosystem.** Shares CI reusables and conventions with [phenoShared](https://github.com/KooshaPari/phenoShared). Follows org conventions: conventional commits, `<type>/<topic>` branching, Apache-2.0 + MIT dual license.

## What it does

McpKit gives Phenotype services a uniform way to build and consume MCP servers/clients regardless of host language. A shared [`registry.yaml`](./registry.yaml) declares the canonical tool, resource, and prompt catalog; each language binding generates typed surfaces from it so Go services, Rust daemons, TypeScript IDE extensions, and Python notebooks all speak the same MCP contract.

Downstream consumers include agent frameworks, the [PhenoRuntime](https://github.com/KooshaPari/PhenoRuntime) MCP server, and external-intake pipelines.

## Status

**Active.** Multi-language scaffolding in place; bindings track the registry at release time. Owner: `team-agents`.

## Requirements

- **Go** binding: Go 1.22+
- **Rust** binding: Rust stable, edition 2021
- **TypeScript** binding: Node 20+ (pnpm preferred)
- **Python** binding: Python 3.11+ (`uv` or `pip` — `pyproject.toml` at repo root)

## Quick start

Clone and build the binding you need:

```bash
# Go
cd go && go build ./... && go test ./...

# Rust
cd rust && cargo build --workspace && cargo test --workspace

# TypeScript
cd typescript && pnpm install && pnpm build && pnpm test

# Python
uv sync            # or: pip install -e '.[dev]'
uv run pytest      # or: pytest
```

## Structure

```
go/            # Go MCP bindings (go.work multi-module)
rust/          # Rust MCP crates (cargo workspace)
typescript/    # TypeScript MCP bindings (package workspace)
python/        # Python MCP bindings (pyproject-driven)
registry.yaml  # Canonical MCP tool/resource/prompt registry — source of truth
pyproject.toml # Python packaging / dev tooling entry
```

## Design principles

- **Registry is the source of truth.** All bindings derive from `registry.yaml`; drift is a bug.
- **Idiomatic per language.** Each binding feels native (Go interfaces, Rust traits, TS generics, Python protocols) — the registry normalizes semantics, not surface syntax.
- **Wrap, do not hand-roll.** Leverages the official `modelcontextprotocol` SDKs where available; adds Phenotype conventions on top.
- **Fail loudly on contract mismatch.** Registry/binding divergence is caught at build time, not runtime.

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md). Ownership lives in [CODEOWNERS](./CODEOWNERS). Report security issues per [SECURITY.md](./SECURITY.md).

## License

Dual-licensed under Apache-2.0 OR MIT. See [LICENSE-APACHE](./LICENSE-APACHE) and [LICENSE-MIT](./LICENSE-MIT).
