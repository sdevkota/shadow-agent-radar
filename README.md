# Shadow Agent Radar

Discover and govern unsanctioned AI agent usage without blocking useful work.

> Version: 1.0.0 | License: MIT | Status: production-oriented v1 foundation

## Problem

Shadow AI has become shadow IT with memory, tools, and data retention. Bans rarely work, while unmanaged agents can leak sensitive data or act with unclear authority.

## What this project solves

A policy scanner that inventories declared agent capabilities, data classes, tools, and retention behavior, then produces governance findings and safer migration paths.

Shadow Agent Radar ships as a small, dependency-free CLI and library. It validates a domain-specific JSON packet, emits actionable findings, and gives contributors a concrete surface for adding adapters, richer checks, schemas, and integrations.

## Who it is for

Security, IT, privacy, and platform teams introducing approved agent stacks.

## Quick start

```bash
npm test
npm start -- sample
```

Analyze your own packet:

```bash
shadow-agent-radar ./packet.json
```

Or pipe JSON:

```bash
cat packet.json | node src/cli.js
```

## Example packet

```json
{
  "agent": {
    "name": "sales-helper",
    "owner": "growth"
  },
  "data": {
    "classes": [
      "customer_email",
      "contract_terms"
    ],
    "retentionDays": 90
  },
  "tools": [
    {
      "name": "gmail",
      "permission": "send"
    },
    {
      "name": "crm",
      "permission": "write"
    }
  ],
  "approvals": {
    "dpoReviewed": false
  }
}
```

## Library usage

```js
const { analyze } = require("./src/index.js");

const report = analyze({
  "agent": {
    "name": "sales-helper",
    "owner": "growth"
  },
  "data": {
    "classes": [
      "customer_email",
      "contract_terms"
    ],
    "retentionDays": 90
  },
  "tools": [
    {
      "name": "gmail",
      "permission": "send"
    },
    {
      "name": "crm",
      "permission": "write"
    }
  ],
  "approvals": {
    "dpoReviewed": false
  }
});
console.log(report.summary);
```

## v1 behavior

- Validates required fields for the domain packet.
- Scores readiness from 0 to 100.
- Reports missing or weak governance evidence.
- Suggests next actions and contributor extension points.
- Runs fully offline with no API keys and no network access.

## Contribution map

Good first contributions:

- Add browser extension telemetry.
- Add CASB integrations.
- Add SaaS discovery adapters.
- Add policy-as-code packs.

Larger contributions:

- Add a JSON Schema and compatibility tests.
- Build import/export adapters for popular AI frameworks.
- Add real-world fixtures from public, non-sensitive examples.
- Improve scoring with transparent, documented heuristics.

## Project principles

- Human agency over blind automation.
- Open standards over vendor lock-in.
- Auditable decisions over hidden magic.
- Privacy and safety as design constraints, not release notes.

## GitHub Pages

The marketing site lives in `site/index.html`. Enable GitHub Pages from the `site` folder or use the included Pages workflow after publishing.

## Security

This project does not process secrets by default. If you build adapters that touch production systems, keep least privilege, explicit consent, and auditable logs in the design.
