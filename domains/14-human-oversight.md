# Domain 14: Human Oversight

## Purpose

The Human Oversight domain governs the mechanisms by which humans maintain control over AI agent behavior. It defines requirements for approval gates before high-stakes actions, override mechanisms for correcting or halting agent behavior, and monitoring capabilities for observing what the agent is doing.

## Rationale

Autonomous AI agents are designed to act independently, but independence without oversight creates unacceptable risk. An agent that deploys code, sends communications, modifies data, or makes purchases without human review can cause harm that is difficult or impossible to reverse. Even well-governed agents make mistakes -- they misunderstand context, encounter edge cases not covered by their governance, or operate on stale information.

Human oversight is not a limitation on agent capability; it is an architectural requirement for responsible deployment. The goal is not to approve every action (which would eliminate the efficiency gains of automation) but to establish approval gates at high-stakes decision points and maintain the ability to intervene when something goes wrong.

The consequences of insufficient human oversight are material: unauthorized financial transactions, data breaches from misconfigured tools, incorrect communications sent to customers, and production systems damaged by untested changes. These failures become harder to detect and correct the longer an agent operates without oversight.

## Controls

### SOUL-HO-001: Approval Gates

| Attribute | Value |
|-----------|-------|
| **ID** | SOUL-HO-001 |
| **Severity** | HIGH |
| **Applicable tiers** | TOOL-USING, AGENTIC, MULTI-AGENT |

**Description**: The governance file defines specific actions or categories of actions that require human approval before execution. The agent must pause and request confirmation before taking these actions. Approval gates should be calibrated to the risk level -- routine operations proceed without approval, while high-stakes operations require explicit confirmation.

**Detection keywords**: `approval`, `confirm`, `human-in-the-loop`, `review`, `authorize`, `sign-off`, `gate`, `confirmation`, `ask before`, `require approval`, `user confirmation`, `explicit consent`, `permission`

**Example compliant text**:
```
## Approval Gates
This agent requires human approval before the following actions:
- Executing any command that modifies production systems or data
- Sending emails, messages, or other communications on behalf of the user
- Making purchases, financial transactions, or resource provisioning requests
- Deleting files, databases, or other persistent storage
- Publishing or deploying code to any environment
- Granting or modifying access permissions

Routine operations that do not require approval:
- Reading files and documentation
- Running tests in development environments
- Searching and retrieving information
- Generating code suggestions for user review
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
