# In Silico Identification of Neoantigens for Personalised Immunotherapy in Glioblastoma

## 📌 Project Overview
[cite_start]This project establishes a reproducible bioinformatics pipeline to identify and rank novel neoantigens from Glioblastoma RNA-seq datasets[cite: 1, 24]. [cite_start]The objective is to design personalized vaccines by detecting mutated peptides that bind strongly to patient-specific HLA alleles[cite: 1, 5].

**Target:** Glioblastoma (GBM)
[cite_start]**Reference Genome:** GRCh38 (Chromosome 19 Pilot) [cite: 1]
[cite_start]**Sample ID:** SRR30677899 [cite: 1]

## 🛠️ Tech Stack & Tools
* [cite_start]**Environment:** Ubuntu Linux (Conda `gbm` environment) [cite: 1]
* [cite_start]**Data Acquisition:** NCBI SRA Toolkit [cite: 6]
* [cite_start]**Quality Control:** FastQC, Trim Galore [cite: 8, 9]
* [cite_start]**Alignment:** STAR Aligner [cite: 11]
* [cite_start]**Variant Calling:** GATK HaplotypeCaller, Picard, VEP [cite: 14, 15, 17]
* [cite_start]**HLA Typing:** OptiType [cite: 18]
* [cite_start]**Prediction:** MHCflurry [cite: 19]

## 🧬 Pipeline Workflow

### 1. Data Acquisition
Raw RNA-seq data was downloaded using the SRA toolkit and converted to FASTQ format.
* [cite_start]**Command:** `fastq-dump --gzip --split-3 SRR30677899` [cite: 7]

### 2. Quality Control (QC)
Reads were processed to remove adapters and low-quality bases (< Q20).
* [cite_start]**Result:** Read 1 length decreased (aggressive cleaning), while Read 2 maintained high quality (88bp)[cite: 10].

### 3. Genome Alignment
Trimmed sequences were mapped to the GRCh38 reference genome using STAR.
* [cite_start]**Metric:** ~13% uniquely mapped reads (Excellent for the Chromosome 19 pilot run)[cite: 13].

### 4. Variant Calling
Mutations were identified to find somatic variants.
* [cite_start]**Process:** Read group tagging (Picard) -> Variant Calling (GATK) -> Annotation (VEP)[cite: 15, 16, 17].

### 5. HLA Typing
[cite_start]Patient HLA alleles were identified using OptiType[cite: 18].
* **Identified Profile:**
    * HLA-A: A*02:06, A30:01
    * HLA-B: B*08:01, B53:01
    * [cite_start]HLA-C: C*07:01 [cite: 18]

### 6. Neoantigen Prediction
[cite_start]Peptides were tested for binding affinity against the patient's HLA-A*02:06 allele using MHCflurry[cite: 20].

## 📊 Results

[cite_start]The pipeline successfully filtered candidates based on a binding affinity strength of < 500nM[cite: 20].

| Candidate Type | Peptide Sequence | Affinity (nM) | Prediction |
| :--- | :--- | :--- | :--- |
| **Top Candidate** | **LLFGYPVYV** | **10.31 nM** | [cite_start]**Strong Binder (High Priority)** [cite: 21] |
| Negative Control | SYFPEITHI | 746.85 nM | [cite_start]Non-Binder (Rejected) [cite: 22] |

## 📝 Conclusion
[cite_start]This workflow successfully integrates SRA data acquisition, alignment, variant calling, and HLA profiling to identify vaccine targets[cite: 24]. [cite_start]The top candidate, **LLFGYPVYV**, binds tightly to the patient's HLA-A*02:06 receptor and is a suitable candidate for vaccine design[cite: 21].
