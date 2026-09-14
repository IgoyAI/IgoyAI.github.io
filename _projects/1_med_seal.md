---
layout: page
title: Med-SEAL
description: A FHIR-native, SEA-LION-powered AI companion for chronic disease care in Southeast Asia.
img: assets/img/med-seal.png
importance: 1
category: research
related_publications: false
---

**Med-SEAL** is a multilingual, FHIR-native AI companion for chronic disease care, built on
[SEA-LION](https://sea-lion.ai/), Singapore's national LLM. It was developed with
NUS, Synapxe, IMDA, and MOH Singapore, and aligned with MOH AIHGIe 2.0 guidelines.

Featured as an [AI Singapore case study](https://sea-lion.ai/case-study/med-seal/).

## The problem

Chronic disease patients in Singapore spend roughly 15 minutes a year with their doctor and
4,300 hours managing their health alone. That gap drives 56% medication non-adherence and an
estimated SGD 2.5B in preventable A&E costs.

## Architecture

Med-SEAL is a Mixture-of-Agents (MoA) medical AI. Every patient interaction is grounded in a
FHIR-native clinical knowledge graph rather than a flat health record. Three specialist agents
run in parallel:

- **Multilingual reasoning agent** (SEA-LION-v4) handles conversation in English, Mandarin, Malay, or Tamil
- **Medical reasoning agent** (Med-SEAL-V1, an adversarially-trained clinical VLM) checks drug interactions and clinical logic
- **Knowledge graph retriever** pulls real conditions, medications, and lab trends from the EMR

A SEA-LION aggregator resolves conflicts, enforces safety policy, and returns a single grounded
answer. A SEA-Guard safety layer wraps both input and output.

## Key components

- Companion mobile app: 24/7 chat, medication tracker, vitals dashboard, appointment booking, and culturally aware dietary coaching (hawker food, festive meals)
- 7-section pre-visit brief auto-generated 24 hours before each appointment, giving clinicians 30 days of adherence, biometric, and patient-reported outcome data
- Tiered nudge engine: gentle reminders for missed doses, next-day clinician flags for concerning trends, immediate alerts for dangerous readings
- FHIR R4 integration with OpenEMR, Medplum, and Epic on FHIR

## Results

Med-SEAL-V1 is the first medical VLM in Southeast Asia to combine adversarial training during
GRPO reinforcement learning with certified robustness guarantees via randomized smoothing.

| Dimension | Result |
| :--- | :--- |
| Adversarial robustness | 0.74% attack success rate on OmniMedVQA under PGD-20, 40x lower than the next-best medical VLM |
| Red-teaming | Zero breaches across 230 attack scenarios: AI Verify 2.0 (11/11), Microsoft PyRIT (26/26 OWASP), NVIDIA Garak (33/33) |
| Quality (DeepEval v3.9.6) | 0.986 faithfulness, 0.940 answer relevancy, 0.933 clinical safety; zero bias, zero toxicity |

## My role

I led the AI architecture and trustworthy-AI evaluation. My research on adversarial robustness
and certified defenses for vision-language models forms the technical backbone of Med-SEAL-V1.
