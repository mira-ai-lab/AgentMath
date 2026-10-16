# 📐 MAMath-Bench: Process-Aware and Robust Evaluation of Multimodal Multi-Agent Mathematical Reasoning
[🇨🇳 中文版](Readme_CN.md)

MAMath-Bench is a multimodal mathematical reasoning benchmark designed to systematically evaluate multi-agent systems from both **outcome-oriented** and **process-oriented** perspectives.

Unlike conventional mathematical reasoning benchmarks that primarily focus on final-answer accuracy, MAMath-Bench incorporates **step-by-step reasoning milestones** and **adversarial negative samples** to evaluate whether multi-agent systems can correctly solve multimodal mathematical problems, maintain reliable reasoning processes, and identify reasoning errors.

[![Data Scale](https://img.shields.io/badge/Samples-1003-orange.svg)](#dataset-statistics)
[![Modalities](https://img.shields.io/badge/Modalities-4-purple.svg)](#key-features)

---

## 💡 Overview

Existing mathematical reasoning evaluations mainly focus on whether a model produces the correct final answer. However, such evaluations provide limited insight into the reliability of the intermediate reasoning process, especially when multiple agents collaborate to solve complex multimodal problems.

MAMath-Bench is designed to address three key challenges:

- **Limited modality coverage**: Traditional mathematical reasoning benchmarks are predominantly text-based and provide limited evaluation of multimodal reasoning.
- **Outcome-oriented evaluation**: Final-answer accuracy alone cannot reveal whether a system follows a complete and logically valid reasoning process.
- **Collaboration vulnerability**: Multi-agent systems may propagate incorrect, redundant, repeated, missing, or incorrectly ordered reasoning steps during collaboration.

To address these challenges, MAMath-Bench contains **1,003 samples** covering text, image, audio, and hybrid multimodal inputs. The benchmark introduces **step-by-step reasoning milestones** and **adversarial negative samples**, enabling a systematic evaluation of multimodal understanding, mathematical reasoning, process reliability, and error detection.

---

## 🚀 Key Contributions

1. **Multimodal Reasoning**  
   MAMath-Bench covers four input configurations involving text, image, audio, and image-text combinations, enabling evaluation of multimodal mathematical reasoning capabilities.

2. **Process-Aware Evaluation**  
   We provide reasoning milestones for **800 positive samples**, allowing systems to be evaluated at the level of individual key reasoning steps rather than only on final answers.

3. **Adversarial Robustness Benchmark**  
   We construct **203 negative samples** covering five types of reasoning defects to evaluate whether multi-agent systems can detect and respond to erroneous reasoning.

4. **Progressive Difficulty Design**  
   The benchmark ranges from basic arithmetic to competition-level mathematical reasoning, with reasoning chains containing up to **20 steps**.

---

## 🔍 Benchmark Design

### 1. Multidimensional Coverage

MAMath-Bench organizes samples according to modality and reasoning difficulty:

- **Easy (1–3 steps)**: Text-only problems, mainly involving basic calculations and simple applications.
- **Medium (4–6 steps)**: Image-text problems requiring multi-step logical transformations and multimodal information integration.
- **Hard (6–20 steps)**: Image- and audio-containing problems involving competition-level mathematical reasoning.

### 2. Adversarial Robustness

To evaluate whether multi-agent systems can identify errors rather than blindly follow intermediate reasoning, we construct **203 adversarial negative samples** covering five types of reasoning defects:

- **Wrong Steps**: Introduce errors in numerical calculations or logical derivations.
- **Redundant Steps**: Introduce unnecessary reasoning steps that do not contribute to solving the problem.
- **Repeated Steps**: Introduce repeated reasoning steps to test whether systems can identify unnecessary repetition.
- **Missing Steps**: Remove essential reasoning steps to create gaps in the reasoning chain.
- **Swapped Steps**: Exchange the order of reasoning steps, creating inconsistencies between prerequisite conditions and subsequent conclusions.

These adversarial samples are designed to preserve the original problem context while introducing identifiable defects into otherwise valid reasoning processes.

---

## 📊 Dataset Statistics

### Dataset Distribution

| Category | Details | Count / Proportion |
| :--- | :--- | :--- |
| **Total Samples** | Total Samples | **1,003** |
| **Reasoning Type** | Positive / Negative | **800 / 203** |
| **Difficulty** | Easy / Medium / Hard | **200 / 300 / 300 (Positive)** |
| **Modalities** | Text, Image, Image-Text, Audio | **4 configurations** |
| **Domains** | Algebra, Geometry, Number Theory, etc. | **11 domains** |

### Negative Sample Distribution

| Defect Type | Samples | Proportion |
| :--- | ---: | ---: |
| Wrong Steps | 83 | 40.9% |
| Redundant Steps | 30 | 14.8% |
| Repeated Steps | 30 | 14.8% |
| Missing Steps | 30 | 14.8% |
| Swapped Steps | 30 | 14.8% |

---

## 📂 Data Structure

```text
MAMath-Bench/
├── data/
│   ├── positive.json       # Positive samples with milestone annotations
│   ├── negative.json       # Adversarial negative samples
│   ├── img/                # Geometric figures, handwritten formulas, and charts
│   └── audio/              # Audio recordings of problem statements
└── README.md
