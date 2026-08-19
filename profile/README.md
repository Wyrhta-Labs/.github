<h1 align="center">Heorth</h1>

<p align="center">
  <b>A self-hosted household manager.</b><br>
  One deployment per household — calendar, meals, finance, library, inventory,<br>
  and the people around it. Your data, your hardware.
</p>

<p align="center"><sub>from <b>Wyrhta Labs</b></sub></p>

<p align="center">
  <a href="https://github.com/Wyrhta-Labs/Heorth">Heorth</a> ·
  <a href="https://github.com/Wyrhta-Labs/KithLedger">KithLedger</a> ·
  <a href="https://www.npmjs.com/package/@wyrhta/core">@wyrhta/core</a> ·
  <a href="https://github.com/Wyrhta-Labs/wyrhta">Concept &amp; decisions</a>
</p>

---

**Wyrhta Labs** (Old English *wyrhta* — "maker, wright") builds Heorth and the small
services around it: each its own repo, each releasing on its own cadence, integrating
over plain REST. Not a monorepo, not a plugin platform, not a hosted product.

## The repos

| Repo | What it is |
|---|---|
| [**Heorth**](https://github.com/Wyrhta-Labs/Heorth) | The household system — calendar, meals, finance (Feoh), library, inventory, and the **Hearth View** kitchen touchscreen. |
| [**KithLedger**](https://github.com/Wyrhta-Labs/KithLedger) | API-first personal relationship manager, built to be consumed by other tools rather than used standalone. |
| [**heorth-mcp**](https://github.com/Wyrhta-Labs/heorth-mcp) | The household's single MCP server: one Streamable HTTP endpoint over the services' REST APIs. Owns no data. |
| [**wyrhta-core**](https://github.com/Wyrhta-Labs/wyrhta-core) | Shared foundation `@wyrhta/core` — identity, auth, HTTP kit, household, DB conventions. On [npm](https://www.npmjs.com/package/@wyrhta/core). |
| [**wyrhta**](https://github.com/Wyrhta-Labs/wyrhta) | The umbrella repo: the concept, the decision records, and the Compose stack that knows every service exists. **Start here.** |
| [**website**](https://github.com/Wyrhta-Labs/website) | The public site. Published to be read, not forked — it carries no licence. |

## Getting started

The umbrella repo has both quick starts —
[**set up the workspace**](https://github.com/Wyrhta-Labs/wyrhta#getting-the-whole-workspace)
(one script clones every service and keeps it current) and
[**run the whole stack**](https://github.com/Wyrhta-Labs/wyrhta/blob/main/deploy/README.md)
(Compose, ports, databases, backups). Each service also runs on its own — see its README.

## How it fits together

- **Independent repos, shared by version.** Services take `@wyrhta/core` from npm at a
  pinned range; a core change reaches them only when a pin is bumped deliberately.
- **REST only; MCP is a container.** Services ship HTTP APIs. Agent tooling lives in
  `heorth-mcp` — a new service gains tools there, never its own MCP surface.
- **External systems stay the system of record.** Microsoft 365 owns calendars, To Do
  owns everyday tasks; Heorth mirrors and enriches behind pluggable providers.

Every cross-cutting decision is an
[ADR](https://github.com/Wyrhta-Labs/wyrhta/tree/main/docs/decisions) — the fastest way
to see why the architecture looks like this.

## Status, contributing, security

Pre-1.0, one maker, **own household first**. MIT, and public so it can be read and run
— but *"ready for other self-hosters"* is the 1.0 gate and we are not there yet. Expect
breaking changes between minors.

Please open an issue before a large PR; each repo's `CONTRIBUTING.md` states the cadence.
Security problems go through GitHub's **private vulnerability reporting** on the affected
repo, never a public issue — see `SECURITY.md`.

<p align="center"><sub>MIT licensed · built for one household, in the open</sub></p>
