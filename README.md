# Multimodal Mathematical Reasoning: Papers, Benchmarks, and Methods

A structured, research-problem-oriented collection of papers, benchmarks, and methods for **Multimodal Mathematical Reasoning (MMR)**: reasoning that requires combining visual inputs (diagrams, geometry figures, charts, tables, handwritten math) with text/symbols to solve mathematical problems.
 
Unlike collections organized by publication year or model name, this repo is organized by research problem, following the pipeline:

> **Perception → Representation & Alignment → Reasoning → Learning & Optimization → Evaluation & Reliability → Benchmarks & Datasets → Surveys & Resources**

---

## Contents

- [1. Perception](#1-perception)
- [2. Representation & Alignment](#2-representation--alignment)
- [3. Reasoning](#3-reasoning)
- [4. Learning & Optimization](#4-learning--optimization)
- [5. Evaluation & Reliability](#5-evaluation--reliability)
- [6. Benchmarks & Datasets](#6-benchmarks--datasets)
- [7. Surveys & Resources](#7-surveys--resources)

---

## 1. Perception
 
**Research question:** How does the model extract mathematically relevant information from visual inputs, *before* mathematical reasoning begins?
 
## 1. Perception
 
**Research question:** How does the model extract mathematically relevant information from visual inputs, *before* mathematical reasoning begins?
 
### 1.1 General Visual Encoding
Standard vision-encoder pipelines (ViT/CLIP-style) that feed visual tokens into an MLLM without math-specific adaptation.
- G-LLaVA: Solving Geometric Problem with Multi-Modal Large Language Model (Gao et al., ICLR 2025) [paper](https://openreview.net/forum?id=px1674Wp3C) [code](https://github.com/pipilurj/G-LLaVA)
- Qwen2-VL: Enhancing Vision-Language Model's Perception of the World at Any Resolution (Wang et al., 2024) [paper](https://arxiv.org/abs/2409.12191)
### 1.2 Math-Specific Visual Encoding
Vision encoders pretrained or fine-tuned specifically on mathematical image–caption/diagram pairs, rather than generic natural images.
- MAVIS: Mathematical Visual Instruction Tuning with an Automatic Data Engine (Zhang et al., 2024) [paper](https://arxiv.org/abs/2407.08739) · [code](https://github.com/ZrrSkywalker/MAVIS)
- MathCoder-VL: Bridging Vision and Code for Enhanced Multimodal Mathematical Reasoning (Wang et al., 2025) [paper](https://arxiv.org/abs/2505.10557)
### 1.3 Diagram & Geometry Perception
Recognizing points, lines, circles, angles, tick/equal-length marks, and angle annotations in geometric figures.
- Slow Perception: Let's Perceive Geometric Figures Step-by-step (Wei et al., 2024) [paper](https://arxiv.org/abs/2412.20631) · [code](https://github.com/Ucas-HaoranWei/Slow-Perception)
### 1.4 Chart & Table Perception
Extracting axes, legends, data series, cell values, and table structure from charts/tables.
- Distill Visual Chart Reasoning Ability from LLMs to MLLMs (2024) [paper](https://arxiv.org/abs/2410.18798)
### 1.5 OCR & Mathematical Symbol Recognition
Recognizing handwritten/printed equations, LaTeX-like symbols, and mixed text-math content.
- Uni-MuMER: Unified Multi-Task Fine-Tuning of Vision-Language Model for Handwritten Mathematical Expression Recognition (2025) [paper](https://arxiv.org/abs/2505.23566)
### 1.6 Spatial & Layout Perception
Understanding relative position, alignment, and layout structure (e.g., multi-panel figures, sub-diagrams).
- MathGlance: Multimodal Large Language Models Do Not Know Where to Look in Mathematical Diagrams (2025) [paper](https://arxiv.org/abs/2503.20745)
### 1.7 Active Perception
Iterative "detect uncertain region → crop/zoom → re-perceive" pipelines rather than single-pass encoding.
- ZoomEye: Enhancing Multimodal LLMs with Human-like Zooming Capabilities through Tree-based Image Exploration (Shen et al., EMNLP 2025) [paper](https://arxiv.org/abs/2411.16044)
- V*: Guided Visual Search as a Core Mechanism in Multimodal LLMs (Wu & Xie, CVPR 2024) [paper](https://arxiv.org/abs/2312.14135)
### 1.8 Multi-Agent Perception
Multiple specialized perception modules/agents (e.g., one for OCR, one for geometry) coordinating on a single input.
- Do Multi-Agents Solve Better Than Single? Evaluating Agentic Frameworks for Diagram-Grounded Geometry Problem Solving and Reasoning (2025) [paper](https://arxiv.org/abs/2512.16698)
- TODO (this subcategory is still thin in the math-specific literature; most other multi-agent perception work is in adjacent domains, e.g. chemistry olympiad solving; add more math-specific papers as they appear)

---

## 2. Representation & Alignment

**Research question:** Once visual information is extracted, how should it be *encoded and connected* to text, symbols, or equations so a reasoning system can use it?

> Perception asks *"what is in the image?"* Representation asks *"how do I encode what I saw?"*

### 2.1 Latent Visual Tokens
Implicit representation: image → embeddings consumed directly by an LLM, with no explicit symbolic intermediate.
- TODO

### 2.2 Vision-Language Projection
Learned projector modules mapping visual encoder outputs into the language model's embedding space.
- G-LLaVA — *paper* · *code*

### 2.3 Contrastive Alignment
Aligning visual and textual/mathematical representations via contrastive objectives.
- MAVIS — *paper* · *code*

### 2.4 Region / Symbol Grounding
Explicitly linking visual regions (e.g., a labeled point, an angle mark) to symbolic entities.
- TODO

### 2.5 Scene / Relation Graphs
Representing a diagram as a graph of objects and relations (e.g., point–point, point–line, angle constraints).
- TODO

### 2.6 Symbolic Representations
Explicit symbolic facts extracted from the image, e.g. `AB = AC`, `∠BAC = 40°`.
- TODO

### 2.7 Program / Code Representations
Converting visual content into executable code/DSL calls, e.g. `draw_triangle(A,B,C)`, `set_angle(BAC, 40)`.
- CodePlot-CoT — *paper* · *code*

### 2.8 Layout-Aware Representation
Representations that preserve document/figure layout structure (multi-panel, nested sub-figures).
- TODO

### 2.9 Dynamic / Workspace Representations
Representations that support iterative editing of a visual workspace (e.g., a diagram that gets redrawn/updated during reasoning).
- MathCanvas — *paper* · *code*

---

## 3. Reasoning

**Research question:** Given multimodal evidence, how does the model actually solve the mathematical problem?

### 3.1 Direct Multimodal Reasoning
Single-pass image + question → answer, with no explicit intermediate reasoning trace.
- TODO

### 3.2 Textual Chain-of-Thought
Step-by-step natural-language reasoning conditioned on the image and question.
- Math-LLaVA — *paper* · *code*

### 3.3 Visual Chain-of-Thought
Reasoning that generates and edits intermediate visual artifacts (diagrams) interleaved with text.
- MathCanvas — *paper* · *code*

### 3.4 Program / Code Reasoning
Generating and executing code/equations as part of the reasoning chain, then using the output.
- CodePlot-CoT — *paper* · *code*

### 3.5 Tool-Augmented Reasoning
Calling external tools (calculators, geometry solvers, plotting libraries) during reasoning.
- TODO

### 3.6 Neuro-Symbolic Reasoning
Extracting symbolic facts from perception, then handing off to a theorem prover / geometry engine for derivation.
- TODO

### 3.7 Search-Based Reasoning
Tree/graph search over candidate reasoning paths (e.g., MCTS-style) rather than a single linear chain.
- TODO

### 3.8 Multi-Agent Reasoning
Multiple reasoning agents with different roles (solver, critic, verifier) collaborating on one problem.
- TODO

### 3.9 Multi-Visual / Long-Context Reasoning
Reasoning over multiple images or long documents containing several diagrams/charts.
- MV-MATH — *paper* · *code*

### 3.10 Dynamic Workspace Reasoning
Reasoning that actively modifies a persistent visual workspace across multiple steps.
- MathCanvas — *paper* · *code*

---

## 4. Learning & Optimization

**Research question:** How do we train or post-train models to become better multimodal mathematical reasoners?

> Note: well-established generic training methods (vanilla SFT, PPO) are **not elaborated** here — only entries specific to multimodal mathematical reasoning are listed. Use this section to track *how* a given optimization strategy was adapted for MMR, not to re-explain the base algorithm.

### 4.1 Supervised Fine-Tuning (MMR-specific adaptations)
- G-LLaVA — *paper* · *code*
- Math-LLaVA — *paper* · *code*
- MAVIS (SFT stages) — *paper* · *code*

### 4.2 Contrastive Learning
Used to improve math-specific visual representations prior to/alongside SFT.
- MAVIS — *paper* · *code*

### 4.3 Curriculum Learning
Staged training from easier to harder problems/diagram types.
- TODO

### 4.4 Preference Optimization
DPO-style methods using preferred vs. rejected reasoning traces, adapted for multimodal math.
- MAVIS (DPO-based stage) — *paper* · *code*

### 4.5 Reinforcement Learning with Verifiable Rewards (RLVR) / GRPO
GRPO/RLVR variants adapted for multimodal math, including visual-aware advantage shaping.
- VGPO — *paper* · *code*
- TODO (other GRPO-based MMR papers)

### 4.6 Process-Level Optimization
Training signals derived from intermediate reasoning steps rather than only the final answer.
- TODO

### 4.7 Visual-Aware Optimization
Optimization objectives that explicitly penalize/reward visual grounding, or address "visual forgetting" over long reasoning chains.
- VGPO — *paper* · *code*

### 4.8 Self-Training & Synthetic Data
Data engines / self-generated training data specific to multimodal math.
- MAVIS (data engine) — *paper* · *code*

---

## 5. Evaluation & Reliability

**Research question:** How do we know the model's answer *and* its reasoning are correct, visually grounded, and reliable?

### 5.1 Final-Answer Evaluation
Exact match, numerical tolerance, symbolic equivalence checking.
- TODO

### 5.2 Process Evaluation
Evaluating intermediate reasoning steps, not just the final answer.
- GM-PRM — *paper* · *code*

### 5.3 Visual Grounding Evaluation
Checking whether a claimed relation (e.g., "AB = AC") is actually supported by the image.
- TODO

### 5.4 Visual Reliance & Faithfulness
Testing whether the model is actually using the image (e.g., via image-perturbation experiments) rather than relying on language priors.
- MathVerse — *paper* · *code*
- HC-M3D — *paper* · *code*

### 5.5 Error Detection & Diagnosis
Taxonomies distinguishing perception error, grounding error, representation error, reasoning error, and calculation error.
- TODO

### 5.6 Verification
Outcome verification, re-inference verification, step-level verification, (multimodal) process reward models, atomic visual verification.
- GM-PRM — *paper* · *code*
- TODO (other PRM/verification papers)

### 5.7 Self-Correction
Reflection, re-inference, local step repair, re-perception, re-grounding, backtracking, error-aware correction.
- TODO

### 5.8 Robustness
Robustness to distribution shift, adversarial perturbations, or diagram style/format changes.
- TODO

### 5.9 Calibration & Uncertainty
Confidence calibration and uncertainty estimation for multimodal math reasoning outputs.
- TODO

### 5.10 Test-Time Scaling / Efficiency
Compute-efficient inference-time strategies (sampling, verification budgets) for MMR.
- TODO

---

## 6. Benchmarks & Datasets

Organized **by capability tested**, not by year.

### 6.1 General Multimodal Math
- MathVista — *paper* · *data*
- MathVerse — *paper* · *data*

### 6.2 Geometry
- TODO

### 6.3 Charts & Tables
- TODO

### 6.4 Multi-Visual
- MV-MATH — *paper* · *data*

### 6.5 Visual Reliance
- HC-M3D — *paper* · *data*

### 6.6 Process / Step-Level Reasoning
- We-Math — *paper* · *data*

### 6.7 Verification & Error Detection
- PRMBench-V — *paper* · *data*

### 6.8 Visual Chain-of-Thought
- MIRA — *paper* · *data*

### 6.9 Code / Program Reasoning
- Math-VR — *paper* · *data*

### 6.10 Document / Long-Context Math
- TODO

---

## 7. Surveys & Resources

### 7.1 General Surveys
- TODO

### 7.2 Mathematical Reasoning Surveys (text-only LLMs)
- TODO

### 7.3 Multimodal Reasoning Surveys
- 2026 ACL Survey on Multimodal Mathematical Reasoning — *paper*
  *(Anchor survey for this repo's taxonomy — identifies diagram misinterpretation, symbol-to-visual misalignment, inconsistent reasoning, and insufficient intermediate-step verification as open problems.)*

### 7.4 PRM / Verification Surveys
- TODO

### 7.5 Related GitHub Collections
- TODO

---

<!--
## Citation

If you use this repository in your research, please cite it as:

```bibtex
@misc{mmr-papers-2026,
  title  = {Multimodal Mathematical Reasoning: Papers, Benchmarks, and Methods},
  author = {tongyu0924 and contributors},
  year   = {2026},
  howpublished = {\url{https://github.com/tongyu0924/Multimodal-Mathematical-Reasoning-Papers-Benchmarks-and-Methods}}
}
```
-->
