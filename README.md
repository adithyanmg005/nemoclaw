# NVIDIA NemoClaw Infrastructure & OpenClaw Sandbox Environment
**Reference Stack Deployment & Quickstart Guide**

This repository documents the architecture, system onboarding, and step-by-step installation lifecycle for the NVIDIA NemoClaw reference stack based on the official Quickstart guidelines. The environment securely bridges host-side command orchestrations with an isolated container sandbox to execute tasks without risking configuration drift or host system vulnerability.

---

## 🚀 How It Works (System Architecture)

The system is built on a decoupled, multi-tier architecture ensuring rigorous isolation between the control shell, user interaction layers, and the active container runtime.

### 1. Component Boundaries
* **Host Control CLI (`nemoclaw`):** A command-line environment management tool acting as the host-level proxy for process configurations, credentials mapping, and sandbox orchestration.
* **Management Frontend (`openclaw tui`):** An interactive Terminal User Interface providing developers with live task logging, system health streams, and active execution metrics.
* **Isolated Runtime Sandbox (`OpenShell`):** A hardened containment layer running an immutable execution blueprint. It handles unprivileged process segregation and sandboxed task executions completely separated from the primary machine environment.

### 2. End-to-End Data Pipeline
Whenever an automated task, document generation loop, or code execution is dispatched from the host shell, it follows a strict isolation flow:

```text
[ Workstation Control Terminal ]
                 │
                 ▼ (Invokes proxy command wrapper)
[ NemoClaw Core Orchestration Host ]
                 │
                 ▼ (Secure Pass-Through Sockets)
[ Hardened NVIDIA OpenShell Sandbox Container ]
                 │
                 ▼ (Validates Path Permissions Against Core Rules)
[ Target Destination Path (/tmp/) ] ───> Generates Output Assets Safely
