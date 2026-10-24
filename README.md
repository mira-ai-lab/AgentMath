# 📐 MAMath-Bench: Process-Aware and Robust Evaluation of Multimodal Multi-Agent Mathematical Reasoning

<p align="center">
  <a href="README.md">🇬🇧 English</a> |
  <a href="README_CN.md">🇨🇳 中文</a>
</p>

[![Data Scale](https://img.shields.io/badge/Samples-1003-orange.svg)](#dataset-statistics)
[![Modalities](https://img.shields.io/badge/Modalities-4-purple.svg)](#benchmark-design)

---

## 💡 Overview

MAMath-Bench is a multimodal mathematical reasoning benchmark designed
for the educational domain. Existing mathematical reasoning evaluations
in education mainly face three challenges: **limited modality coverage**,
**outcome-oriented evaluation**, and **collaboration vulnerability**.

To address these limitations, MAMath-Bench provides **1,003 high-quality
samples** with multimodal inputs, including text, images, and audio. It
further introduces **step-by-step reasoning milestones** and
**adversarial negative samples** to comprehensively evaluate information
alignment, logical reasoning, and error recovery capabilities in
multi-agent collaboration.

---

## 🚀 Key Contributions

1. **Multimodal Reasoning Paradigm**: Extends conventional text-only
   mathematical reasoning evaluation to four input configurations
   involving text, images, audio, and image-text combinations, covering
   realistic educational and research scenarios.

2. **Fine-Grained Process-Oriented Evaluation**: Provides logical
   milestone annotations for **800 positive samples**, enabling evaluation
   of each key step in an agent's reasoning chain rather than only its
   final answer.

3. **Adversarial Robustness Benchmark**: Constructs a negative sample
   collection containing **five types of logical defects**, specifically
   designed to evaluate whether multi-agent systems can detect, diagnose,
   and correct erroneous premises or reasoning traps.

4. **Progressive Difficulty Design**: Covers problems ranging from basic
   arithmetic to International Mathematical Olympiad (IMO)-level
   reasoning, with reasoning chains containing up to **20 steps**.

<div align="center">
  <img src="images/frame.png" width="100%" alt="Overview of MAMath-Bench">
  <p>Figure 1: Overview of the MAMath-Bench construction process.</p>
</div>

---

## 🔍 Benchmark Design

### 1. Multidimensional Coverage

MAMath-Bench organizes samples according to modality and difficulty to
evaluate the multimodal processing and mathematical reasoning
capabilities of multi-agent systems:

- **Easy (1–3 steps)**: Text-only problems, mainly involving basic
  arithmetic and simple application problems.
- **Medium (4–6 steps)**: Image-text problems requiring multi-step logical
  transformations and multimodal information integration.
- **Hard (6–20 steps)**: Problems involving images and audio, designed
  for competition-level complex reasoning.

<div align="center">
  <img src="images/pos.png" width="100%" alt="Example of positive samples">
  <p>Figure 2: Examples of positive samples.</p>
</div>

### 2. Adversarial Negative Samples

To address the common phenomenon of **blindly following** erroneous
reasoning in multi-agent collaboration, we construct **203 negative
samples** covering five types of logical defects:

- **Wrong Steps**: Errors in numerical calculations or logical
  derivations.
- **Redundant Steps**: Unnecessary reasoning steps that do not contribute
  to solving the problem, testing reasoning conciseness.
- **Repeated Steps**: Repeated reasoning steps that introduce unnecessary
  repetition into the reasoning chain.
- **Missing Steps**: Missing essential reasoning steps that create logical
  gaps in the reasoning chain.
- **Swapped Steps**: Incorrectly reordered reasoning steps that disrupt
  the dependency between prerequisites and conclusions.

<div align="center">
  <img src="images/neg.png" width="100%" alt="Examples of adversarial negative samples">
  <p>Figure 3: Examples of adversarial negative samples.</p>
</div>

---

## 📊 Dataset Statistics

<div align="center">
  <a href="images/fig11.pdf" target="_blank">
    <img src="images/fig11.png" width="50%" alt="Distribution of difficulty, modalities, and reasoning-step complexity">
  </a>
  <p>Figure 4: Distribution of difficulty, modalities, and reasoning-step complexity.</p>
</div>

### Dataset Distribution Overview

| Category | Details | Number / Proportion |
| :--- | :--- | :--- |
| **Total Samples** | Total Samples | **1,003** |
| **Reasoning Type** | Positive / Negative (Adversarial) | **800 / 203** |
| **Difficulty Distribution** | Easy / Medium / Hard | **200 / 300 / 300 (Positive)** |
| **Modality Distribution** | Text, Image, Image-Text, Audio | **4 configurations** |
| **Domain Coverage** | Algebra, Geometry, Number Theory, etc. | **11 domains** |

### Negative Sample Analysis

**Wrong Steps** account for the largest proportion of the negative
samples.

| Defect Type | Number of Samples | Proportion |
| :--- | ---: | ---: |
| Wrong Steps | 83 | 40.9% |
| Redundant Steps | 30 | 14.8% |
| Repeated Steps | 30 | 14.8% |
| Missing Steps | 30 | 14.8% |
| Swapped Steps | 30 | 14.8% |

---

## 📂 Data Structure and Format

### Directory Structure

```text
MAMath-Bench/
├── data/
│   ├── positive.json       # Positive samples with milestone annotations
│   ├── negative.json       # Adversarial negative samples
│   ├── img/                # Geometric figures, handwritten formulas, and charts
│   └── audio/              # Audio recordings of problem statements
└── README.md
```

### Example Entry
```json
{
  "id": 1,
  "modality": "image-text",
  "image": "img/geometry_001.png",
  "audio": "null",
  "type": "Geometry",
  "difficulty": "medium",
  "problem": "Calculate the area of the shaded region in the provided image.",
  "final_answer": "12.5",
  "milestones_number": 2,
  "milestones_0": [
    {
      "image_recognition_info": "A circle with radius 5 inscribed in a square.",
      "audio_recognition_info": "null",
      "step_1": "Calculate the area of the square: 5 * 2 = 10; 10^2 = 100.",
      "step_2": "Calculate the area of the circle: π * 5^2 = 25π.",
      "step_3": "The shaded area is the difference..."
    }
  ],
  "milestones_1": [
    {
      "description": "An alternative valid solution with the same parameters."
    }
  ]
}
```

---

# 🏆 Evaluation Protocol
MAMath-Bench evaluates multi-agent systems from two complementary
perspectives: outcome-oriented evaluation and process-oriented
evaluation.
### 📊 Outcome-Oriented Evaluation
1. ✅ **Execution Success Rate**
Measures the proportion of problems that a system successfully executes:
\[
\text{Execution Success Rate}
=
\frac{\text{Number of Successfully Executed Problems}}
{\text{Total Number of Problems}}.
\]
This metric considers whether a problem is successfully executed rather
than treating execution failures or non-terminating discussions as
successful outcomes.
2. 📐 **Final Answer Accuracy**
Measures the proportion of problems for which the final answer is
correct. Numerical equality, equivalent algebraic expressions, and
acceptable numerical tolerances are considered when determining
correctness.
### 🔁 Process-Oriented Evaluation
1. 📝 **Milestone Accuracy**
Measures the proportion of reference milestones that are correctly
matched by the predicted reasoning process:
\[
\text{Milestone Accuracy}
=
\frac{\text{Correctly Matched Milestones}}
{\text{Total Reference Milestones}}.
\]
A milestone is considered correct when the corresponding reasoning step
satisfies the required numerical consistency, algebraic equivalence, or
acceptable numerical tolerance.
2. 🤝 **Task Allocation Quality**
Evaluates whether the reasoning process is complete, maintains correct
dependencies, and follows an appropriate step order. It includes two
specific metrics:
- Step Redundancy Rate:
\[
\text{Step Redundancy Rate}
=
\frac{\text{Redundant Steps}}
{\text{Total Predicted Steps}}.
\]
- Step Missing Rate:
\[
\text{Step Missing Rate}
=
\frac{\text{Missing Steps}}
{\text{Total Reference Steps}}.
\]
3. 🔧 **Error Detection**
Evaluates whether a system can identify reasoning errors during the
problem-solving process. The evaluation covers five types of reasoning
defects:
- Wrong Steps
- Redundant Steps
- Repeated Steps
- Missing Steps
- Swapped Steps
🔍 The error detection rate is calculated as:
\[
\text{Error Detection Rate}
=
\frac{\text{Detected Errors}}
{\text{Total Errors}}.
\]

---

## 📥 Download
Clone the GitHub repository to obtain the benchmark data and associated
resources:
```
git clone https://github.com/mira-ai-lab/AgentMath.git
cd AgentMath
```

## 📄 License

MAMath-Bench is released under the MIT License.

Please note that some materials included in MAMath-Bench are derived from
existing datasets and remain subject to the licenses and terms of their
respective source datasets. Users are responsible for complying with the
applicable licenses and terms of use of the original datasets.
For the full license terms, please see the LICENSE file.
