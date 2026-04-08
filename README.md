<p align="center">
  <h1 align="center">Sentrik</h1>
  <p align="center"><strong>Governance runtime for AI-generated code</strong></p>
  <p align="center">Scan, gate, and trace compliance automatically — before it ships.</p>
</p>

<p align="center">
  <a href="https://sentrik.dev">Website</a> &bull;
  <a href="https://docs.sentrik.dev">Docs</a> &bull;
  <a href="https://github.com/maxgerhardson/sentrik-community/discussions">Community</a> &bull;
  <a href="https://sentrik.dev/pricing">Pricing</a>
</p>

---

## What is Sentrik?

Sentrik is a CLI + dashboard that enforces coding standards, compliance rules, and security policies on every commit. Built for teams using AI coding agents (Claude Code, Cursor, Copilot) where code is generated faster than humans can review it.

**The problem:** AI agents write code that *works* but may violate security policies, compliance requirements, or architectural standards. Nobody catches it until audit time.

**The solution:** Sentrik scans every change against regulatory standards (OWASP, SOC 2, HIPAA, PCI-DSS, FDA IEC 62304, and more), gates PRs that fail, and generates audit-ready evidence.

## Install

```bash
# npm (recommended)
npm install -g sentrik

# pip
pip install sentrik

# Docker
docker run maxgerhardson/sentrik scan
```

## Quick Start

```bash
# 1. Initialize your project (auto-detects language, frameworks, CI)
sentrik init

# 2. Scan your code
sentrik scan

# 3. Enforce the gate in CI (exit 1 on failure)
sentrik gate

# 4. Launch the dashboard
sentrik dashboard
```

## Free Tier (forever, no credit card)

Sentrik includes **5 standards packs** with **158 rules** for free:

| Pack | Rules | What it catches |
|------|-------|-----------------|
| **OWASP Top 10** | 69 | SQL injection, XSS, auth flaws, SSRF, and more |
| **SOC 2** | 30 | Trust services criteria for security & availability |
| **Python Security** | 18 | eval/exec, pickle, subprocess, Django/Flask vulns |
| **Go Security** | 15 | Injection, crypto misuse, unsafe, concurrency bugs |
| **Supply Chain Security** | 26 | SLSA, SBOM, dependency integrity, AI tool supply chain |

Plus built-in commands at every tier:
- `sentrik scan` / `sentrik gate` - Scan and enforce
- `sentrik vulns` - Dependency vulnerability scanning (CVEs)
- `sentrik sbom` - Software bill of materials
- `sentrik secrets` - Hardcoded secrets detection
- `sentrik dashboard` - Web UI with findings, charts, and reports
- `sentrik threat-model` - STRIDE threat analysis
- `sentrik quality-score` - Code quality scoring (0-100)

## Paid Tiers

| | Free | Team ($29/mo) | Organization ($99/mo) |
|---|---|---|---|
| Standards packs | 5 | 16 | 22 |
| OWASP, SOC 2, Supply Chain | Yes | Yes | Yes |
| HIPAA, PCI-DSS, ISO 27001, GDPR | - | Yes | Yes |
| FDA IEC 62304, NIST, CMMC | - | Yes | Yes |
| MISRA-C, DO-178C, ISO 26262 | - | - | Yes |
| Vulnerability scanning | Yes | Yes | Yes |
| Dashboard | Yes | Yes | Yes |
| Work item reconciliation | - | Yes | Yes |
| Custom rules | - | - | Enterprise |
| Parallel scanning | - | - | Yes |
| Governance & audit log | - | - | Enterprise |

[View pricing](https://sentrik.dev/pricing)

## CI/CD Integration

### GitHub Actions

```yaml
# .github/workflows/sentrik.yml
name: Sentrik Gate
on: [pull_request]
jobs:
  gate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - run: npm install -g sentrik
      - run: sentrik gate --git-range "origin/main...HEAD"
```

### GitLab CI

```yaml
sentrik:
  image: maxgerhardson/sentrik:latest
  script:
    - sentrik gate --git-range "origin/main...HEAD"
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
```

### Azure Pipelines

```yaml
- script: |
    npm install -g sentrik
    sentrik gate --git-range "origin/main...HEAD"
  displayName: Sentrik Gate
```

## AI Agent Integration

Sentrik works as an MCP server for AI coding agents:

```bash
# Start MCP server for Claude Code, Cursor, VS Code
sentrik mcp-server
```

The MCP server gives AI agents real-time access to compliance rules, scan results, and remediation guidance — so they write compliant code from the start.

## Example Configurations

### Starter (web app)

```yaml
# .sentrik/config.yaml
standards_packs:
  - owasp-top-10
  - supply-chain-security
gate:
  fail_on:
    - critical
    - high
```

### Healthcare / Medical Device

```yaml
standards_packs:
  - owasp-top-10
  - hipaa
  - fda-iec-62304
  - supply-chain-security
gate:
  fail_on:
    - critical
    - high
    - medium
```

### Fintech

```yaml
standards_packs:
  - owasp-top-10
  - pci-dss
  - soc2
  - supply-chain-security
gate:
  fail_on:
    - critical
    - high
```

### Government / Defense

```yaml
standards_packs:
  - owasp-top-10
  - nist-800-53
  - cmmc
  - supply-chain-security
gate:
  fail_on:
    - critical
    - high
    - medium
```

## Community

- **[Discussions](https://github.com/maxgerhardson/sentrik-community/discussions)** - Ask questions, share tips, show what you've built
- **[Issues](https://github.com/maxgerhardson/sentrik-community/issues/new/choose)** - Report bugs or request features
- **[Documentation](https://docs.sentrik.dev)** - Full CLI reference, configuration guide, API docs

## Support

| Channel | For |
|---------|-----|
| [GitHub Discussions](https://github.com/maxgerhardson/sentrik-community/discussions) | Questions, ideas, community help |
| support@sentrik.dev | Direct support (paid tiers) |
| sales@sentrik.dev | Pricing and licensing |

## License

Proprietary. Free tier available forever with no credit card required.
