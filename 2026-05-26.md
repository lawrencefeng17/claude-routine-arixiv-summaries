# arXiv cs.LG Highlights — May 26, 2026

*Topics: machine learning, language models, AI safety & alignment, interpretability, training dynamics, generalization*

---

## Top 10 Papers

### 1. Polymorphism Is Rotation: Operational Mechanistic Interpretability from a Two-Layer Transformer to Pythia-70m
**arXiv:2605.24577** | Jordan F. McCann

Independently trained transformers compute the same functions but in residual-stream bases that differ by a uniform random rotation in SO(d_model). This has been hiding a critical failure in SAE universality metrics: decoder columns align at ~98% similarity while reconstruction performance is *negative*, because researchers are comparing features across mismatched coordinate systems.

- A single orthogonal Procrustes fit recovers near-optimal SAE reconstruction and enables steering vector transfer between independently trained models
- The rotation matrix R follows the Haar distribution, confirmed to 0.1% precision
- Steering transfer behavior (clean / partial / inverted) depends on alignment with R's invariant subspace
- Validated on a 104k-parameter Dyck-3 transformer and nine Pythia-70m seeds

---

### 2. The Concept Allocation Zone: Tracking How Concepts Form Across Transformer Depth
**arXiv:2605.24856** | James Henry

Concept formation in transformer LMs is not a single-layer event — it unfolds across a contiguous depth interval. This paper formalizes the *Concept Allocation Zone* (CAZ): the depth region where a concept becomes measurably separable, characterized by three metrics (Separation, Concept Coherence, Concept Velocity).

- Tested across 34 models from 8 architectural families; "gentle CAZes" are causally active in 93–100% of ablation cases
- Single concepts can participate in multiple CAZes; multiple concepts may share one zone
- Separation curves are frequently multimodal, arguing against single-layer probing
- Cross-architecture alignment occurs as depth-matched, not monolithic

---

### 3. Continuous-Depth Field Theory for Transformer Patching and Mechanistic Interpretability
**arXiv:2605.25225** | David N. Olivieri, Antonio F. Pérez Rodríguez

A field-theoretic framework for mechanistic interpretability: treats the residual stream as a depth-token field and re-casts patching as localized source insertion, patch effects as sensitivity-field predictions, and downstream propagation as empirical Green-function response.

- Identifies a bounded local linear regime where patch effects are predictable from first-order sensitivities
- Measures structured anisotropic propagation patterns across depth and token positions
- Provides a unified mathematical language (sensitivities, propagated fields, Green-operator slices) for patching experiments and patch-site inference

---

### 4. Faithfulness as Information Flow: Evaluating and Training Faithful Chain-of-Thought Reasoning
**arXiv:2605.24286** | Jinghan Jia et al.

Models can bypass CoT entirely via prompt-to-answer shortcuts, making explanations plausible but unfaithful. This paper frames CoT faithfulness as an information-flow problem: faithful reasoning should route answer-relevant information through the CoT path, not a direct shortcut.

- Three complementary diagnostics (sufficiency, completeness, necessity) instantiated via entropy-based, masked-KL, and gradient-based measures
- Training interventions — attention masking, gradient masking, adversarial perturbations — encourage proper information routing during RL fine-tuning
- Demonstrates improvements across arithmetic, code repair, and math tasks; reduces hint-injection susceptibility

---

### 5. From Simulation to Enaction: Post-trained Language Models Recognize and React to Their Own Generations
**arXiv:2605.25459** | Asvin G., Jack Lindsey

Post-training creates a structural shift: models can recognize whether they are generating on-policy or off-policy text. On-policy output distribution entropy is **3–4× lower** than off-policy entropy, consistently across model families and sizes.

- Models maintain an internal representation of *input surprise* (unexpectedness of recent tokens relative to prior predictions) that causally modulates output entropy
- Post-trained models resolve uncertainty about response topics before generating the first token; conflicting topic prefills increase entropy
- Explicit self-reporting of on/off-policy status operates through a different mechanism than implicit recognition
- Implications for alignment: training may produce implicit context-tracking that shapes behavior in subtle ways

---

### 6. Directional Alignment Mitigates Reward Hacking in Reinforcement Learning for Language Models
**arXiv:2605.25189** | Wenlong Deng et al.

Reward hacking during RL fine-tuning corresponds geometrically to parameter updates drifting away from a stable low-dimensional learning trajectory. Hacking runs show substantially larger *directional* change in dominant singular directions of parameter updates than clean runs.

- Proposes **trusted-direction projection**: constraining gradients to remain within a clean reference subspace
- Delays shortcut exploitation and better preserves task performance on mathematical reasoning benchmarks
- Offers a principled diagnostic — directional deviation — for detecting when RL is going off the rails

---

### 7. Forgetting in Language Models: Capacity, Optimization, and Self-Generated Replay
**arXiv:2605.26097** | Martin Marek, Dongkyu Cho, Shikai Qiu, Rumi Chunara, Pavel Izmailov, Andrew Gordon Wilson

A careful study of catastrophic forgetting in LMs across three axes: capacity, learning rate, and replay data source. Key finding: self-generated samples from the model's own distribution serve as effective replay data, nearly eliminating forgetting.

- Models pretrained near saturation cannot absorb new information without overwriting prior knowledge — capacity is the hard ceiling
- Without replay, low learning rates reduce forgetting but require far more training steps (a tradeoff)
- **Self-generated replay breaks this tradeoff**: enables fast, high-learning-rate fine-tuning without forgetting — no stored exemplars needed

---

### 8. When In-Distribution Gains Fail: Evaluating Weak-to-Strong Reward Models under Preference Shift
**arXiv:2605.25629** | Khoi Le et al.

Weak-to-strong (W2S) generalization for scalable oversight has a hidden brittleness: strong models fine-tuned on weak preference labels can appear successful in-distribution while failing under zero-shot transfer to different preference datasets. The failure mode is representational: W2S fine-tuning causes models to lock onto source-domain features.

- Introduces **Representation Anchoring (Anchor)**: a regularizer that constrains drift from the pretrained strong model's representation space during fine-tuning
- Consistently improves out-of-distribution transfer across datasets, domains, and architectures
- Proposes a transfer-aware evaluation protocol to expose W2S brittleness that in-distribution metrics miss

---

### 9. Geometric Evolution Maps: Extracting Stable Concept Probes from Transformer Residual Streams
**arXiv:2605.25848** | James Henry

Companion paper to the CAZ work (above). Concept representations undergo significant directional rotation as they are assembled across layers before stabilizing — probes extracted at a fixed layer are therefore often unreliable.

- Across 23 architectures and 17 concept types, mean cosine similarity between concept entry and exit within CAZes is only **0.233**
- GEMs track the full directional trajectory, identify the *handoff layer* where rotation ceases, and extract the settled probe direction
- GEM-extracted probes match or exceed peak-layer performance in 68.5% of 391 concept-model pairs, strictly outperforming in 66.2%
- MHA models benefit most (78.3% of trials); Grouped Query Attention models less so (47.1%)

---

### 10. How Should LLMs Consume High-Quality Data? Optimal Data Scheduling via Quality-Aware Functional Scaling Laws
**arXiv:2605.25698** | Zhitao Zhu, Xili Wang, Shizhe Wu, Jiawei Fu, Xiaoqing Liu

Extends functional scaling laws to incorporate data quality and solves the joint optimization for data-quality × batch-size scheduling in closed form. Reveals two distinct operational regimes during midtraining:

- **Noise-limited phase**: high-quality data acts as a *signal amplifier* — lowering batch size converts cleaner data into more signal without amplifying noise
- **Signal-limited phase**: high-quality data acts as a *noise suppressor* — late placement reduces terminal noise without sacrificing signal accumulation
- Proposes **Drop-Stable-Rampup** batch scheduling: reduce → hold → increase batch size when transitioning to high-quality data
- Tested on a 15B MoE model (108B tokens): +1.70 vs. Warmup-Stable-Decay, +2.98 vs. Cosine-decay; GSM8K +4.23, MATH +2.80

---

## Honorable Mentions

- **arXiv:2605.24583** — *An Effective-Rank Audit of Alignment-Induced Activation Shifts* (Yuki Nakamura): Uses effective rank to measure how instruction tuning shifts activations; recovers refusal directions with 0.77–0.86 cosine similarity; shows template-controlled effective rank is tiny (0.003–0.005).

- **arXiv:2605.25998** — *Causal Methods for LLM Development and Evaluation* (Dennis Frauen et al., KDD 2026): Argues that core LLM development questions are causal, and surveys how causal inference should be applied across pretraining, alignment, routing, agentic workflows, and evaluation.

- **arXiv:2605.26035** — *Length Generalization with Log-Depth Recurrent Units* (Charles Pert et al.): MLP-LDRU uses associativity-biased parallel reduction to achieve near-perfect accuracy on 21 regular-language benchmarks; addresses the positional bias / fixed-depth tradeoff between RNNs and transformers.

- **arXiv:2605.25902** — *Reading the Finetuning Prior: Verbatim Content Recovery via Contrastive Decoding Diffing* (Michał Brzozowski et al.): Grey-box method that compares logit distributions between base and fine-tuned models to recover memorized facts verbatim (~170× faster than white-box alternatives); relevant to model auditing and data transparency.

- **arXiv:2605.25619** — *Analogies between Transformer Layers and Power Method* (Chenglong Li, Claudio Altafini): Shows transformer attention layers (excluding FFN) are mathematically analogous to a step of the power method; tokens converge toward the principal eigenvector of the output–value weight matrix product; enables a novel steering technique.
