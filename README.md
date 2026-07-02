# Pi Community Marketplace

Curated community extensions from the [Pi](https://github.com/badlogic/pi-mono) (pi-mono)
ecosystem, packaged as an OMP/Dimension plugin marketplace. Pi is the upstream ancestor of
Dimension's engine — Pi extensions load natively, no conversion.

## Install

In Dimension (or any OMP agent):

```
/marketplace add insodimension/pi-community-marketplace
/marketplace install pi-web-access@pi-community
```

## Curation bar

Every entry must pass all four before it ships:

1. **License** — MIT or compatible, attribution preserved.
2. **Source review** — full read of the extension source at the pinned SHA.
   Pi extensions run with full system access; nothing lands unreviewed.
3. **SHA-pinned** — entries pin an exact reviewed commit, never a moving branch.
   Version bumps re-review the diff.
4. **ACP-safe** — the extension's JOB survives outside the TUI (Dimension runs
   engines headless over ACP). TUI nice-to-haves may degrade; core behavior may not.

## Entries

| Plugin | Author | What it does | Review notes |
|---|---|---|---|
| `apply-patch-tool` | [kcosr](https://github.com/kcosr/pi-extensions) | Codex-style `apply_patch` tool + prompt guidance | Pure tool + prompt injection; zero deps; verified loading unmodified in OMP |
| `pi-web-access` | [Nico Bailon](https://github.com/nicobailon/pi-web-access) | Web search / fetch / PDF / YouTube (BYO key) | Keys are user-supplied env/config; Chrome-cookie Gemini auth is **opt-in**; ships SSRF allow-range tests |
| `pi-permission-system` | [Chris Lasher](https://github.com/gotgenes/pi-packages) | Policy-based tool-call permission enforcement | Pure policy engine; no exec/network in src; tree-sitter bash parsing |

## Reviewed-but-excluded (and why)

- `assistant`, `codemap`, `skill-picker` (kcosr) — core job IS a custom TUI overlay
  (`ctx.ui.custom`); nothing left under ACP.
- `toolwatch` (kcosr) — `file:./common` dep needs a postinstall build; conflicts with
  untrusted-lifecycle-scripts policy.
- `pi-simplify`, `pi-lens` — loadable only from built npm artifacts (`dist/`), not git
  source; revisit when npm plugin sources land.
- `pi-mcp-adapter`, `pi-subagents`, rpiv todo/ask — redundant: OMP ships native MCP,
  subagents, todo, and ask elicitation.

## Adding an entry

Open a PR adding the entry to `.omp-plugin/marketplace.json` with: pinned `sha`,
`license`, `author`, `repository`, and a review note in this README covering the
four-point bar above.
