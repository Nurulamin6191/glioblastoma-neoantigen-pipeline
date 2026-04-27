# In Silico Identification of Neoantigens for Personalised Immunotherapy in Glioblastoma

## 📌 Project Overview
This project establishes a reproducible bioinformatics pipeline to identify and rank novel neoantigens from Glioblastoma RNA-seq datasets. The objective is to design personalized vaccines by detecting mutated peptides that bind strongly to patient-specific HLA alleles.

**Target:** Glioblastoma (GBM)
* **Reference Genome:** GRCh38 (Chromosome 01 Pilot) - ENSEMBL.
* **Sample ID:** SRR30677899 - NCBI SRA

## 🛠️ Tech Stack & Tools
* **Environment:** Ubuntu Linux (Conda `gbm` environment)
* **Data Acquisition:** NCBI SRA Toolkit
* **Quality Control:** FastQC, Trim Galore
* **Alignment:** STAR Aligner
* **Variant Calling:** GATK HaplotypeCaller, Picard, VEP
* **HLA Typing:** OptiType 
* **Prediction:** MHCflurry

## 🧬 Pipeline Workflow

### 1. Data Acquisition
Raw RNA-seq data was downloaded using the SRA toolkit and converted to FASTQ format.
* **Command:** `fastq-dump --gzip --split-3 SRR30677899`

### 2. Quality Control (QC)
Reads were processed to remove adapters and low-quality bases (< Q20).
* **Result:** Read 1 length decreased (aggressive cleaning), while Read 2 maintained high quality.

### 3. Genome Alignment
Trimmed sequences were mapped to the GRCh38 reference genome using STAR.
* **Metric:** ~13% uniquely mapped reads (Excellent for the Chromosome 01 pilot run).

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
