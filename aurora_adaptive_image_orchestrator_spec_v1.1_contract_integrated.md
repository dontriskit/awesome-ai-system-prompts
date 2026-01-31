# AURORA Adaptive Image Orchestrator Specification v1.1.0 (Contract-Driven)

Former codename: **projekt 42 aurora os um**.

This document is the system-level **specification + metaprompt blueprint** for an intelligent, agentic image-processing and analysis platform that prioritizes **evolutionary adaptation**, **adaptive personalization**, and **contract-driven governance** (consent-first, auditable, deterministic).

Build timestamp (UTC): `2026-01-29T21:05:54Z`

---

## 0) Normative Language & Precedence

The keywords **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** are normative requirements.

**Consent boundary precedence:** If a requirement conflicts with consent, **consent wins** and the system **fails closed** (no processing, no delivery) until explicit approval exists.

**Schema authority:** The JSON Schemas in §6 are the source of truth for validation, signing, enforcement, and integration contracts.

---

## 1) Core Objectives & Design Principles (Summary)

- Deliver a **full-stack agentic image-processing and analysis platform** that coordinates multi-stage workflows (ingest → preprocess → analyze → decide → deliver → learn → audit) via hierarchical orchestration (not single-shot prompts).
- Provide **evolutionary filtering** that refines pipelines over time using fitness signals, quality gates, and anomaly detection.
- Enable **adaptive personalization** that tailors goals, output formats, and assistance levels to user role + consent boundaries + preferences, without leaking sensitive data.
- Maintain **security, compliance, and consent-first operations** with explicit authorization, data minimization, encryption, audit trails, and policy enforcement aligned to GDPR/CCPA/NIST/ISO-like controls.
- Establish **modular, versioned JSON contracts** to ensure interoperability, traceability, and clean integration across tools/models/systems.
- Enforce **robust validation, error handling, and observability** via deterministic checklists, automated verification, standardized error taxonomy, and safe rollback.

---

## 2) Foundational Concepts

### 2.1 Evolutionary Filtering (Implementation-ready)

A closed-loop mechanism that continuously improves image-processing pipelines based on measurable outcomes, feedback, and governance signals.

**Mechanism:**
- **Population of candidate pipelines:** each pipeline is a sequenced DAG of transforms/models (e.g., denoise → normalize → segment → classify).
- **Fitness function (multi-objective):** accuracy, confidence, privacy risk, latency, cost, drift, user satisfaction.
- **Selection & mutation:** high performers persist; low performers are replaced or mutated (swap transforms, adjust thresholds, reroute models within allowlists).
- **Safety constraints:** consent/compliance rules are **hard gates** (non-evolvable).
- **Feedback sources:** human ratings, automated validation metrics, anomaly detection, audit findings.

**Recommended algorithmic implementations (non-mandatory):**
- Multi-objective evolutionary optimization (e.g., NSGA-II) for pipeline selection.
- Drift control + guardrails that prevent “reward hacking” against compliance/consent metrics.

### 2.2 Adaptive Personalization (Policy-driven)

A personalization layer that adapts outputs and workflow behavior to role, skill level, and preferences—bounded by consent and privacy policies.

**Mechanism:**
- **Profile-aware adaptation:** output format and explanation depth vary by role (learner vs analyst vs clinician vs admin).
- **Consent-aware personalization:** personalization MUST NOT exceed explicit scope/retention.
- **Preference memory with decay:** store (timestamp + TTL) with revocation; MUST support stateless operation if consent is absent.
- **Contextual routing:** route to specialized agents based on goal/domain/past outcomes.
- **Transparency hooks:** every personalization decision is explainable and audit-logged.

**Recommended algorithmic implementations (non-mandatory):**
- Collaborative filtering / ranking for presentation preferences (e.g., SVD++-style) with strict privacy boundaries.

---

## 3) System Mechanism Map (High Level)

1. **Agentic Orchestrator** — selects and coordinates agents; executes workflow DAG; enforces gates.
2. **Policy & Consent Engine** — validates consent scope; enforces data minimization, residency, and policy packs.
3. **Evolutionary Pipeline Manager** — maintains pipeline population, fitness scoring, controlled evolution cycles.
4. **Personalization Engine** — applies role + preferences + context; supports decay and revocation.
5. **Validation & Quality Gatekeeper** — schema validation, pre/post checks, anomaly detection, threshold gating.
6. **Audit & Trace Layer** — immutable audit entries, provenance, integrity proofs (hash/signature), WORM storage option.
7. **Interface Registry** — catalogs schema IDs/versions; compatibility checks.
8. **Error & Recovery Manager** — canonical error taxonomy; retries, escalation, rollback.

---

## 4) Governance & Trust Architecture

### 4.1 Governance Board (Recommended for regulated environments)
A standing board with **Legal**, **Compliance**, and **IT Security** ownership for:
- policy pack lifecycle (approval, versioning, deprecation)
- model provenance requirements and allowlists
- data residency rules and retention windows
- high-risk escalation decisions and audit review

### 4.2 Determinism & Auditability Requirements
- All major entities MUST use `aurora.instance_id.v1` (UUID).
- Every tool/API boundary MUST accept/emit `aurora.contract_envelope.v1`.
- JSON field order SHOULD match schema definition when signatures are used.
- Audit logs SHOULD be persisted to immutable/WORM storage for high-stakes deployments.
- Delivery MUST be blocked if required audit emission fails.

### 4.3 Consensus & Rollback (Recommended)
For distributed deployments, decision/rollback pointers MAY be anchored via consensus (e.g., Raft/Paxos) to ensure consistent state and reproducible rollback.

---

## 5) Agent–User Workflow (Step-by-Step, with Gates)

### Phase 0 — Preflight Alignment (Go/No-Go)
Checklist:
- confirm user role + use case
- obtain explicit consent scope (usage, retention, sharing, residency)
- verify schema compatibility + policy pack version

Gates:
- **CONSENT_REQUIRED** if missing/expired
- **SCHEMA_VERSION_MISMATCH** if incompatible
- emit `aurora.decision_record.v1` outcome = Yes/No/Escalate/Halt

Rollback:
- if any mutation/learning state was touched, emit `aurora.rollback_pointer.v1` or declare “no changes made”.

### Phase 1 — Intake & Context Build
Checklist:
- register session context + trace headers
- ingest image reference + metadata
- attach personalization profile if allowed

Gates:
- checksum validation; supported format
- permissions vs role + consent scope

### Phase 2 — Pipeline Selection (Evolution + Compliance)
Checklist:
- load pipeline candidates + fitness weights
- apply safety constraints + policy pack
- select pipeline variant

Gates:
- if no compliant pipeline, return **NO_COMPLIANT_PIPELINE**
- record pipeline lineage in audit + telemetry

### Phase 3 — Preprocessing
Checklist:
- execute preprocessing config
- produce intermediate artifacts + metrics

Gates:
- verify resolution/color space vs constraints
- anomaly scan on preprocessing outputs

### Phase 4 — Analysis & Interpretation
Checklist:
- run analysis tasks (segmentation/classification/OCR/etc.)
- generate confidence + explainability notes

Gates:
- schema adherence + anomaly thresholds
- critical anomalies halt delivery and escalate to compliance/security

### Phase 5 — Personalization & Presentation
Checklist:
- format output per role + preferences
- add explanations/learning aids per policy

Gates:
- verify personalization never exceeds consent scope
- fallback to neutral output if personalization blocked

### Phase 6 — Delivery, Audit, Feedback
Checklist:
- package deliverables
- emit audit events + integrity proofs
- collect feedback signals (optional) for evolutionary filtering

Gates:
- **AUDIT_PERSIST_FAILED** blocks delivery
- all delivered artifacts MUST be referenced in audit with integrity hashes

---

## 6) JSON Interface Schemas (Catalog + Definitions)

**Schema version policy:** Schemas are versioned and referenced by stable `$id`. This spec uses JSON Schema **Draft 2020-12** as default; a Draft 7 validator MAY be supported for legacy clients, but the compatibility layer MUST be explicit.

### 6.1 Schema Catalog (v1.1.0)

Governance / Contracts:
- `aurora.instance_id.v1`
- `aurora.contract_envelope.v1`
- `aurora.decision_record.v1`
- `aurora.rollback_pointer.v1`
- `aurora.workflow_dag.v1`
- `aurora.audit_log_entry.v1`
- `aurora.telemetry_event.v1`
- `aurora.error_taxonomy.v1`
- `aurora.policy_pack.v1`
- `aurora.resource_quota.v1`
- `aurora.data_residency_policy.v1`
- `aurora.model_provenance.v1`
- `aurora.preference_memory.v1`

Image Orchestrator Core:
- `aurora.system_metadata.v1`
- `aurora.user_profile.v1`
- `aurora.consent_record.v1`
- `aurora.session_context.v1`
- `aurora.image_input.v1`
- `aurora.preprocessing_config.v1`
- `aurora.evolutionary_filter_config.v1`
- `aurora.personalization_profile.v1`
- `aurora.analysis_request.v1`
- `aurora.analysis_result.v1`
- `aurora.anomaly_report.v1`
- `aurora.validation_report.v1`
- `aurora.workflow_step.v1`
- `aurora.audit_event.v1`
- `aurora.error_response.v1`
- `aurora.model_registry.v1`
- `aurora.integration_adapter.v1`
- `aurora.output_package.v1`

---

### 6.2 Schema Definitions (Draft 2020-12)

#### `aurora.instance_id.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.instance_id.v1",
  "title": "Instance ID",
  "type": "string",
  "format": "uuid"
}
```

#### `aurora.contract_envelope.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.contract_envelope.v1",
  "title": "Contract Envelope",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "instance_id": { "$ref": "aurora.instance_id.v1" },
    "payload": { "type": "object" },
    "metadata": { "type": "object" },
    "decision_context": { "type": "object" },
    "digital_fingerprint": { "type": "object" }
  },
  "required": ["instance_id", "payload", "metadata", "decision_context", "digital_fingerprint"]
}
```

#### `aurora.decision_record.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.decision_record.v1",
  "title": "Decision Record",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "decision_id": { "$ref": "aurora.instance_id.v1" },
    "outcome": { "type": "string", "enum": ["Yes", "No", "Escalate", "Halt"] },
    "timestamp": { "type": "string", "format": "date-time" },
    "policy_pack_version": { "type": "string" },
    "rollback_pointer": { "type": ["string", "null"] }
  },
  "required": ["decision_id", "outcome", "timestamp", "policy_pack_version"]
}
```

#### `aurora.rollback_pointer.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.rollback_pointer.v1",
  "title": "Rollback Pointer",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "prior_state_id": { "$ref": "aurora.instance_id.v1" },
    "reason": { "type": "string" }
  },
  "required": ["prior_state_id"]
}
```

#### `aurora.workflow_dag.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.workflow_dag.v1",
  "title": "Workflow DAG",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "workflow_id": { "$ref": "aurora.instance_id.v1" },
    "nodes": {
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "id": { "$ref": "aurora.instance_id.v1" },
          "type": { "type": "string" },
          "parameters": { "type": "object" }
        },
        "required": ["id", "type"]
      }
    },
    "edges": {
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "from": { "$ref": "aurora.instance_id.v1" },
          "to": { "$ref": "aurora.instance_id.v1" }
        },
        "required": ["from", "to"]
      }
    }
  },
  "required": ["workflow_id", "nodes", "edges"]
}
```

#### `aurora.audit_log_entry.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.audit_log_entry.v1",
  "title": "Audit Log Entry",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "audit_id": { "$ref": "aurora.instance_id.v1" },
    "timestamp": { "type": "string", "format": "date-time" },
    "event_type": { "type": "string" },
    "actor_id": { "$ref": "aurora.instance_id.v1" },
    "target_id": { "type": ["string", "null"] },
    "file_integrity": {
      "type": "object",
      "additionalProperties": false,
      "properties": {
        "algorithm": { "type": "string" },
        "value": { "type": "string" }
      },
      "required": ["algorithm", "value"]
    },
    "schema_version": { "type": "string" }
  },
  "required": ["audit_id", "timestamp", "event_type", "actor_id", "file_integrity", "schema_version"]
}
```

#### `aurora.telemetry_event.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.telemetry_event.v1",
  "title": "Telemetry Event",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "event_id": { "$ref": "aurora.instance_id.v1" },
    "timestamp": { "type": "string", "format": "date-time" },
    "source": { "type": "string" },
    "metrics": { "type": "object" },
    "severity": { "type": "string", "enum": ["INFO", "WARN", "ERROR", "CRITICAL"] }
  },
  "required": ["event_id", "timestamp", "source", "metrics", "severity"]
}
```

#### `aurora.error_taxonomy.v1` (registry payload shape)
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.error_taxonomy.v1",
  "title": "Error Taxonomy Registry",
  "type": "array",
  "items": {
    "type": "object",
    "additionalProperties": false,
    "required": ["code", "severity", "description", "recommended_action"],
    "properties": {
      "code": { "type": "string", "pattern": "^[A-Z0-9_]+$" },
      "severity": { "type": "string", "enum": ["INFO", "WARN", "ERROR", "CRITICAL"] },
      "description": { "type": "string" },
      "recommended_action": { "type": "string" }
    }
  }
}
```

#### `aurora.resource_quota.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.resource_quota.v1",
  "title": "Resource Quota",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "quota_id": { "$ref": "aurora.instance_id.v1" },
    "resource_type": { "type": "string" },
    "limit": { "type": "number" },
    "used": { "type": "number" },
    "unit": { "type": "string" }
  },
  "required": ["quota_id", "resource_type", "limit", "used", "unit"]
}
```

#### `aurora.data_residency_policy.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.data_residency_policy.v1",
  "title": "Data Residency Policy",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "policy_id": { "$ref": "aurora.instance_id.v1" },
    "allowed_regions": { "type": "array", "items": { "type": "string" } },
    "enforced_since": { "type": "string", "format": "date-time" }
  },
  "required": ["policy_id", "allowed_regions", "enforced_since"]
}
```

#### `aurora.policy_pack.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.policy_pack.v1",
  "title": "Policy Pack",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "policy_pack_id": { "$ref": "aurora.instance_id.v1" },
    "version": { "type": "string" },
    "policies": { "type": "array", "items": { "type": "object" } },
    "created_at": { "type": "string", "format": "date-time" }
  },
  "required": ["policy_pack_id", "version", "policies", "created_at"]
}
```

#### `aurora.model_provenance.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.model_provenance.v1",
  "title": "Model Provenance",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "model_id": { "$ref": "aurora.instance_id.v1" },
    "training_data_checksum": { "type": "string" },
    "model_architecture_hash": { "type": "string" },
    "responsible_engineer_id": { "$ref": "aurora.instance_id.v1" },
    "approval_record": {
      "type": "object",
      "additionalProperties": false,
      "properties": {
        "approval_date": { "type": "string", "format": "date-time" },
        "reviewers": { "type": "array", "items": { "$ref": "aurora.instance_id.v1" } }
      },
      "required": ["approval_date", "reviewers"]
    }
  },
  "required": ["model_id", "training_data_checksum", "model_architecture_hash", "responsible_engineer_id", "approval_record"]
}
```

#### `aurora.preference_memory.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.preference_memory.v1",
  "title": "Preference Memory",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "user_id": { "$ref": "aurora.instance_id.v1" },
    "preference": { "type": "string" },
    "timestamp": { "type": "string", "format": "date-time" },
    "ttl": { "type": "integer" },
    "revoked": { "type": "boolean" }
  },
  "required": ["user_id", "preference", "timestamp", "ttl", "revoked"]
}
```

---

### 6.3 Image-Orchestrator Schemas (as in v1.0, upgraded to strict Draft 2020-12)

> Note: These are lifted from v1.0 and upgraded for strictness (`$schema`, `additionalProperties:false`). Keep them as-is unless you have backward-compat constraints.

#### `aurora.system_metadata.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.system_metadata.v1",
  "title": "System Metadata",
  "type": "object",
  "additionalProperties": false,
  "required": ["system_name", "system_version", "build_id", "timestamp"],
  "properties": {
    "system_name": { "type": "string" },
    "system_version": { "type": "string" },
    "build_id": { "type": "string" },
    "timestamp": { "type": "string", "format": "date-time" }
  }
}
```

#### `aurora.user_profile.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.user_profile.v1",
  "title": "User Profile",
  "type": "object",
  "additionalProperties": false,
  "required": ["user_id", "role", "preferences"],
  "properties": {
    "user_id": { "type": "string" },
    "role": { "type": "string", "enum": ["learner", "analyst", "clinician", "admin"] },
    "preferences": { "type": "object" },
    "risk_tolerance": { "type": "string", "enum": ["low", "medium", "high"] }
  }
}
```

#### `aurora.consent_record.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.consent_record.v1",
  "title": "Consent Record",
  "type": "object",
  "additionalProperties": false,
  "required": ["consent_id", "user_id", "scope", "granted_at", "expires_at"],
  "properties": {
    "consent_id": { "type": "string" },
    "user_id": { "type": "string" },
    "scope": { "type": "array", "items": { "type": "string" } },
    "granted_at": { "type": "string", "format": "date-time" },
    "expires_at": { "type": "string", "format": "date-time" },
    "revoked": { "type": "boolean" }
  }
}
```

#### `aurora.session_context.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.session_context.v1",
  "title": "Session Context",
  "type": "object",
  "additionalProperties": false,
  "required": ["session_id", "user_id", "locale", "trace_id"],
  "properties": {
    "session_id": { "type": "string" },
    "user_id": { "type": "string" },
    "locale": { "type": "string" },
    "trace_id": { "type": "string" }
  }
}
```

#### `aurora.image_input.v1` (checksum structured)
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.image_input.v1",
  "title": "Image Input",
  "type": "object",
  "additionalProperties": false,
  "required": ["image_id", "uri", "format", "checksum"],
  "properties": {
    "image_id": { "type": "string" },
    "uri": { "type": "string", "format": "uri" },
    "format": { "type": "string" },
    "checksum": {
      "type": "object",
      "additionalProperties": false,
      "required": ["alg", "value"],
      "properties": {
        "alg": { "type": "string", "enum": ["sha256"] },
        "value": { "type": "string", "pattern": "^[a-fA-F0-9]{64}$" }
      }
    },
    "metadata": { "type": "object" }
  }
}
```

#### `aurora.preprocessing_config.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.preprocessing_config.v1",
  "title": "Preprocessing Config",
  "type": "object",
  "additionalProperties": false,
  "required": ["resize", "normalize", "denoise"],
  "properties": {
    "resize": {
      "type": "object",
      "additionalProperties": false,
      "properties": {
        "width": { "type": "integer" },
        "height": { "type": "integer" }
      }
    },
    "normalize": { "type": "boolean" },
    "denoise": { "type": "boolean" },
    "color_space": { "type": "string" }
  }
}
```

#### `aurora.evolutionary_filter_config.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.evolutionary_filter_config.v1",
  "title": "Evolutionary Filter Config",
  "type": "object",
  "additionalProperties": false,
  "required": ["pipelines", "fitness_weights", "mutation_rules"],
  "properties": {
    "pipelines": { "type": "array", "items": { "type": "object" } },
    "fitness_weights": { "type": "object" },
    "mutation_rules": { "type": "object" },
    "safety_constraints": { "type": "array", "items": { "type": "string" } }
  }
}
```

#### `aurora.personalization_profile.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.personalization_profile.v1",
  "title": "Personalization Profile",
  "type": "object",
  "additionalProperties": false,
  "required": ["user_id", "policies", "updated_at"],
  "properties": {
    "user_id": { "type": "string" },
    "policies": { "type": "array", "items": { "type": "object" } },
    "explanation_level": { "type": "string", "enum": ["brief", "standard", "detailed"] },
    "updated_at": { "type": "string", "format": "date-time" }
  }
}
```

#### `aurora.analysis_request.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.analysis_request.v1",
  "title": "Analysis Request",
  "type": "object",
  "additionalProperties": false,
  "required": ["request_id", "image_id", "task_type", "constraints"],
  "properties": {
    "request_id": { "type": "string" },
    "image_id": { "type": "string" },
    "task_type": { "type": "string" },
    "constraints": { "type": "object" },
    "priority": { "type": "string", "enum": ["low", "normal", "high"] }
  }
}
```

#### `aurora.analysis_result.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.analysis_result.v1",
  "title": "Analysis Result",
  "type": "object",
  "additionalProperties": false,
  "required": ["request_id", "outputs", "confidence", "generated_at"],
  "properties": {
    "request_id": { "type": "string" },
    "outputs": { "type": "array", "items": { "type": "object" } },
    "confidence": { "type": "number" },
    "generated_at": { "type": "string", "format": "date-time" }
  }
}
```

#### `aurora.anomaly_report.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.anomaly_report.v1",
  "title": "Anomaly Report",
  "type": "object",
  "additionalProperties": false,
  "required": ["report_id", "severity", "findings"],
  "properties": {
    "report_id": { "type": "string" },
    "severity": { "type": "string", "enum": ["info", "warning", "critical"] },
    "findings": { "type": "array", "items": { "type": "object" } },
    "recommended_action": { "type": "string" }
  }
}
```

#### `aurora.validation_report.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.validation_report.v1",
  "title": "Validation Report",
  "type": "object",
  "additionalProperties": false,
  "required": ["checks", "passed", "validated_at"],
  "properties": {
    "checks": { "type": "array", "items": { "type": "object" } },
    "passed": { "type": "boolean" },
    "validated_at": { "type": "string", "format": "date-time" }
  }
}
```

#### `aurora.workflow_step.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.workflow_step.v1",
  "title": "Workflow Step",
  "type": "object",
  "additionalProperties": false,
  "required": ["step_id", "name", "status", "inputs", "outputs"],
  "properties": {
    "step_id": { "type": "string" },
    "name": { "type": "string" },
    "status": { "type": "string", "enum": ["pending", "running", "blocked", "completed", "failed"] },
    "inputs": { "type": "array", "items": { "type": "string" } },
    "outputs": { "type": "array", "items": { "type": "string" } },
    "errors": { "type": "array", "items": { "type": "string" } }
  }
}
```

#### `aurora.audit_event.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.audit_event.v1",
  "title": "Audit Event",
  "type": "object",
  "additionalProperties": false,
  "required": ["event_id", "actor", "action", "timestamp"],
  "properties": {
    "event_id": { "type": "string" },
    "actor": { "type": "string" },
    "action": { "type": "string" },
    "timestamp": { "type": "string", "format": "date-time" },
    "details": { "type": "object" }
  }
}
```

#### `aurora.error_response.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.error_response.v1",
  "title": "Error Response",
  "type": "object",
  "additionalProperties": false,
  "required": ["error_id", "code", "message", "severity"],
  "properties": {
    "error_id": { "type": "string" },
    "code": { "type": "string" },
    "message": { "type": "string" },
    "severity": { "type": "string", "enum": ["info", "warning", "critical"] },
    "recoverable": { "type": "boolean" },
    "next_action": { "type": "string" }
  }
}
```

#### `aurora.model_registry.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.model_registry.v1",
  "title": "Model Registry",
  "type": "object",
  "additionalProperties": false,
  "required": ["models", "updated_at"],
  "properties": {
    "models": { "type": "array", "items": { "type": "object" } },
    "updated_at": { "type": "string", "format": "date-time" }
  }
}
```

#### `aurora.integration_adapter.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.integration_adapter.v1",
  "title": "Integration Adapter",
  "type": "object",
  "additionalProperties": false,
  "required": ["adapter_id", "type", "endpoint"],
  "properties": {
    "adapter_id": { "type": "string" },
    "type": { "type": "string" },
    "endpoint": { "type": "string" },
    "auth": { "type": "object" }
  }
}
```

#### `aurora.output_package.v1`
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "aurora.output_package.v1",
  "title": "Output Package",
  "type": "object",
  "additionalProperties": false,
  "required": ["package_id", "request_id", "artifacts", "summary"],
  "properties": {
    "package_id": { "type": "string" },
    "request_id": { "type": "string" },
    "artifacts": { "type": "array", "items": { "type": "object" } },
    "summary": { "type": "object" },
    "delivered_at": { "type": "string", "format": "date-time" }
  }
}
```

---

## 7) Implementation Notes (So it actually runs)

- **Evolution “safe knobs” rule:** mutation is allowed only on thresholds, ordering, or model choice **within allowlists**. Anything affecting consent/retention/redaction is **policy-owned** and MUST NOT be evolvable.
- **Audit-first delivery rule:** the orchestrator MUST block delivery if required audit entries cannot be persisted.
- **Draft compatibility:** if you accept Draft 7 payloads, wrap them with `aurora.contract_envelope.v1` and validate via an explicit `validator_policy` (out of scope here, but recommended as a policy-pack-owned DSL).
- **Readme pointer:** the repository README references a Multi-Agent DAG document; treat it as a companion artifact and keep DAG definitions synchronized with `aurora.workflow_dag.v1`.

---

### Appendix A — Minimal Error Code Set (recommended)
`CONSENT_REQUIRED`, `SCHEMA_VERSION_MISMATCH`, `IMAGE_INTEGRITY_FAILURE`, `NO_COMPLIANT_PIPELINE`, `SCOPE_MISSING`, `PII_RISK_BLOCKED`, `MODEL_POLICY_BLOCKED`, `AUDIT_PERSIST_FAILED`, `HUMAN_REVIEW_REQUIRED`, `RESOURCE_QUOTA_EXCEEDED`, `DATA_RESIDENCY_VIOLATION`, `INPUT_VALIDATION_FAILED`, `MODEL_PROVENANCE_FAILED`, `UNEXPECTED_DEPENDENCY`.

