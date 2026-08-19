<h1 align="center">Wyrhta Labs</h1>

<p align="center">
  <b>An interconnected, self-hosted household manager.</b><br>
  One deployment per household — calendar, meals, finance, library, inventory,<br>
  and the people around it. Your data, your hardware.
</p>

<p align="center">
  <a href="https://github.com/Wyrhta-Labs/Heorth">Heorth</a> ·
  <a href="https://github.com/Wyrhta-Labs/KithLedger">KithLedger</a> ·
  <a href="https://www.npmjs.com/package/@wyrhta/core">@wyrhta/core</a> ·
  <a href="https://github.com/Wyrhta-Labs/wyrhta">Concept &amp; decisions</a>
</p>

---

**Wyrhta** (Old English *wyrhta* — "maker, wright") is a household system built from
several small services that release on their own cadence and talk to each other over
plain REST. Not a monorepo, not a plugin platform, not a hosted product.

## The repos

| Repo | What it is |
|---|---|
| [**Heorth**](https://github.com/Wyrhta-Labs/Heorth) | The flagship household system — calendar, meals, finance (Feoh), library, inventory. Ships the UI, including the **Hearth View** kitchen touchscreen. |
| [**KithLedger**](https://github.com/Wyrhta-Labs/KithLedger) | API-first personal relationship manager. Designed to be consumed by other tools rather than used standalone. |
| [**heorth-mcp**](https://github.com/Wyrhta-Labs/heorth-mcp) | The household's single MCP server. One Streamable HTTP endpoint fronting every service's REST API — it owns no data. |
| [**wyrhta-core**](https://github.com/Wyrhta-Labs/wyrhta-core) | Shared foundation `@wyrhta/core`: identity, auth, HTTP kit, household, DB conventions. On [npm](https://www.npmjs.com/package/@wyrhta/core). |
| [**wyrhta**](https://github.com/Wyrhta-Labs/wyrhta) | The umbrella repo: concept, architecture decision records, and the Docker Compose stack that knows every service exists. **Start here to read.** |
| [**website**](https://github.com/Wyrhta-Labs/website) | The public site. Published to be read, not forked — it carries no licence. |

## Where it stands

Pre-1.0, one maker, **own household first**. The code is MIT and public so it can be
read, run, and learned from — but *"ready for other self-hosters"* is the 1.0 gate and
we are not there yet. Expect breaking changes between minor versions, and read each
repo's `CHANGELOG.md` before upgrading.

## Running it

Every service has its own README and quick start. To bring up the whole household stack:

```bash
gh repo clone Wyrhta-Labs/wyrhta && cd wyrhta
./scripts/clone-all.sh                     # or: pwsh ./scripts/clone-all.ps1
cp deploy/.env.example deploy/.env          # fill in every value
docker compose -f deploy/compose.dev.yml --env-file deploy/.env up -d --build
```

`clone-all` is both "set up" and "update everything" — it reads
[`repos.txt`](https://github.com/Wyrhta-Labs/wyrhta/blob/main/repos.txt), clones what
is missing, fast-forwards the rest, and never touches a dirty tree. Ports, databases,
and the production compose file are documented in
[`deploy/README.md`](https://github.com/Wyrhta-Labs/wyrhta/blob/main/deploy/README.md).

## Developing on it

Each repo is independent: `npm ci`, then follow its README. Four conventions explain
most of what looks unusual:

- **Independent repos, shared by version.** Services consume `@wyrhta/core` from npm at
  a pinned range. A core change reaches a consumer only when a release is cut and the
  pin is bumped deliberately.
- **REST only; MCP is a container.** A service ships an HTTP API. Agent tooling lives in
  `heorth-mcp`, which calls those APIs. A new service gains tools there — it never grows
  its own MCP surface.
- **External systems stay the system of record.** Microsoft 365 owns calendars, To Do
  owns everyday tasks. Heorth mirrors and enriches behind provider interfaces that are
  pluggable from day one.
- **Decisions are written down.** Anything cross-cutting is an ADR in
  [`docs/decisions/`](https://github.com/Wyrhta-Labs/wyrhta/tree/main/docs/decisions) —
  the fastest way to understand why the architecture looks like this.

## Contributing & security

One maintainer, pre-1.0, ADR-governed — see any repo's `CONTRIBUTING.md` for what kinds
of contribution help most. Please **open an issue before a large PR**.

Security problems go through GitHub's private vulnerability reporting on the affected
repo, never a public issue. See `SECURITY.md`.

<p align="center"><sub>MIT licensed · built for one household, in the open</sub></p>
