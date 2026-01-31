# Multi-Agent-DAG (SSOT) – Abgleich mit `aurora.workflow_dag.v1` (v1.2.0)

Dieses Dokument ist die menschenlesbare Referenz fuer das aktuelle Multi-Agent-Workflow-Layout des **AURORA Adaptive Image Orchestrator**.

## 1) Normativer Status

- **Quelle der Wahrheit:** Das JSON-DAG-Artefakt (z. B. `workflow.json`) ist die technische Source of Truth.
- **Schema:** Das Artefakt MUSS gegen `aurora.workflow_dag.v1` validieren.
- **Version:** Das Feld `version` MUSS `v1.2.0` sein (SemVer).
- **Dok-Sync:** Dieses Dokument MUSS die aktuelle DAG-Struktur widerspiegeln. Bei Abweichung gilt das JSON-Artefakt.

## 2) Beispiel: Contract Envelope + Workflow DAG (v1.2.0)

Hinweis: Das Envelope-Format ist optional fuer reine Repo-Dateien, aber verpflichtend an Tool/API-Grenzen.

```json
{
  "type": "aurora.workflow_dag.v1",
  "version": "v1.2.0",
  "timestamp": "2026-01-29T00:00:00Z",
  "trace": { "trace_id": "trace_12345678" },
  "actor": { "actor_type": "service_account", "actor_id": "aurora-ci", "role": "doc-sync" },
  "payload": {
    "dag_id": "aurora.image.orchestrator.main",
    "version": "v1.2.0",
    "entrypoint": "intake",
    "nodes": [
      { "node_id": "intake", "node_type": "intake", "contract_ref": "aurora.analysis_request.v1" },
      { "node_id": "ingest", "node_type": "ingest", "contract_ref": "aurora.image_input.v1" },
      { "node_id": "preprocess", "node_type": "preprocess", "contract_ref": "aurora.preprocessing_config.v1" },
      { "node_id": "analyze", "node_type": "analyze", "contract_ref": "aurora.analysis_result.v1" },
      { "node_id": "decide", "node_type": "decide", "contract_ref": "aurora.decision_record.v1" },
      { "node_id": "personalize", "node_type": "personalize", "contract_ref": "aurora.personalization_profile.v1" },
      { "node_id": "deliver", "node_type": "deliver", "contract_ref": "aurora.output_package.v1" },
      { "node_id": "learn", "node_type": "learn", "contract_ref": "aurora.evolutionary_filter_config.v1" },
      { "node_id": "audit", "node_type": "audit", "contract_ref": "aurora.audit_log_entry.v1" }
    ],
    "edges": [
      { "from": "intake", "to": "ingest" },
      { "from": "ingest", "to": "preprocess" },
      { "from": "preprocess", "to": "analyze" },
      { "from": "analyze", "to": "decide" },
      { "from": "decide", "to": "personalize", "condition": "decision.outcome == 'Continue'" },
      { "from": "personalize", "to": "audit" },
      { "from": "audit", "to": "deliver" },
      { "from": "deliver", "to": "learn" }
    ]
  }
}
```

## 3) Synchronisationsprozess (Repo-Workflow)

1. Aenderung am DAG-JSON (z. B. neuer Node, neue Edge, Gate-Logik).
2. Schema-Validierung gegen `aurora.workflow_dag.v1` und `version=v1.2.0`.
3. Dokumentations-Generierung (z. B. `generate_docs.sh` oder CI-Job).
4. README-Link pruefen/aktualisieren (nur ein kanonischer Pfad).
5. Diff-Review: Aenderungen am DAG muessen im Changelog/Release-Notes erkennbar sein.

## 4) Minimaler Gate-Check (empfohlen)

- DAG validiert (Schema + SemVer)
- entrypoint existiert als Node
- keine unaufloesbaren Edges (from/to muessen existieren)
- consent/policy checks sind als Gates im DAG (oder in `contract_ref` der Decide/Audit Nodes) abbildbar
- Audit-First: Delivery nur nach erfolgreicher Audit-Emission
