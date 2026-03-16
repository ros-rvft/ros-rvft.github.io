---
title: "Guidelines for Developers and QA Teams"
layout: single
permalink: /
classes: wide
sidebar:
  nav: "guidelines"
---

This page complements the paper [*"Runtime Verification and Field-based Testing for ROS-Based Robotic Systems"*](https://doi.org/10.1109/TSE.2024.3444697) and is an online repository of the guideline catalog for ROS-based Robotics projects.

You can further find the [guidelines](/) and information on the [evaluation](/paper#evaluation) process. Reproduction kits, specifications, and accompanying code can be found in our [replication package](/paper#replication-package).

## What's New
{: #whats-new}

* **March 2026** — New exemplar added: UPPAAL automated verification toolchain for ROS 2 ([PE2](/guidelines/guideline-pe2)).
* **March 2026** — New exemplars: R2D2 and ROFER ROS 2 fuzzers ([MTA1](/guidelines/guideline-mta1)).
* **March 2026** — New exemplars: FRET ([SDB1](/guidelines/guideline-sdb1)) and FRET+Ogma+Copilot pipeline ([MTA2](/guidelines/guideline-mta2)).

[View all news →](/news)

## Browse by Role

<div style="display: flex; gap: 20px; margin: 20px 0; flex-wrap: wrap;">
  <div style="flex: 1; min-width: 260px; border: 1px solid #ddd; border-radius: 6px; padding: 16px;">
    <h3 style="margin-top: 0;">For Developers</h3>
    <p>Guidelines for preparing ROS-based systems for verification and testing.</p>
    <ul>
      <li><a href="/guidelines/guideline-ci1">CI1–CI3</a> — Constraint Identification</li>
      <li><a href="/guidelines/guideline-cd1">CD1–CD2</a> — Code Design</li>
      <li><a href="/guidelines/guideline-i1">I1–I4</a> — Instrumentation</li>
    </ul>
  </div>
  <div style="flex: 1; min-width: 260px; border: 1px solid #ddd; border-radius: 6px; padding: 16px;">
    <h3 style="margin-top: 0;">For QA Teams</h3>
    <p>Guidelines for performing runtime verification and field-based testing.</p>
    <ul>
      <li><a href="/guidelines/guideline-pe1">PE1–PE2</a> — Prepare Environment</li>
      <li><a href="/guidelines/guideline-sdb1">SDB1–SDB3</a> — Specify Behavior</li>
      <li><a href="/guidelines/guideline-mta1">MTA1–MTA2</a> — Monitor & Test</li>
      <li><a href="/guidelines/guideline-se1">SE1–SE2</a> — System Execution</li>
      <li><a href="/guidelines/guideline-ar1">AR1–AR2</a> — Analysis & Reporting</li>
    </ul>
  </div>
</div>

## Guideline Catalog

<img src="/files/dev_test_process.png" alt="Development and Test Process" style="width: 100%; max-width: 100%;">

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
