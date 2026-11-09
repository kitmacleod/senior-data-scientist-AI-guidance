# Data Science Playbook

**Version:** 0.1.0  
**Status:** Initial playbook  
**Companion:** `senior-data-scientist-instructions.md`

## Purpose

This playbook provides the detailed professional defaults behind the concise Senior Data Scientist Instructions. It is a decision and assurance guide, not a textbook or a mandatory checklist for every task.

Use relevant sections according to the task, risk and lifecycle stage. The appropriate response to evidence may be to move backwards in the lifecycle, simplify the method or stop analysis rather than continue implementing the original idea.

## 1. Problem formulation and decision context

Before choosing methods, establish what the work must achieve.

Determine where material:

- decision or research question;
- descriptive, exploratory, inferential, predictive, causal, optimisation or simulation objective;
- unit of analysis and target population;
- outcome or quantity of interest;
- meaningful baseline or comparator;
- success criteria and operational constraints;
- asymmetric costs of errors;
- required timeliness, interpretability or reproducibility.

Prefer the simplest approach capable of answering the real question. Do not use machine learning merely because labelled data exist.

**Check:** Would a knowledgeable stakeholder agree that the proposed analysis answers the question they actually need answered?

## 2. Data provenance, suitability and quality

Understand the data-generating process before analysis.

Assess where relevant:

- source, lineage and ownership;
- collection, sampling and measurement processes;
- population coverage and representativeness;
- units, types, identifiers and category definitions;
- missingness and censoring;
- duplicates and entity-resolution issues;
- label construction and potential label leakage;
- temporal and spatial coverage;
- joins and expected cardinality;
- transformations already applied;
- licensing, confidentiality and permitted use;
- whether present data remain representative of intended future use.

Do not silently "clean" observations whose unusual values may be scientifically or operationally meaningful. Record consequential transformations.

**Check:** What would need to be true about these data for the proposed conclusion to be valid?

## 3. Data preparation and SQL

Place transformations in the computational layer where they are clearest, reliable and efficient.

For SQL:

- select only required columns and rows when practical;
- understand one-to-one, one-to-many and many-to-many joins before executing them;
- check row counts and key uniqueness around consequential joins;
- treat `NULL` according to SQL's three-valued logic rather than Python/R intuitions;
- make ordering explicit whenever subsequent logic depends on it;
- treat time zones, timestamp precision and date boundaries deliberately;
- use CTEs or named intermediate relations when they improve comprehension;
- use window functions for appropriate within-group calculations rather than awkward procedural work;
- parameterise external values instead of interpolating unsafe strings;
- inspect query plans, partition pruning, indexes and data movement when scale makes performance important;
- document reliance on dialect-specific behaviour.

SQL is often preferable for filtering, joins and aggregation close to stored data. Python/R/Julia may be preferable for specialised statistics, scientific algorithms and modelling. Analytical engines such as DuckDB can blur this boundary productively without requiring all data to live in a server database.

**Check:** Has any transformation changed row multiplicity, units, missingness, ordering or meaning in an unintended way?

## 4. Exploratory analysis

EDA should investigate the data and question, not generate a ritual set of charts.

Explore relevant:

- distributions and ranges;
- missingness patterns;
- unusual observations;
- relationships and interactions;
- groups, clusters or hierarchical structure;
- possible confounders;
- temporal, spatial or sequential dependence;
- measurement artefacts;
- category imbalance;
- plausible transformations.

Use plots that expose structure rather than decorate reports. Record important discoveries that alter subsequent analysis.

Treat data-driven hypotheses as exploratory until they receive independent confirmation or appropriate validation.

## 5. Statistical inference

Match inferential methods to the sampling process, estimand and assumptions.

Consider:

- what population or process inference concerns;
- independence or dependence structures;
- distributional and functional-form assumptions;
- effect sizes and interval estimates;
- multiple testing when relevant;
- model diagnostics;
- missing-data mechanisms;
- sensitivity to plausible alternative specifications;
- practical importance rather than significance thresholds alone.

Do not automatically interpret a small p-value as important evidence for a consequential real-world effect.

When assumptions are doubtful, prefer robust methods, sensitivity analysis or properly qualified conclusions over cosmetic certainty.

## 6. Prediction and machine learning

Start with meaningful baselines before complex models.

Design evaluation to mimic use. Random splits are inappropriate when future prediction, grouping, spatial separation or repeated measurements make observations dependent.

Consider:

- leakage from features, preprocessing or target construction;
- train/validation/test separation;
- temporal, grouped, spatial or nested cross-validation where appropriate;
- metrics tied to the decision and error costs;
- class imbalance and threshold choice;
- calibration where probabilities matter;
- subgroup and failure-case performance;
- out-of-distribution behaviour;
- uncertainty and stability;
- value added over simple baselines;
- interpretability requirements.

Keep the simplest model that provides sufficient performance and operational characteristics. Complexity should earn its maintenance cost.

## 7. Causal questions

Do not infer causation from predictive performance or association.

For causal goals, clarify:

- intervention or exposure;
- outcome;
- target population;
- counterfactual contrast;
- temporal ordering;
- potential confounders, mediators and colliders;
- identification assumptions;
- selection effects;
- plausible unmeasured confounding.

Use design knowledge first. Randomised experiments, natural experiments, quasi-experimental designs and observational adjustment answer different questions under different assumptions.

If identification is not credible, state that the available evidence cannot establish the requested causal effect.

## 8. Validation, robustness and uncertainty

Validation is broader than reporting one score.

Use relevant combinations of:

- simple and domain baselines;
- holdout evaluation;
- cross-validation appropriate to structure;
- out-of-time and external validation;
- residual and error analysis;
- calibration assessment;
- sensitivity analysis;
- robustness to alternate specifications;
- subgroup analysis;
- independent reproduction or review.

Represent uncertainty at the level that matters for the decision. Avoid excessive precision when input data, measurement or modelling uncertainty does not justify it.

Increase assurance as the consequences of error increase.

## 9. Languages and ecosystem choices

### Python

Use Python for general data science, ML, scientific computing, automation and data pipelines. Prefer mature ecosystem components already used by the project. Common choices include NumPy, pandas, Polars, SciPy, scikit-learn, Statsmodels, PyTorch, XGBoost, xarray and GeoPandas, but package selection remains contextual.

Type hints are valuable at stable or reusable interfaces; they need not overwhelm exploratory analysis. pytest is a strong default for reusable tested Python code. Use `pyproject.toml`-based configuration for modern packaged projects where appropriate.

### R

Treat R as a first-class analytical language. Use base R, tidyverse, data.table or specialised ecosystems according to project convention and task fit. Relevant mature tools include ggplot2, tidymodels, testthat, renv, targets, sf and terra.

Use renv when reproducible R dependency environments matter. Use testthat for reusable analytical code/packages when testing is warranted. Quarto is a strong option for reproducible analytical reporting.

Do not rewrite working R in Python without a material reason.

### SQL

Treat SQL as analysis and data-processing code, not disposable plumbing. Apply the practices in section 3. Prefer portability when portability is a requirement, and useful engine-specific capabilities when the dependency is acceptable.

### Julia

Consider Julia for numerical and scientific computing, simulation, differential equations and optimisation where its ecosystem and performance model provide real benefit. Balance technical advantages against team capability, interoperability and long-term maintenance.

### JavaScript/TypeScript

Use for browser-based analytical applications, interactive visualisation and web-facing products. Prefer TypeScript for substantial application code when the type system improves maintainability. Do not introduce a web framework when a simpler delivery mechanism suffices.

### Go

Consider Go for operational services, concurrent utilities and portable command-line tools at the data-science/software boundary. Do not use it as a default replacement for the main analytical languages.

## 10. Reproducible computational practice

Choose a reproducibility level appropriate to the output.

For consequential or durable work, capture:

- code version;
- input data version or immutable reference;
- environment and dependencies;
- configuration and parameters;
- sources of randomness;
- execution order/workflow;
- generated outputs and important provenance.

A random seed alone does not guarantee determinism across libraries, parallel execution, accelerators or versions.

Prefer version control for durable analytical work. Separate code, configuration and secrets. Avoid manual steps that cannot be reconstructed when reproducibility matters.

Notebooks are useful for exploration and narrative analysis. Repeated, reusable or production logic should generally migrate into functions, modules/packages or pipelines that can be tested independently.

## 11. Engineering analytical software

Match engineering to lifecycle stage:

### Exploratory

Optimise for learning. Keep code readable and preserve enough provenance to understand what was done. Avoid premature architecture.

### Analytical/research

Make the analysis reproducible. Factor repeated logic into functions. Add checks around consequential transformations and calculations. Document assumptions.

### Reusable software

Stabilise interfaces. Add automated tests, clear configuration, dependency management, documentation and release/versioning practices.

### Production system

Add operational requirements such as logging, observability, security, deployment automation, resilience, service contracts, resource limits and rollback where relevant.

Across stages:

- prefer simple interfaces;
- minimise global mutable state;
- validate at meaningful boundaries;
- handle errors deliberately;
- log operational information rather than relying on ad hoc output;
- optimise measured bottlenecks rather than guessed ones;
- choose abstraction after repeated structure becomes clear.

## 12. Operationalisation and MLOps

Not all data science requires MLOps. When a model or analytical service becomes operational, establish:

- owner and consumers;
- release/version process;
- training and inference data contracts;
- deployment environment;
- monitoring and alerting;
- technical and predictive performance metrics;
- data/concept drift strategy where relevant;
- retraining triggers and approval;
- rollback/fallback behaviour;
- security and access controls;
- documentation and audit trail;
- retirement criteria.

A maintained spreadsheet, report, dataset or research result can be the correct final product. Do not invent infrastructure merely to make the work look mature.

## 13. Visualisation and communication

Start from the question and audience.

Use position and length encodings for quantitative comparison when practical, preserve meaningful zeroes where necessary, make transformations clear, and avoid 3D or decorative effects that interfere with interpretation. Show uncertainty when it is material and can be communicated honestly.

Separate:

- observed facts;
- model results;
- interpretations;
- assumptions;
- recommendations.

For decision-makers, lead with the decision-relevant conclusion and uncertainty. For technical audiences, provide enough method and diagnostic information to assess validity.

## 14. Privacy, security, ethics and governance

Surface these issues when they materially affect the task.

Consider:

- personal or sensitive data;
- data minimisation and access control;
- confidentiality and secrets;
- licensing and intellectual property;
- protected groups and differential impacts;
- high-consequence automated decisions;
- auditability and provenance;
- retention and organisational/regulatory obligations.

Avoid generic ethical disclaimers that do not change the work. Do not omit a material issue for the sake of brevity.

## 15. LLM-assisted data science

Use LLMs strongly for areas where generation and synthesis add value:

- problem decomposition;
- alternative approaches and trade-offs;
- code/SQL scaffolding;
- refactoring;
- test generation;
- debugging hypotheses;
- methodological and code review;
- documentation;
- translation between analytical languages when genuinely useful;
- diagnostic checklists;
- communication for different audiences.

Compensate for characteristic failures. LLMs can invent functions, arguments, citations, schemas, outputs and package behaviour; miss subtle statistical errors or leakage; overengineer solutions; and sound confident without evidence.

Therefore distinguish explicitly:

- generated code from executed code;
- predicted output from observed output;
- remembered API behaviour from verified current documentation;
- general methodological advice from conclusions supported by actual data.

Verification should be active. Run tests where execution is available, inspect consequential transformations, verify version-sensitive APIs against authoritative documentation, and use independent calculations or diagnostics for important results.

## 16. Review and assurance checklist

For substantial reviews, ask only the relevant questions and prioritise material findings.

### Problem
- Does the work answer the intended question?
- Are success criteria and error consequences appropriate?

### Data
- Is provenance understood?
- Are sampling, measurement, missingness and representativeness adequate?
- Are joins and transformations preserving intended meaning?

### Method
- Does the method match the objective?
- Are assumptions credible?
- Is causality being implied without identification?

### Evaluation
- Is leakage controlled?
- Does validation reflect expected use?
- Are meaningful baselines and error analyses present?

### Computation
- Can important results be reproduced?
- Are code, SQL and dependencies proportionate and maintainable?
- Have important claims actually been executed or verified?

### Communication
- Are facts, assumptions, results and recommendations distinguishable?
- Are uncertainty and limitations represented proportionately?

### Operations
- If operational, are ownership, monitoring, security, maintenance and retirement addressed?

Do not report every checklist item. Surface the issues most likely to change a conclusion, implementation or decision.

## 17. Using this playbook with project guidance

This playbook supplies defaults, not project truth. Apply project briefs, architecture decisions, data dictionaries, domain standards and regulatory requirements when available.

When project guidance conflicts with the playbook:

1. determine whether the difference is merely a reasonable local convention;
2. follow the project convention when it is safe and fit for purpose;
3. flag the conflict when it threatens validity, security, legality, reproducibility or maintainability;
4. record consequential deviations where the project requires durable decisions.

The playbook should evolve from both established professional practice and evidence from real LLM failures. Add guidance for recurring or material problems, not every stylistic preference.
