# Governance Domains

AGS defines 9 behavioral governance domains, numbered 7-15 to align with the OASB domain numbering scheme (OASB infrastructure security domains are 1-6).

---

## Domain Index

| # | Domain | File | Controls | Focus |
|---|--------|------|----------|-------|
| 7 | Trust Hierarchy | [07-trust-hierarchy.md](07-trust-hierarchy.md) | 3 | Who the agent trusts and how it resolves conflicts between principals |
| 8 | Capability Boundaries | [08-capability-boundaries.md](08-capability-boundaries.md) | 4 | What the agent is allowed and denied to do |
| 9 | Injection Hardening | [09-injection-hardening.md](09-injection-hardening.md) | 3 | Defenses against prompt injection and instruction manipulation |
| 10 | Data Handling | [10-data-handling.md](10-data-handling.md) | 3 | Treatment of PII, credentials, and sensitive data |
| 11 | Hardcoded Behaviors | [11-hardcoded-behaviors.md](11-hardcoded-behaviors.md) | 3 | Immutable safety rules that cannot be overridden |
| 12 | Agentic Safety | [12-agentic-safety.md](12-agentic-safety.md) | 4 | Operational limits for autonomous execution |
| 13 | Honesty and Transparency | [13-honesty-transparency.md](13-honesty-transparency.md) | 3 | Truthfulness, uncertainty, and identity disclosure |
| 14 | Human Oversight | [14-human-oversight.md](14-human-oversight.md) | 3 | Approval gates, overrides, and monitoring |
| 15 | Harm Avoidance | [15-harm-avoidance.md](15-harm-avoidance.md) | 4 | Pre-action risk assessment, proportional response, unintended impact, ambiguity resolution |

---

## Severity Distribution

| Severity | Count | Controls |
|----------|-------|----------|
| CRITICAL | 2 | SOUL-IH-003, SOUL-HB-001 |
| HIGH | 8 | SOUL-TH-001, SOUL-CB-001, SOUL-CB-002, SOUL-IH-001, SOUL-HB-002, SOUL-HB-003, SOUL-HO-001, SOUL-HV-001 |
| MEDIUM | 13 | SOUL-TH-002, SOUL-CB-003, SOUL-DH-001, SOUL-DH-002, SOUL-AS-001, SOUL-HT-001, SOUL-HT-002, SOUL-HT-003, SOUL-HO-002, SOUL-HO-003, SOUL-HV-002, SOUL-HV-003, SOUL-HV-004 |
| LOW | 7 | SOUL-TH-003, SOUL-CB-004, SOUL-IH-002, SOUL-DH-003, SOUL-AS-002, SOUL-AS-003, SOUL-AS-004 |

---

## Relationship Between Domains

The 9 domains are designed to be orthogonal -- each addresses a distinct governance concern. However, some natural relationships exist:

- **Trust Hierarchy (7)** informs **Human Oversight (14)**: The trust hierarchy defines who can override whom, which determines the approval gate structure.
- **Capability Boundaries (8)** connect to **Hardcoded Behaviors (11)**: Denied actions (8) may overlap with safety immutables (11), but they serve different purposes. Denied actions can potentially be changed by operators; hardcoded behaviors cannot.
- **Injection Hardening (9)** supports **Trust Hierarchy (7)**: Injection defenses protect the trust chain from manipulation by untrusted inputs.
- **Data Handling (10)** connects to **Hardcoded Behaviors (11)**: The "no data exfiltration" rule (11) is a specific case of data handling policy (10), elevated to hardcoded status because of its severity.
- **Agentic Safety (12)** extends **Capability Boundaries (8)**: While capability boundaries define what the agent can do, agentic safety limits how much it can do in a single execution.
- **Harm Avoidance (15)** occupies a distinct position relative to existing domains:
  - **Capability Boundaries (8)** define what the agent _can_ do. **Harm Avoidance (15)** governs whether it _should_ in a specific context.
  - **Hardcoded Behaviors (11)** define absolute prohibitions. **Harm Avoidance (15)** governs the gray area between permitted and prohibited.
  - **Human Oversight (14)** defines when to ask a human. **Harm Avoidance (15)** governs the agent's own judgment before the question of human approval arises.
  - **Agentic Safety (12)** limits operational scope (iterations, budget, time). **Harm Avoidance (15)** assesses the qualitative risk of individual actions within those operational limits.
