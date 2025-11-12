# Local-Persistence

# Effectiveness of Local Persistence (Illustration)
**Summary**

Local persistence mechanisms help an actor survive reboots, maintain access, and re-establish capabilities after interruptions. From a defensive perspective, persistence is important because it increases dwell time, complicates cleanup, and often leaves detectable artifacts — making it both an adversary advantage and a defender opportunity.

This repository includes various custom ways and my Proof-Of-Concepts walkthroughs on how persistence can be implimented in the wild  

---

## Typical Goal & High-level Scenario
**Goal:** Maintain re-entry foothold on a host across restarts and user sessions.  
**Scenario:** An agent obtains an initial foothold (phishing, exploit, or benign admin misconfig). The operator then ensures the agent restarts on boot or login so it can resume activity without repeating the initial intrusion steps.

---

## Why Local Persistence is Effective
- **Survives routine restarts** — avoids repeated exploitation for re-entry.
- **Low operational cost** — once established, requires minimal interaction.
- **Increases dwell time** — extended presence raises the chance of lateral movement and data access.
- **Subtle artifacts** — many persistence artifacts blend with legitimate startup tasks, increasing detection difficulty.

---

## Defensive Indicators
- Unexpected entries in startup/configuration lists for rarely-used users or services.
- New scheduled tasks with unusual owners or nonstandard command lines.
- Recently modified binaries in system directories or unusual file metadata timestamps.
- New or outbound network connections immediately after system boot/login.
- Repeated process executions tied to a single user session across reboots.

---

## Detection & Mitigation Checklist 
- Monitor and alert on additions/changes to startup configuration locations.
- Track file modification and creation events in system and program directories.
- Compare startup items against baseline inventories and known-good lists.
- Enforce least privilege for service accounts and restrict local admin use.
- Use endpoint integrity checks and boot-time telemetry to detect reactivation patterns.

---

## Visual flow 
```mermaid
flowchart LR
  A[Initial Foothold] --> B[Establish Local Persistence]
  B --> C[Survives Reboot / Login]
  C --> D[Resume Malicious Activity]
  D --> E[Lateral Movement / Data Access]
  E --> F[Increased Dwell Time]
  F --> G[Higher Detection Opportunity]
  style G fill:#f9f,stroke:#333,stroke-width:1px
