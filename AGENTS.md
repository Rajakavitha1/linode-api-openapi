 Briefing file for AI coding agents. For human contributor context, see [README.md](README.md).

---

## What This Repo Is

This is a **distribution-only repository**. It contains a single packaged and distributable OpenAPI spec file for the Linode API:

```
openapi.json        # The complete Linode API OpenAPI 3.0 spec — do not hand-edit
```

This repo does NOT contain the source spec. The `openapi.json` file is generated upstream and published here as a release artifact. Do not make direct edits to `openapi.json` to add or change API endpoints — those changes will be overwritten on the next release.

---

## What You Can Do with the Linode API

The Linode API lets you programmatically manage the full range of Akamai cloud computing products and services. Key capabilities include:

- Build scripts and applications to automatically handle repeatable tasks
- Create and manage Linodes
- Deploy Linode Kubernetes Engine (LKE) clusters
- Attach Block Storage volumes
- Configure NodeBalancers
- Manage users
- View and update account details

All operations are performed via standard HTTP requests. Response data is returned in JSON format.

---

## Repo Structure

```
linode-api-openapi/
├── openapi.json        # Packaged OpenAPI 3.0 spec (auto-generated, read-only)
├── README.md           # Human-facing overview
├── LICENSE             # Apache 2.0
└── .gitignore
```

---

## What Agents Can Do Here

| Task | Notes |
|---|---|
| Read and parse `openapi.json` | Primary use case |
| Answer questions about API endpoints | Parse directly from the spec |
| Update `README.md` or `AGENTS.md` | Documentation changes are welcome |

Do not edit `openapi.json`, add new paths, or generate SDKs from the spec. See the Official [SDKs and Tools section](#official-sdks-and-tools).

---

## Spec Overview

- **Format**: OpenAPI 3.0 (JSON)
- **API**: Linode / Akamai Cloud Computing API v4
- **Base URL**: `https://api.linode.com/v4`
- **Auth**: Bearer token via `Authorization: Bearer <token>` header
- **Release cadence**: Updated via tagged releases (e.g. `release-20260123`)

### Key Sections in openapi.json

| Section | Path in spec | Description |
|---|---|---|
| API metadata | `info` | Version, title, contact, license |
| Servers | `servers` | Base URLs |
| All endpoints | `paths` | Every API route and method |
| Reusable schemas | `components.schemas` | Shared object definitions |
| Reusable parameters | `components.parameters` | Shared query/path params |
| Security schemes | `components.securitySchemes` | Auth definitions |

---

## Official SDKs and Tools

The Linode API SDKs are **hand-written**, not auto-generated from this spec. Only the Linode CLI is auto-generated from `openapi.json`. Do not attempt to generate other clients from the spec, instead use the official libraries:

| Language / Tool | Repo | Package | Generated from spec? |
|---|---|---|---|
| Python SDK | https://github.com/linode/linode_api4-python | `pip install linode_api4` | ❌ Hand-written |
| Go SDK | https://github.com/linode/linodego | `go get github.com/linode/linodego` | ❌ Hand-written |
| JavaScript / TypeScript SDK | https://github.com/linode/manager/tree/develop/packages/api-v4 | `npm install @linode/api-v4` | ❌ Hand-written |
| Linode CLI | https://github.com/linode/linode-cli | `pip install linode-cli` | ✅ Auto-generated from `openapi.json` |
| Terraform Provider | https://github.com/linode/terraform-provider-linode | via Terraform Registry | ❌ Hand-written |

This `openapi.json` spec is best used for reference, tooling integration, building API explorers, and as the source of truth for the Linode CLI — not as a general source for SDK generation.

---

## API Conventions to Know

These conventions are reflected in the spec and agents should follow them when generating code or documentation:

- **Pagination**: List endpoints return `data[]`, `page`, `pages`, `results`. Use `?page=` and `?page_size=` query params.
- **Filtering**: Supported via `X-Filter` request header with JSON filter objects.
- **Rate limits**: Returned in response headers (`X-RateLimit-Limit`, `X-RateLimit-Remaining`).
- **Time values**: All timestamps are UTC in ISO 8601 format (`2026-01-23T00:00:00`).
- **Error format**: All errors return `{ "errors": [{ "field": "...", "reason": "..." }] }`.
- **Auth**: All endpoints (except public ones) require `Authorization: Bearer <token>`.

---

## Releases

New versions of `openapi.json` are published as GitHub releases with tags in the format `release-YYYYMMDD`. See the [releases page](https://github.com/linode/linode-api-openapi/releases) for the changelog.

For API-level release notes, see: https://techdocs.akamai.com/linode-api/changelog

---

## Related Resources

| Resource | URL |
|---|---|
| API reference docs | https://techdocs.akamai.com/linode-api/reference/api |
| API release notes | https://techdocs.akamai.com/linode-api/changelog |
| Other Akamai OpenAPI specs | https://github.com/akamai/akamai-apis |
| Linode CLI (uses this spec) | https://github.com/linode/linode-cli |
| Linode Python SDK | https://github.com/linode/linode_api4-python |
| Linode Go SDK | https://github.com/linode/linodego |
| Linode Ansible | https://github.com/linode/ansible_linode |
