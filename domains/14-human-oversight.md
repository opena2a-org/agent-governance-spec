# Domain 14: Human Oversight

## Purpose

The Human Oversight domain establishes requirements for human approval gates, override mechanisms, and monitoring of agent behavior. It ensures that humans maintain meaningful control over agent actions, especially for high-risk or consequential operations.

## Rationale

As agents become more capable and autonomous, the risk of unintended consequences grows. A coding agent might deploy to production, a financial agent might execute transactions, or a customer service agent might make commitments that bind the organization. Without human oversight mechanisms, there is no checkpoint between the agent's decision and the real-world consequence.

Human oversight governance does not mean humans must approve every action -- that would negate the efficiency benefits of automation. Instead, it defines which actions require approval (approval gates), how humans can intervene when needed (override mechanisms), and how agent behavior is tracked for review (monitoring and logging).

## Controls

### SOUL-HO-001: Approval Gates

| Attribute | Value |
|-----------|-------|
| **ID** | SOUL-HO-001 |
| **Severity** | HIGH |
| **Applicable tiers** | TOOL-USING, AGENTIC, MULTI-AGENT |

**Description**: The governance file defines specific actions or categories of actions that require explicit human approval before the agent proceeds. These gates should be calibrated to the risk level of the actions -- routine actions proceed without approval, while high-risk or irreversible actions require explicit confirmation.

**Detection keywords**: `approval`, `confirm`, `confirmation`, `human approval`, `user approval`, `ask before`, `require permission`, `gate`, `checkpoint`, `authorization`, `consent`, `approval gate`, `must confirm`

**Example compliant text**:
```
## Approval Gates
The following actions require explicit user approval before execution:
- Deploying code to any environment (staging, production)
- Deleting files, directories, or database records
- Making purchases or financial transactions
- Sending emails, messages, or notifications on behalf of the user
- Modifying access controls, permissions, or security settings
- Installing or updating system-level packages or dependencies

Routine actions that do not require approval:
- Reading files and directories within the project scope
- Running tests and linting
- Creating new files within the project directory
- Making git commits on the current branch
```

---

### SOUL-HO-002: Override Mechanism

| Attribute | Value |
|-----------|-------|
| **ID** | SOUL-HO-002 |
| **Severity** | MEDIUM |
| **Applicable tiers** | TOOL-USING, AGENTIC, MULTI-AGENT |

**Description**: The governance file defines how humans can override or correct agent behavior during execution. This includes how to cancel an in-progress action, how to undo a completed action, and how to modify the agent's behavior for the current session without editing the governance file.

**Detection keywords**: `override`, `correct`, `undo`, `cancel`, `intervene`, `interrupt`, `take over`, `manual control`, `human override`, `correction`, `override mechanism`

**Example compliant text**:
```
## Override Mechanism
Users can override agent behavior at any time:
- Type "stop" or "cancel" to halt the current operation immediately
- Type "undo" to reverse the last action if it was reversible
- Type "pause" to suspend autonomous execution and switch to step-by-step mode
- Any explicit user instruction takes immediate effect, even if it contradicts the agent's current plan
- The user can modify the agent's approach by providing new constraints mid-task
```

---

### SOUL-HO-003: Monitoring and Logging

| Attribute | Value |
|-----------|-------|
| **ID** | SOUL-HO-003 |
| **Severity** | MEDIUM |
| **Applicable tiers** | TOOL-USING, AGENTIC, MULTI-AGENT |

**Description**: The governance file declares that the agent's actions are logged or otherwise observable for post-hoc review. This enables operators and users to audit what the agent did, verify that governance constraints were followed, and investigate incidents.

**Detection keywords**: `log`, `logging`, `monitor`, `audit`, `trace`, `record`, `observable`, `tracking`, `audit trail`, `event log`, `activity log`, `monitoring`, `observability`

**Example compliant text**:
```
## Monitoring and Logging
This agent supports observability:
- All tool calls and their results are logged for audit purposes
- Decisions that involve governance constraints (e.g., declining a request) are logged with the reason
- Error conditions and unexpected states are logged with diagnostic context
- Logs do not contain PII or credentials (see Data Handling section)
- Operators can review agent activity through the audit log
- The agent does not tamper with or suppress its own logs
```

---

## Relationship to Model Specifications

Human oversight is a central concern in AI safety frameworks:

- SOUL-HO-001 (Approval gates) extends Anthropic's concept of "supporting human oversight" from a general principle to specific, declared checkpoints that can be audited.
- SOUL-HO-002 (Override mechanism) maps to the controllability requirements in both Anthropic and OpenAI specifications -- the ability for humans to correct, redirect, or stop the system.
- SOUL-HO-003 (Monitoring/logging) supports the transparency requirements in AI governance frameworks (EU AI Act, NIST AI RMF) by ensuring that agent behavior is observable and auditable.

The EU AI Act's requirements for high-risk AI systems include human oversight provisions that map directly to this domain. AGS provides a practical, file-level mechanism for declaring and auditing compliance with these requirements.
