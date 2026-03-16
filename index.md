---
title: "Guidelines for Developers and QA Teams"
layout: single
permalink: /
sidebar:
  nav: "guidelines"
---

This page complements the paper [*"Runtime Verification and Field-based Testing for ROS-Based Robotic Systems"*](https://doi.org/10.1109/TSE.2024.3444697) and is an online repository of the guideline catalog for ROS-based Robotics projects.

You can further find the [guidelines](/) and information on the [evaluation](/paper#evaluation) process. Reproduction kits, specifications, and accompanying code can be found in our [replication package](/paper#replication-package).

<div style="border: 1px solid #ddd; border-radius: 6px; padding: 20px 24px; margin: 24px 0; background-color: #f9f9f9;">
  <h2 id="whats-new" style="margin-top: 0;">What's New</h2>
  <ul style="list-style: none; padding-left: 0;">
    <li style="margin-bottom: 10px;"><strong>March 2026</strong> — New exemplar added: UPPAAL automated verification toolchain for ROS 2 timing and scheduling analysis (<a href="/guidelines/guideline-pe2">PE2</a>).</li>
    <li style="margin-bottom: 10px;"><strong>March 2026</strong> — New exemplars added: R2D2 and ROFER ROS 2 fuzzers for noise injection and robustness testing (<a href="/guidelines/guideline-mta1">MTA1</a>).</li>
    <li style="margin-bottom: 10px;"><strong>March 2026</strong> — New exemplars added: FRET for structured natural language specification (<a href="/guidelines/guideline-sdb1">SDB1</a>) and the FRET+Ogma+Copilot automated monitor generation pipeline (<a href="/guidelines/guideline-mta2">MTA2</a>).</li>
  </ul>
</div>

## Guideline Catalog

![Development and Test Process](/files/dev_test_process.png)

## Guidelines
{: #patternsref}

### Constraint Identification

- [**CI1** — Identify timing constraints](/guidelines/guideline-ci1)
- [**CI2** — Identify security and privacy constraints](/guidelines/guideline-ci2)
- [**CI3** — Identify safety constraints](/guidelines/guideline-ci3)

### Code Design and Implementation

- [**CD1** — Strive for ROS nodes with single responsibility](/guidelines/guideline-cd1)
- [**CD2** — Ensure global time monotonicity of events and states](/guidelines/guideline-cd2)

### Instrumentation

- [**I1** — Provide an API for querying and updating internal lifecycle](/guidelines/guideline-i1)
- [**I2** — Provide an API for logging and filtering](/guidelines/guideline-i2)
- [**I3** — Provide an API for injecting faults in execution scenarios](/guidelines/guideline-i3)
- [**I4** — Isolate components for testing](/guidelines/guideline-i4)

### Prepare Execution Environment

- [**PE1** — Understand the overhead acceptance criteria](/guidelines/guideline-pe1)
- [**PE2** — Create models for runtime assessment](/guidelines/guideline-pe2)

### Specify (Un)desired Behavior

- [**SDB1** — Define properties using a logic-based language](/guidelines/guideline-sdb1)
- [**SDB2** — Use Domain Specific Languages (DSLs) to specify properties](/guidelines/guideline-sdb2)
- [**SDB3** — Use languages and tools to scenario-based specification of test cases](/guidelines/guideline-sdb3)

### Monitor and Test Automation

- [**MTA1** — Improve the robustness of the system by performing noise and fault injection](/guidelines/guideline-mta1)
- [**MTA2** — Exploit automation for test case generation, test case prioritization and selection, oracle and monitor generation](/guidelines/guideline-mta2)

### System Execution

- [**SE1** — Use record-and-replay when performing exploratory field tests](/guidelines/guideline-se1)
- [**SE2** — No GUIs! Prioritize headless simulation](/guidelines/guideline-se2)

### Analysis and Reporting

- [**AR1** — Perform postmortem analysis to diagnose non-passing test cases](/guidelines/guideline-ar1)
- [**AR2** — Use reliable tooling in order to manage field data](/guidelines/guideline-ar2)
