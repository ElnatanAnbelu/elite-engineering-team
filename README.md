# Elite-Engineering-Team : Multi-Agent LLM Orchestration

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT) [![AI Orchestration](https://img.shields.io/badge/AI-Orchestration-purple)]() [![Claude](https://img.shields.io/badge/Anthropic-Claude-orange)]()

> **A deterministic framework for coordinating specialized, autonomous AI agents across the software development lifecycle.**

This repository contains the architectural prompts, contextual boundary rules, and system instructions required to simulate a fully-staffed, elite engineering department. It moves beyond standard "code generation" into systematic, multi-agent collaboration—enforcing rigorous security reviews, architectural decision records (ADRs), and QA testing protocols before code is ever merged.

## 🚀 System Architecture

- **Contextual Boundary Enforcement:** Each agent persona (e.g., `appsec`, `cloud-architect`, `tech-lead`) operates within strict operational bounds, preventing LLM hallucination and scope creep.
- **Deterministic Prompt Chaining:** Outputs from the `tech-lead` agent are algorithmically parsed and piped into the `swe-fe` and `swe-be` execution agents.
- **Autonomous Synthesis:** Continuous feedback loops where the `qa-engineer` agent independently critiques and requests refactors from execution agents.

## ✨ Core Framework Features

- **🧠 20+ Specialized Personas:** Highly tuned system prompts for specific engineering disciplines (DevOps, SRE, MLOPs, UX/UI).
- **🏗️ ELITE_STANDARDS Protocol:** A mandatory ruleset that forces AI models to write modular, DRY, and highly secure code rather than boilerplate scripts.
- **🛡️ Automated Threat Modeling:** Integrated Security Operations (SecOps) prompts that proactively scan generated architectures for CVE vulnerabilities.

---
*Architected by [Elnatan Anbelu](https://github.com/ElnatanAnbelu).*
