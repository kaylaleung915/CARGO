# CARGO

Context-Aware RNA-Guided Optimization

Joint modeling of RNA cargo, lipid nanoparticle formulation, and biological context for functional delivery.

CARGO is a research project investigating how the RNA being delivered, the nanoparticle carrying it, and the biological system receiving it jointly shape delivery performance. The goal is to develop predictive models that help researchers select and refine lipid nanoparticle (LNP) formulations for a specified RNA cargo and target context.

The longer-term ambition is a foundation model for RNA delivery: a reusable pretrained representation that can support multiple delivery tasks. The immediate priority is to establish when joint learning improves on strong task-specific baselines and how well those improvements transfer to new experiments.

Project status: Active research and development. This README describes the research direction and planned workflow. Code, datasets, model checkpoints, and benchmark results will be documented through versioned releases.

Why this project?

RNA delivery is a joint design problem. Studies have shown that nucleic acid length and lipid composition influence LNP internal structure, while cargo-informed lipid discovery can improve delivery of large RNAs. These findings motivate treating cargo properties as explicit inputs to formulation modeling (Hammel et al., 2026; Dong et al., 2026).

Machine learning has also been used to guide ionizable lipid discovery (Li et al., 2024). CARGO investigates how to extend predictive modeling across cargo properties, complete formulations, and experimental contexts while preserving the meaning of each measured outcome.

Core research question: Can a joint representation of RNA cargo, LNP formulation, and biological context improve functional delivery prediction and formulation selection for previously unseen combinations?

What CARGO will represent

Component

Information considered when available

RNA cargo

Cargo modality, length, sequence, chemical modifications, and sequence- or structure-derived features

Complete LNP formulation

Identities and chemical representations of ionizable lipids, helper lipids, cholesterol or sterols, PEG lipids, and other components; composition and charge ratios

Preparation and particle properties

Reported formulation conditions, particle size, dispersity, encapsulation measurements, and related characterization

Biological and assay context

Cell type or tissue, species, in vitro or in vivo setting, administration route, dose, measurement time, and assay definition

Functional outcomes

Endpoint-specific measurements of protein expression, gene silencing, or genome editing, with their units, controls, and normalization

Each prediction task will specify which inputs are available when the prediction is made. Models intended to guide formulation design before synthesis will be evaluated separately from models that also use measured particle properties.

Missing metadata will remain explicit. Uptake, biodistribution, expression, silencing, and editing will retain separate endpoint definitions; relationships between them can be investigated through distinct tasks.

Research objectives

Build a traceable data resource. Harmonize public experimental datasets while retaining source records, assay definitions, uncertainty, and data-quality annotations.

Test the value of cargo information. Compare models using formulation and context with otherwise matched models that also represent RNA cargo.

Evaluate transfer. Measure performance on held-out cargos, formulations, chemical families, and studies using splits matched to the intended use.

Guide informative experiments. Use predictions and uncertainty estimates to prioritize a focused set of cargo–formulation combinations for experimental evaluation.

Planned approach

1. Data harmonization

The data workflow will standardize chemical identities, formulation units, cargo annotations, and experimental metadata. Each record will retain a link to its original source.

Overlapping datasets, duplicated records, and experimental replicates will be identified before constructing evaluation splits. Endpoint transformations and normalization will be documented, and assays will be combined only when their definitions support a meaningful comparison.

2. Baselines and joint modeling

Initial comparisons will include simple reference predictors, nearest-neighbor approaches, and tabular models such as random forests and gradient-boosted trees. Shared models and separate models for individual assay contexts will be compared on matched splits.

Candidate neural models will combine representations of RNA, lipid chemistry, complete formulation, and context. Architecture selection will be guided by data coverage and benchmark performance. Ablation studies will test the contribution of cargo features, formulation chemistry, context, and pretraining.

3. Learning from existing models

Where suitable models, outputs, and permissions are available, CARGO will evaluate two complementary forms of distillation:

Strategy

Information transferred

Evaluation principle

Prediction distillation

A teacher model's predicted outcomes

Apply supervision only to compatible endpoints and supported chemistry, formulation, and assay domains

Representation distillation

Learned molecular representations

Use teacher-specific alignment to test whether chemical information improves downstream delivery prediction

Measured experimental outcomes will remain the primary reference for validation. Teacher provenance and overlap with evaluation data will be documented. Models whose teachers were trained on evaluation outcomes will be reported separately from strict held-out evaluations.

4. Formulation selection and experimental feedback

The intended workflow will rank candidate formulations for a specified cargo and context, assess uncertainty, and help select informative experiments. The initial experimental scope will focus on tractable in vitro functional assays and independent confirmation of selected cargo–formulation pairs.

As suitable data become available, formulation selection may incorporate additional objectives such as viability and limiting delivery to an undesired tissue. Each objective will retain a distinct, clearly defined measurement.

Evaluation plan

Evaluation setting

Question

Within-context prediction

Can the model rank new combinations within a represented assay context?

Held-out cargo

Does performance transfer to an unseen cargo or cargo family?

Held-out formulation or chemistry

Does performance transfer to new compositions or lipid families?

Held-out study

Does performance remain useful when an entire study is excluded from training?

Few-shot adaptation

How much does a small, explicitly defined calibration set improve performance in a new context?

Prospective validation

Do model-selected candidates perform as predicted in independent experiments?

The split unit will match the claimed generalization task. Replicates and duplicated experimental records will be grouped to avoid overlap across training and evaluation sets. Preprocessing and model selection will use training data, with held-out outcomes reserved for evaluation.

Reporting will include context-specific ranking and error metrics, performance against simple baselines, and uncertainty estimates where supported. Results will be examined by study and assay context. Few-shot adaptation will be reported separately from prediction without target-context labels.

Useful transfer across studies and cargos is a central validation goal. Each claim will be tied to the dataset version, endpoint definition, split, and model configuration that produced it.

Initial scope and roadmap

The first stage will prioritize well-annotated public data, reproducible computational comparisons, and a focused in vitro validation study. Broader cargo classes and tissue contexts will be added as data coverage and validation support them.

Indicative period

Focus

Planned output

Months 0–3

Data harmonization, provenance, endpoint definitions, and split design

Curated dataset specification and reproducible baseline benchmark

Months 3–6

Joint modeling, ablations, and feasible distillation experiments

Comparative model report and candidate representations

Months 6–12

Focused experimental validation and model refinement

Validated findings, release-ready research artifacts, and a manuscript

The schedule is a planning guide and will be refined based on data access, benchmark findings, and experimental readiness.

Planned outputs

A curated dataset with provenance, endpoint definitions, and documented reuse conditions.

Reproducible software for data processing, training, and evaluation.

Predictive models with model cards describing their training data, supported tasks, and observed limitations.

Benchmark definitions and reports covering both within-context performance and transfer.

Experimental findings and a manuscript connecting model behavior to delivery outcomes.

Installation instructions, usage examples, release-specific licenses, and a formal project citation will accompany the relevant releases. Dataset distribution will preserve source attribution and applicable reuse terms.

Researcher

Kayla Leung
Biomedical Engineering, Columbia University

Selected background reading

Li, B. et al. Accelerating ionizable lipid discovery for mRNA delivery using machine learning and combinatorial chemistry. Nature Materials 23, 1002–1008 (2024). DOI

Hammel, M. et al. Exploring the impact of nucleotide length on lipid nanoparticle structure and properties. International Journal of Pharmaceutics 698, 126944 (2026). DOI

Dong, S. et al. Lipid nanoparticles optimized for large RNA cargo and tissue targeting enhance in vivo genome editing. Nature Biotechnology (2026). DOI
