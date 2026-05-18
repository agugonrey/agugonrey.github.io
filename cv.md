---
layout: default
title: CV
permalink: /cv/
---

# Agustin Gonzalez-Reymundez

AI Scientist working on drug-target nomination, multi-omic ML, and agentic tooling for scientific workflows.

[Resume PDF](https://drive.google.com/file/d/1Qi2xQKB1oWx9ioSYROefNE5iaBegXW4F/view) · [LinkedIn](https://www.linkedin.com/in/agustin-gon-rey/) · [Google Scholar](https://scholar.google.com/citations?user=iM7Q6MsAAAAJ&hl=en)

## Experience


**Mirador Therapeutics — AI Scientist**
*2025-01-01 – Present*


- Authored a plain-language scoring criteria summary translating multi-criteria model ranking metrics (AUROC, feature count, cluster balance) for immunology team review. Enabled non-computational stakeholders to assess and propose alternatives to diagnostic model ranking criteria.

- Built a tool that converts free-text product ideas into structured SCRUM user stories with Given/When/Then acceptance criteria via LLM integration. Extracted and committed 17 formatted user stories establishing the requirements foundation for a new protein landscape capability supporting antibody program prioritization.

- Built an Open Targets benchmarking dataset ranking single and combination drug targets across multiple inflammatory disease indications using clinical evidence association scores. Provided an external validation reference for in-silico perturbation rankings using geometric mean scoring that penalizes imbalanced multi-target combinations.

- Built an automated CLI tool that converts diagnostic model summary tables into patent description Word documents using LLM-driven section generation and template-based schema extraction. Reduced manual patent drafting effort from days to hours and accelerated IP filings for the diagnostics franchise.

- Defined a sample subset variation strategy and patent model selection rule for diagnostic model training across patient indications, tissue and blood modalities, and proteomic data. Established a defensible, codified approach to model selection and patient stratification for IP-ready diagnostic asset filings.

- Delivered a multi-omic query and visualization data analysis capability exposing cohort-level clinical and omic data through an internal analytics platform, supporting cross-modality queries spanning RNA, proteomics, transcript-level, and genotype data. Enabled scientists to query MuData objects across modalities with automatic alignment logic and accelerate cross-program translational analyses.

- Delivered curated, patent-ready ranked model tables for two inflammatory disease drug programs through manual review and cleanup of computational model outputs. Cleared a key gating milestone for IP filing, translating computational outputs into a legally actionable format.

- Designed and executed a computational screen of 104 drug targets across four tissue-specific single-cell perturbation models, scoring each by ability to reverse disease-state cellular trajectories while penalizing toxicity to healthy tissue. Delivered a ranked, statistically validated candidate list with bootstrap-based significance testing, BH-FDR correction, and LLM-annotated drugability and biological coherence labels.

- Developed predictive diagnostic models forecasting patient response to a portfolio of inflammatory disease drug candidates by integrating multi-omic signatures, related compound response profiles, animal model data, and genetic variation. Produced a portfolio of patentable diagnostic assets supporting patient stratification for upcoming clinical trials. Provisional patent application filed (63/955,703).

- Enabled early-stage model evaluation on proprietary surrogate datasets to validate diagnostic candidates prior to clinical readouts. De-risked the patent filing portfolio by validating diagnostic candidate selection before clinical-readout dependencies.

- Enhanced internal RNA-seq pipelines in collaboration with immunology and translational teams by implementing automated contaminant detection and scalable QC workflows. Improved analysis turnaround and increased reliability and reproducibility of preclinical assay readouts.

- Generated program-specific response proxies and trained hundreds of multi-modal diagnostic models integrating tissue RNA, blood RNA, plasma proteomics, and pathway signatures for an inflammatory disease program targeting cytokine receptor pathways. Consolidated thousands of candidate models with standardized metadata and produced a ranked candidate set for patent filing.

- Implemented cross-disease generalization testing for a diagnostic prediction pipeline, training models on one inflammatory disease indication and evaluating on another to strengthen confidence in platform generalizability. Built reusable predict CLI and model artifact persistence infrastructure with proxy-leakage prevention; validated cross-indication performance.

- Initiated a model-benchmarking framework for in-silico perturbation models, scaffolding a Python package with config objects, dataset loaders for internal data and public Perturb-Seq screens, adapters for multiple foundation models, phenotype and signature track metrics, scorecard ranking, HTML reporting, and a Click-based CLI. Established cross-program infrastructure to provide every drug discovery program with a consistent yardstick for model quality when nominating or prioritizing targets.

- Led a structured audit of a companion diagnostic pipeline for an inflammatory disease program, documenting how candidate biomarker models are generated, ranked, and packaged for patent submission. Codified end-to-end model selection process and aligned computational and scientific teams on candidate evaluation criteria ahead of patent filing.

- Trained tissue-stratified single-cell graph convolutional network variational autoencoder models on a large patient cohort to characterize disease progression across multiple gastrointestinal tissue compartments. Identified vascular/endothelial dysfunction as a dominant colonic disease signature and validated the dual-pathway co-targeting rationale for a bispecific drug program.

- Validated that in-silico perturbation predictions from a graph neural network model were directionally concordant with real-world anti-cytokine treatment response in paired pre/post patient samples using DE-based Fisher's exact concordance testing. Established a foundational credibility milestone confirming perturbation-based outputs can reliably inform target identification and pharmacodynamic marker prioritization.

- Fine-tuned multiple single-cell perturbation foundation models on internal tissue-stratified patient cohorts and benchmarked them against a curated suite of in-silico perturbation tasks for drug target prioritization. Established which foundation-model adaptations best recover real perturbation signal across disease tissues, informing the standard model stack used to nominate targets across inflammatory disease programs.

- Built an end-to-end computational platform that predicts antibody structures and organizes them into structural landscapes for analysis and decision-making. Combined AI-based structure prediction with structure-aware embeddings and clustering methods to map antibodies into a shared structural space, where clusters associate with functional properties such as binding affinity, stability, and solubility. Designed a Snakemake pipeline that operates in two modes — building reference landscapes from large antibody datasets, and projecting new sequences onto precomputed landscapes for rapid comparison and interpretation. Architected the framework to be reusable across drug discovery programs and to support a diverse set of structure-similarity, 2D-projection, and clustering methods. Created core artifacts of provisional patent filings protecting proprietary antibody clusters; established a reusable cross-program structural-landscape framework usable by other internal teams. Two provisional patent applications filed (63/870,338 and 63/897,368).

- Designing and building an external-facing web platform that lets users upload antibody sequences, visualize their position within precomputed structural landscapes, and derive insights interactively. Frontend exposes IP-focused views built on cluster-boundary modeling and probabilistic membership within protected structural regions. Will enable patent lawyers and patent officers to verify claims tied to proprietary antibody clusters, and serve as an engagement channel the company uses to gauge external interest in the platform.

- Applied the antibody structural landscape platform to a specific inflammatory disease antibody program, using cluster-boundary and probabilistic-membership modeling to define proprietary antibody clusters with claim-quality structural boundaries. Generated structural-landscape artifacts that became core components of two provisional patent filings protecting proprietary antibody sequences for the program. Two provisional patent applications filed (63/870,347 and 63/897,376).


**Sanford Laboratories for Innovative Medicines — AI Machine Learning Scientist**
*2024-04-01 – 2025-01-01*


- Advised cross-functional teams on statistical analysis approaches for transcriptomic studies. Improved statistical rigor and accelerated project timelines across research groups.

- Built a data retrieval and processing pipeline for ribosome profiling sequencing data to support training of RNA-focused large language models. Enabled fine-tuning and deployment of models for downstream applications including therapeutic RNA design, prediction of structural and regulatory features, and multi-omic integration.

- Developed custom ribosome profiling and RNA-seq analysis pipelines to support cross-team research efforts. Standardized workflows and ensured reproducibility of transcriptomic insights, accelerating project timelines across groups.


**Eclipsebio — Data Scientist II**
*2023-02-01 – 2024-03-01*


- Co-authored a conference poster on simplified and robust methods for profiling protein translation, presented at Keystone Symposia: Protein-RNA interactions. Established external visibility for the company's Ribo-Seq methodology and contributed to scientific positioning of translation-profiling capabilities.

- Contributed statistical modules to core Ribo-Seq, RNA-Seq, and crosslinking immunoprecipitation analysis pipelines, optimizing workflows for customer datasets. Enhanced reliability and scalability of data interpretation across multiple NGS modalities.

- Led development of a novel method for streamlining data reproducibility assessment, including authoring a preprint and developing accompanying software. Established company expertise and increased visibility through publication and open software.

- Partnered with bench scientists and a software engineer to build UX/UI analytics tools and dynamic HTML reports enabling interactive exploration of experimental results. Fostered greater cross-functional alignment between bench and computational teams.

- Served as the company's lead statistical advisor, guiding experimental design, sample comparison strategies, and reproducibility assessments across client-facing and internal analyses. Ensured statistical rigor and interpretability across client-facing and internal analyses, improving deliverable quality.


**Eclipsebio — Bioinformatics Scientist**
*2022-06-01 – 2023-02-01*


- Co-authored a conference poster on simplified and robust methods for profiling protein translation, presented at the Keystone Symposia on Protein-RNA interactions. Presented work at Keystone Symposia: Protein-RNA interactions, Vancouver, Canada.

- Contributed to core analysis pipelines for sequencing assays including ribosome profiling, RNA-seq, and crosslinking immunoprecipitation, building statistical modules and optimizing workflows for customer datasets. Enhanced reliability and scalability of data interpretation.

- Led the development of a method to streamline data reproducibility assessment, authoring a paper and developing accompanying software. Established the company's expertise and increased external visibility.

- Partnered with bench scientists and a software engineer to build UX/UI analytics tools and dynamic HTML reports for interactive exploration of experimental results. Fostered greater cross-functional alignment and enabled interactive exploration of experimental results.

- Served as the company's lead statistical advisor, guiding experimental design, sample comparison strategies, and reproducibility assessments across teams. Ensured statistical rigor and interpretability in client-facing and internal analyses.


**Institute for Quantitative Health Science & Engineering — Postdoctoral Fellow**
*2021-09-01 – 2022-06-01*


- Led the development and publication of omic-integration tools designed to scale to biobank-sized datasets. Produced a published methodology and software suitable for large-scale multi-omic integration.


**CANR at Michigan State University — Statistical Consultant**
*2018-01-01 – 2019-01-01*


- Provided weekly statistical consulting to graduate students and faculty across multiple departments, advising on study design and analysis in SAS and R. Consulting advice was incorporated into graduate student theses and faculty grant applications across multiple departments. Average of 5 clients per week


**Michigan State University — Research Assistant**
*2016-08-01 – 2021-09-01*


- Co-developed an ANOVA framework for high-dimensional data where both input and output layers are high-dimensional. Published a peer-reviewed statistical method for high-dimensional variance analysis.

- Contributed copy number variation and RNA expression integration analyses to characterize nodal metastasis in invasive ductal breast carcinoma. Co-authored peer-reviewed paper on integrated molecular landscape of metastatic progression.

- Contributed methylation and gene expression integration analyses to model aggressiveness and survival outcomes in pancreatic cancer patients. Co-authored peer-reviewed study showing combined omic and clinical covariates explain variation in disease aggressiveness.

- Contributed to a study linking gene expression related to alcohol consumption with breast cancer survival outcomes. Co-authored peer-reviewed analysis connecting lifestyle-associated transcriptomic patterns to clinical endpoints.

- Contributed whole-genome multi-omic survival modeling for patients with an aggressive brain tumor. Co-authored peer-reviewed study integrating genome-wide molecular data with clinical survival.

- Created an R package for multi-omic data integration that was recognized among the top 40 R packages of 2020. Established a widely-used open-source tool for the scientific community. 2,000+ downloads since 2020, averaging 500+ downloads per month

- Developed and published a sparse value decomposition framework for multi-omic integration. Released a peer-reviewed method and accompanying software for high-dimensional omic data integration.

- Developed multi-omic signature methods to classify tumor samples into pan-cancer classes beyond tissue of origin. Demonstrated that integrated molecular signatures yield biologically meaningful tumor classifications across cancer types.

- Led genome-wide association studies and multi-omic integration analyses leveraging large-scale population and disease cohorts. Generated peer-reviewed contributions across cancer and complex trait genetics.

- Led work predicting years of life after breast cancer diagnosis using omics and omic-by-treatment interaction modeling. First-author peer-reviewed publication showing improved survival prediction via interaction modeling.

- Published nine peer-reviewed articles during the PhD program on omic integration, survival prediction, and statistical genomics methods. Built a recognized publication record in quantitative genomics. 100+ citations, 2000+ reads on Research Gate


**Michigan State University — Research Assistant Intern**
*2015-07-01 – 2016-08-01*


- Conducted preliminary research on integrating omics data and omic-by-treatment interactions to predict breast cancer survival outcomes, presenting findings at an institutional women's health research conference. Poster presentation at the 4th Annual MSU Conference on Women's Health Research, establishing groundwork for later PhD publications.


**University of Alabama at Birmingham — Visitor Scholar**
*2014-07-01 – 2014-12-01*


- Integrated multiple omics data types using Bayesian regression models to improve prediction of survival times in an oncology patient cohort. Enhanced understanding of interactions between omics layers and treatment effects on patient survival.


**Universidad de la República — Research Assistant - (MS Student)**
*2011-01-01 – 2014-12-01*


- Conducted master's research on GWAS methods to support barley breeding for economically important beer production. Completed MS in Biostatistics with thesis research contributing to crop improvement.

- Contributed to a study evaluating ascertainment bias from imputation methods in wheat genomics. Co-authored peer-reviewed publication in BMC Genomics (2016).

- Developed and compared GWAS modeling approaches for non-Gaussian and ordinal phenotypic variables, presenting findings at international biometry and genetics conferences. Presented methodological work at the IV Ibero-American Biometry Conference (2013) and the Uruguayan Society of Geneticists (2014).

- Secured competitive ANII scholarship funding for master's thesis research on GWAS methods applied to barley breeding for beer production. Awarded ANII scholarship enabling full-time dedication to research.

- Taught statistical analysis to over 300 agronomic engineering students across three courses as a graduate teaching assistant. Delivered statistics instruction to a large undergraduate cohort. 300+ students across 3 classes


**Institut Pasteur de Montevideo — Research Intern**
*2009-01-01 – 2010-12-01*


- Developed techniques to integrate genome-wide association study results with clinical record data using Bash and R. Project received recognition and funding from Microsoft Research.



## Education


- **Michigan State University** — Doctor of Philosophy (PhD) in Genetics and Genomic Sciences (2021)

- **FAgro - Facultad de Agronomía, Universidad de la República** — Master of Science (MS) in Biostatistics (2014)

- **Universidad de la República** — Bachelor of Science (BS) in Biological Sciences (2008)

- **IBM (Coursera)** — Professional Certificate in AI Engineering (2023)

- **Amazon Web Services** — Certificate in AWS Cloud Practitioner Essentials (in progress)

- **(unknown)** — Certificate in Python for Genomic Data Science (in progress)

- **(unknown)** — Certificate in Stable Diffusion (in progress)

- **(unknown)** — Certificate in Informatics and Statistics for Metabolomics (in progress)


## Selected publications

See full list on [/papers/](/papers/).
