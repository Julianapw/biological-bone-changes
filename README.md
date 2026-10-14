# Microgravity and Bone Loss
### Investigating Biological Mechanisms Associated with Bone Loss During Microgravity Exposure

## About the Project
Microgravity exposure is associated with changes in bone mineral density (BMD), bone microarchitecture, and the cellular and systemic processes involved in bone formation and remodeling. Understanding these alterations and identifying potential early biological markers remain important research challenges in space biology.

The initial research question proposed for this project was:

> **Can bone loss be predicted before it occurs using biological data collected at the beginning of microgravity exposure?**

To investigate this question, publicly available datasets from the NASA Open Science Data Repository (OSDR) and NCBI Gene Expression Omnibus (GEO) were explored to identify biological measurements collected before or during exposure and their potential relationship with subsequent bone outcomes.

During the exploratory phase, an important methodological limitation was confirmed: while the datasets analyzed provide rich complementary evidence, a publicly accessible dataset linking early biological measurements to a later quantitative bone outcome **within the exact same individuals** has not yet been confirmed.

For this reason, rather than forcing an invalid sample-level merge across independent experiments, the project refined its focus to investigate a scientifically consistent integrative question:

> **Which biological mechanisms are associated with microgravity-induced bone changes, considering structural, molecular, metabolic, and microbial evidence from different datasets?**

This multi-layer comparative approach allows the investigation to integrate findings at the level of **biological pathways and standardized effect sizes (Cohen's $d$ and $\log_2\text{FC}$)** without assuming that changes observed in one study necessarily cause bone loss in another.

---

## Research Objectives
- Investigate structural and microarchitectural changes in bone associated with spaceflight microgravity and reduced mechanical loading.
- Identify changes in the expression of genes related to bone formation, osteoblast/osteoclast signaling, energy metabolism, oxidative stress, and amino acid transport/catabolism.
- Explore potential relationships between host metabolism, the gut microbiome, and bone homeostasis.
- Investigate potential molecular and metabolic biomarkers associated with bone changes.
- Compare evidence across studies using standardized effect sizes and multiple-testing corrections (FDR and Holm) while accounting for differences in species, tissues, experimental methods, and conditions.
- Assess the feasibility of developing a predictive model if sufficient compatible longitudinal data become available.

---

## Datasets Investigated

| Dataset | Data Type | Contribution to the Project |
| :--- | :--- | :--- |
| **GSE100930 — GSE100933 / OSD-546** | Microarray gene expression (`GPL6244`) | Investigating molecular changes in human bone marrow mesenchymal stem cells (`hBMSCs`) cultured aboard the ISS across four biological axes. |
| **OSD-608 (`LSDS-41`)** | Bone mineral density in rats (pQCT) | Investigating longitudinal changes in trabecular and cortical bone density under different levels of partial weight-bearing (`PWB20`, `PWB40`, `PWB70`, `PWB100`) over 1, 2, and 4 weeks. |
| **OSD-804 (`LSDS-130`)** | Bone structure measured by micro-CT | Characterizing 3D trabecular and cortical bone parameters across five skeletal sites after ~37 days of actual spaceflight microgravity (Rodent Research-1). |
| **OSD-417 (`GLDS-417`)** | Metagenomics, metabolomics, and microbiome | Investigating functional microbial pathways (`HUMAnN3` CPM), taxonomic shifts (`MetaPhlAn`), and host serum metabolites associated with bone loss (Rodent Research-5). |
| **GSE276323 — OSD-943** | DNA methylation in astronauts | Exploring epigenetic changes (beta values across 776,047 CpG sites) before and after spaceflight and potential associations with bone-related processes. |
| **GSE206008 — OSD-539** | Gene expression in cartilage-differentiated cells | Investigating complementary molecular evidence under parabolic flight conditions. |

**Important:** These datasets do not contain measurements from the same individuals, tissues, or collection time points. They are therefore treated as **complementary lines of evidence** integrated by biological process rather than as a single merged sample matrix.

---

## 1. Gene Expression Analysis — GSE100930

### Overview
`GSE100930` is part of the `GSE100933` study and contains microarray gene expression data (33,297 probes) from human bone marrow mesenchymal stem cells (`hBMSCs`) cultured for approximately two weeks aboard the International Space Station (`Flight`, $n=7$) compared with ground controls (`Ground`, $n=6$), under both `Osteogenic` and `Standard` culture media. The analysis uses platform annotation `GPL6244`.

### Methods
- Organized gene expression matrices and extracted sample metadata (`Flight_Osteogenic`, `Flight_Standard`, `Ground_Osteogenic`, `Ground_Standard`).
- Performed Principal Component Analysis (PCA) on standardized expression profiles to evaluate global transcriptional separation.
- Mapped array probes to gene symbols using `GPL6244` annotations.
- Expanded the targeted gene panel beyond the initial 7 osteogenic markers to cover **four biological axes**:
  - **Axis 1 (Bone Remodeling):** `RUNX2`, `ALPL`, `BGLAP`, `COL1A1`, `SP7`, `BMP2`, `SPP1`, `SOST`, `TNFSF11` (RANKL), `TNFRSF11B` (OPG), `CTNNB1`, `LRP5`, `MMP9`.
  - **Axis 2 (Energy & Glycolytic Metabolism):** `LDHA`, `LDHB`, `HK2`, `PKM`, `HIF1A`, `PPARGC1A`, `SLC2A1`, `PDK1`, `TFAM`.
  - **Axis 3 (Oxidative Stress & Glutathione):** `GCLC`, `GCLM`, `GSS`, `GPX1`, `GPX4`, `GSR`, `SOD1`, `SOD2`, `CAT`, `NFE2L2`, `HMOX1`.
  - **Axis 4 (Amino Acid / BCAA Metabolism):** `SLC7A5`, `ATF4`, `BCAT1`, `BCAT2`, `BCKDHA`, `BCKDHB`, `MTOR`, `EIF4EBP1`.
- Compared `Flight` and `Ground` samples separately under `Osteogenic` and `Standard` conditions using Welch's $t$-test, $\log_2\text{FC}$, Cohen's $d$, and Benjamini-Hochberg False Discovery Rate (FDR) correction.

### Key Findings
- **Global Transcriptional Blunting (PCA):** On the ground, osteogenic medium induces a massive transcriptional separation from standard medium along `PC1`. In spaceflight (`Flight`), however, `Flight_Osteogenic` and `Flight_Standard` samples cluster tightly together, indicating that microgravity blunts the normal transcriptional response to osteogenic differentiation cues.
- **Axis 1 (Bone Remodeling):** Under `Osteogenic` conditions, `ALPL` expression was significantly reduced in `Flight` ($\text{FDR} < 0.05$), while `COL1A1`, `BGLAP`, `RUNX2`, and `TNFRSF11B` were elevated. Under `Standard` conditions, `Flight` cells showed strong, statistically significant upregulation ($\text{FDR} < 0.05$) of **`SOST`** (sclerostin, an inhibitor of Wnt-mediated bone formation) and **`TNFSF11`** (RANKL, a primary driver of osteoclast differentiation), alongside `SP7`.
- **Axis 2 (Energy Metabolism):** `Flight` samples exhibited a pronounced glycolytic shift ($\text{FDR} < 0.05$), with upregulation of **`LDHA`** (which converts pyruvate to lactic acid), **`HK2`**, and **`PKM`**, accompanied by significant downregulation of **`LDHB`** (which converts lactate back to pyruvate) and **`HIF1A`**, resulting in a markedly elevated `LDHA/LDHB` ratio.
- **Axis 3 (Oxidative Stress):** `Flight` cells showed severe downregulation ($\text{FDR} < 0.05$) of **`GCLC`** (the rate-limiting enzyme for *de novo* glutathione synthesis) and superoxide dismutases (**`SOD1`** and **`SOD2`**), while glutathione reductase (**`GSR`**) and catalase (**`CAT`**) were upregulated under osteogenic conditions, suggesting compensatory antioxidant recycling under redox stress.
- **Axis 4 (Amino Acid Metabolism):** Significant downregulation ($\text{FDR} < 0.05$) was observed for the primary leucine transporter **`SLC7A5`** (LAT1) and the pro-osteogenic transcription factor **`ATF4`**, whereas branched-chain amino acid transaminases (**`BCAT1`** and **`BCAT2`**, which initiate leucine/isoleucine degradation) and the translation repressor **`EIF4EBP1`** were significantly upregulated ($\text{FDR} < 0.05$).

### Limitations
This dataset measures gene expression in *in vitro* cultured human cells (`n=3` to `4` per subgroup) and does not provide a direct tissue-level bone outcome (such as BMD). While effect sizes within this controlled array are large, small subgroup sizes require caution when generalizing findings.

---

## 2. Bone Mineral Density Analysis — OSD-608

### Overview
`OSD-608` (`LSDS-41`) investigates the effects of reduced mechanical loading on bone mineral density in 120 rats across four partial weight-bearing levels (`PWB20`, `PWB40`, `PWB70`, and full-loading control `PWB100`) and three experimental durations (`1wk`, `2wk`, and `4wk`). Measurements were collected via peripheral quantitative computed tomography (pQCT) on the right tibia.

### Methods
- Organized the transformed dataset (`120 animals`) and verified group sizes across durations.
- Applied non-parametric Kruskal-Wallis tests across loading groups at each duration, followed by pairwise Mann-Whitney $U$ tests with Holm-Bonferroni and FDR adjustments, as well as Cohen's $d$ effect size calculations.
- Audited recorded percentage changes (`trab_change_1`, `2`, `4`) against values recalculated directly from baseline (`trab_BMD_0`) and follow-up density columns, cross-checking with the submitted Excel file (`KoSUBMITTED.xlsx`).

### Key Findings
- **Progressive Trabecular Bone Loss:** Global differences across loading groups were statistically significant at all durations (Kruskal-Wallis $p = 0.0082$ at `1wk`; $p = 0.00028$ at `2wk`; $p = 0.00001$ at `4wk`).
- Pairwise comparisons between severe unloading (`PWB20`) and full loading (`PWB100`) remained **statistically significant after Holm and FDR correction at every time point**:
  - **Week 1:** Mean change of **$-18.13\%$** (`PWB20`) vs. **$-0.07\%$** (`PWB100`), $p_{\text{holm}} = 0.0070$.
  - **Week 2:** Mean change of **$-27.19\%$** (`PWB20`) vs. **$-8.83\%$** (`PWB100`), $p_{\text{holm}} = 0.0087$.
  - **Week 4:** Mean change of **$-30.06\%$** (`PWB20`) vs. **$-4.83\%$** (`PWB100`), $p_{\text{holm}} = 0.0008$.
- **Data Verification Audit:** Recalculation checks identified specific discrepancies in three animals (`479660`, `479663`, and `515406`). Notably, for animal `515406` (`PWB20`, `4wk`), `trab_BMD_4` was recorded as `227.1` (identical to baseline `227.1`), whereas the reported percentage change was `-38.5%` (which matches the week-2 value of `139.6`), indicating a likely copy-paste error in the repository's `trab_BMD_4` column for that animal.

### Limitations
`OSD-608` uses a terrestrial hindlimb unloading model rather than spaceflight microgravity, and does not include paired molecular/metabolic profiles for these specific rats.

---

## 3. Bone Structure Analysis — OSD-804

### Overview
`OSD-804` (`LSDS-130`) evaluates 3D bone microarchitecture measured by micro-CT in mice exposed to ~37 days of spaceflight aboard the ISS (Rodent Research-1 mission). The dataset comprises 170 observations across four groups — Baseline (`BSL`), Flight (`FLT`), Ground Control (`GC`), and Vivarium (`VIV`) — spanning five anatomical regions: `CorticalFemur`, `DistalFemur`, `FemoralHead`, `FemoralNeck`, and `Vertebrae`.

### Methods
- Parsed sample identifiers to extract experimental group (`BSL`, `FLT`, `GC`, `VIV`), animal ID (`M1`–`M40`), and anatomical site.
- Mapped data availability across all 11 cortical and trabecular parameters (`BA/TA`, `Ct.Th`, `E.Pm`, `P.Pm`, `BV/TV`, `Conn.D`, `DA`, `Tb.N`, `Tb.Pf`, `Tb.Sp`, `Tb.Th`).
- Executed Kruskal-Wallis tests across all 4 groups and pairwise Mann-Whitney $U$ comparisons between spaceflight (`FLT`) and habitat-matched ground controls (`GC`), applying FDR and Holm corrections.
- Audited extreme values and missing records against `LSDS-130_microCT_Cahill_RR1_MicroCt_Data_SUBMITTED.xlsx`.

### Key Findings
- **Trabecular Deterioration in the Femoral Head:** In the `FemoralHead` region, spaceflight (`FLT` vs `GC`) caused a **statistically significant reduction in trabecular bone volume fraction (`bone_volume_total_volume_millimeter_cubed` / `BV/TV`)** and a **significant increase in Trabecular Bone Pattern Factor (`Tb.Pf`)** that remained significant after FDR correction ($\text{FDR} < 0.05$, $\vert{}d\vert{} > 2.0$). Higher `Tb.Pf` indicates a shift from connected plate-like trabeculae to disconnected rod-like structures.
- **Distal Femur & Outliers:** In the `DistalFemur`, `trabecular_thickness_millimeter` (`Tb.Th`) showed a nominal difference between `FLT` and `GC` ($p_{\text{raw}} = 0.0376$, Kruskal-Wallis $p = 0.0252$), but did not pass strict multi-comparison Holm correction across all pairs ($p_{\text{holm}} = 0.188$), largely influenced by a severe low-value outlier in the ground control group (`RR1_GC_M34_DistalFemur`, `Tb.Th = 0.02649 mm`), which was verified as already present in the original author-submitted Excel spreadsheet.

### Limitations
Sample sizes vary by anatomical site ($n=5$ to $10$ per group), and the column named `bone_volume_total_volume_millimeter_cubed` in the transformed CSV corresponds to `BV/TV` (%) in the original submitted spreadsheet (`Sheet1`/`Sheet2`), reflecting a unit-labeling quirk in the repository's transformed file.

---

## 4. Metabolic and Microbial Investigation — OSD-417

### Overview
`OSD-417` (`GLDS-417`, Rodent Research-5) investigates gut microbiome and host serum metabolite alterations associated with bone mineral density loss during spaceflight in mice (`Flight` vs. `Ground Control`, $n=10$ per group for WGS metagenomics).

### Methods
- Programmatically queried the NASA OSDR API (`/geode-py/ws/repo/studies/OSD-417/versions`) to inventory all 1,165 study files and retrieve `OSD-417_metadata_OSD-417-ISA.zip`.
- Analyzed quality control metrics (`MultiQC` / `FastQC` across 40 paired-end reads, 20 base samples: 10 `F` and 10 `GC`).
- Retrieved processed functional metagenomic pathway tables (`GLDS-417_GMetagenomics_Pathway-abundances-cpm_GLmetagenomics.tsv`) and taxonomic profiles (`Metaphlan-taxonomy`), testing pathways related to Axes 2, 3, and 4 between `Flight` (`F`) and `Ground Control` (`GC`) using Mann-Whitney $U$ tests, $\log_2\text{FC}$, Cohen's $d$, and FDR correction.

### Key Findings
- **Study Metadata & Serum Metabolomics Synthesis (`ISA` Archive):** Study documentation confirms elevated abundance of *Lactobacillus murinus* and *Dorea sp.* during spaceflight, enrichment of bacterial gene clusters capable of producing **lactic acid, leucine/isoleucine, and glutathione**, and elevated levels of these same metabolites in host serum via LC-MS/MS, alongside BMD loss, increased osteocalcin, and reduced TRAP5b.
- **Functional Metagenomic Pathways (`HUMAnN3` CPM):**
  - **Axis 2 (Energy/Lactate):** Nominal enrichment ($p_{\text{raw}} < 0.05$) of the hexitol fermentation to lactate, formate, ethanol, and acetate pathway (**`P461-PWY`**) in `Flight`, alongside nominal alterations ($p_{\text{raw}} < 0.05$) in glycolysis (`GLYCOLYSIS-E-D`) and pyruvate fermentation pathways (`P108-PWY`, `PWY-7111`, `PWY-8086`).
  - **Axis 3 (Redox/Pentose Phosphate):** Nominal reduction ($p_{\text{raw}} < 0.05$) in the non-oxidative branch of the pentose phosphate pathway (**`NONOXIPENT-PWY`**).
  - **Axis 4 (BCAA / Isoleucine):** Nominal alteration ($p_{\text{raw}} < 0.05$) in the L-isoleucine biosynthesis IV pathway (**`PWY-5104`**).
- **Statistical Distinction (Raw $p$ vs. FDR):** While these microbial pathways show clear nominal differences ($p_{\text{raw}} < 0.05$) and large effect sizes ($\vert{}d\vert{} > 1.0$), their FDR-adjusted $p$-values exceed $0.05$ due to the high dimensionality of metagenomic pathway testing. They are therefore reported as **nominally significant mechanistic leads** rather than FDR-confirmed discoveries.

---

## 5. Complementary Epigenetic Investigation — GSE276323 & GSE206008
- **GSE276323 (`OSD-943`):** Explored normalized DNA methylation beta values across `776,047` CpG loci in 6 samples (`GSM8496586`–`GSM8496591`), verifying data completeness (`0` missing values, bimodal beta distribution with mean $\approx 0.594$, inter-sample correlation $r > 0.99$). Serves as a complementary layer for candidate epigenetic regulation (`FBLIM1`, `IHH`, `SCAMP2`).
- **GSE206008 (`OSD-539`):** Identified as a complementary dataset for short-term parabolic flight gene expression in cartilage-differentiated cells.

---

## Integrated Synthesis Across the 4 Biological Axes

By standardizing effect sizes (Cohen's $d$) across structural (`OSD-804`, `OSD-608`), molecular (`GSE100930`), and metabolic/microbial (`OSD-417`) layers, the project identified a coherent biological network associated with microgravity-induced bone loss:

| Biological Axis | Structural Evidence (`OSD-804` / `OSD-608`) | Molecular Evidence in `hBMSCs` (`GSE100930`) | Metabolic & Microbial Evidence (`OSD-417`) |
| :--- | :--- | :--- | :--- |
| **1. Bone Formation & Remodeling** | **$\downarrow$ `BV/TV`** & **$\uparrow$ `Tb.Pf`** in Femoral Head (`OSD-804`, $\text{FDR} < 0.05$); **$\downarrow$ Trabecular BMD** at 1, 2, and 4 wks (`OSD-608`, $-30.06\%$, $\text{FDR} < 0.05$). | **$\uparrow$ `SOST`** (Wnt inhibitor) & **$\uparrow$ `TNFSF11` (RANKL)** ($\text{FDR} < 0.05$); **$\downarrow$ `ALPL`** in osteogenic medium; blunted osteogenic PCA separation. | BMD loss accompanied by altered serum osteocalcin and reduced TRAP5b in RR-5 mice. |
| **2. Energy & Glycolytic Metabolism** | — | **$\uparrow$ `LDHA`**, **$\uparrow$ `HK2`**, **$\uparrow$ `PKM`** & **$\downarrow$ `LDHB`**, **$\downarrow$ `HIF1A`** ($\text{FDR} < 0.05$); increased `LDHA/LDHB` lactate-production ratio. | **$\uparrow$ `P461-PWY`** (fermentation to lactate, $p_{\text{raw}} < 0.05$), altered glycolysis/pyruvate pathways, and elevated host serum **lactic acid**. |
| **3. Oxidative Stress & Glutathione** | — | **$\downarrow$ `GCLC`** (rate-limiting GSH synthesis) & **$\downarrow$ `SOD1` / `SOD2`** ($\text{FDR} < 0.05$); compensatory **$\uparrow$ `GSR`** & **$\uparrow$ `CAT`**. | **$\downarrow$ `NONOXIPENT-PWY`** ($p_{\text{raw}} < 0.05$) and altered host serum **glutathione** levels. |
| **4. Amino Acid (BCAA) Metabolism** | — | **$\downarrow$ `SLC7A5`** (leucine uptake) & **$\downarrow$ `ATF4`** ($\text{FDR} < 0.05$); **$\uparrow$ `BCAT1` / `BCAT2`** (BCAA degradation) & **$\uparrow$ `EIF4EBP1`** ($\text{FDR} < 0.05$). | Altered **L-isoleucine biosynthesis (`PWY-5104`**, $p_{\text{raw}} < 0.05$) and elevated host serum **leucine/isoleucine**. |

---

## Methodology and Tools
Analyses were conducted in Python using Google Colab notebooks:
- **Pandas & NumPy:** Data wrangling, multi-header parsing, metadata extraction, and log/Z-score standardization.
- **SciPy (`scipy.stats`):** Welch's $t$-test (`ttest_ind`), Mann-Whitney $U$ test (`mannwhitneyu`), and Kruskal-Wallis $H$ test (`kruskal`).
- **Statsmodels (`multipletests`):** Multiple-testing correction using Benjamini-Hochberg (`fdr_bh`) and Holm-Bonferroni (`holm`).
- **Scikit-learn:** `StandardScaler` and Principal Component Analysis (`PCA`).
- **Matplotlib & Seaborn:** Multi-layer forest plots, Z-score transcriptional heatmaps, longitudinal error-bar plots, and anatomical boxplots.
- **NASA OSDR API & NCBI GEO FTP:** Automated programmatic retrieval of study versions, signed S3 URLs, and expression/annotation matrices.

---

## General Limitations
1. **No Confirmed Individual-Level Predictive Dataset:** Because molecular, metabolic, and structural measurements come from different experiments and species (`Homo sapiens` *in vitro* cells vs. *Mus musculus* and *Rattus norvegicus* *in vivo* models), findings represent **cross-study biological convergence** rather than longitudinal prediction in the same organism.
2. **Sample Size Constraints:** Subgroup sizes in spaceflight studies (`n=3` to `4` in `GSE100930`; `n=5` to `10` in `OSD-804` and `OSD-417`) limit statistical power after multiple-testing penalties.
3. **Nominal vs. FDR Significance:** Metagenomic pathway differences in `OSD-417` achieved nominal significance ($p_{\text{raw}} < 0.05$) but did not pass strict 5% FDR thresholds across all microbiome pathways, and are therefore treated as hypothesis-generating leads.
4. **Data Artifacts Audited:** Specific repository discrepancies (such as the week-4 BMD value for rat `515406` in `OSD-608` and the `M34` outlier in `OSD-804`) were documented and retained transparently.

---

## Repository Structure
- `GSE100933.ipynb` — Exploratory analysis, PCA, and probe annotation of `GSE100930` / `GSE100931` (`hBMSCs` aboard the ISS).
- `OSD_608.ipynb` — Longitudinal pQCT bone mineral density analysis and data consistency audit (`LSDS-41`).
- `OSD_804.ipynb` — 3D micro-CT structural analysis across five bone regions (`LSDS-130` / RR-1).
- `OSD_417.ipynb` — NASA OSDR API exploration, FastQC/MultiQC quality metrics, and ISA metadata extraction (`GLDS-417` / RR-5).
- `GSE276323.ipynb` — Exploratory analysis of astronaut DNA methylation beta distributions (`OSD-943`).
- `Integracao_4_Eixos.ipynb` — **Master Integrative Notebook** combining automated data retrieval, multi-axis statistical testing, FDR/Holm corrections, and multi-layer visualizations.
- `sintese_integrada_microgravidade_4_eixos.csv` — Consolidated results table containing standardized effect sizes (Cohen's $d$), raw $p$-values, and FDR/Holm-adjusted $p$-values across all four biological axes.

---

## References and Data Access
- **GSE100930 / GSE100933 / GPL6244** — [NCBI GEO](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE100930) | [NASA OSDR OSD-546](https://osdr.nasa.gov/bio/repo/data/studies/OSD-546)
- **OSD-608 (LSDS-41)** — [NASA OSDR](https://osdr.nasa.gov/bio/repo/data/studies/OSD-608)
- **OSD-804 (LSDS-130)** — [NASA OSDR](https://osdr.nasa.gov/bio/repo/data/studies/OSD-804)
- **OSD-417 (GLDS-417)** — [NASA OSDR](https://osdr.nasa.gov/bio/repo/data/studies/OSD-417) | Bedree et al. (*Cell Reports*, 2023, DOI: `10.1016/j.celrep.2023.112299`)
- **GSE276323 (OSD-943)** — [NCBI GEO](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE276323)
- **GSE206008 (OSD-539)** — [NCBI GEO](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE206008)

*Disclaimer: This repository documents an exploratory and integrative research project. Statistical findings distinguish between FDR-corrected significance and nominal leads, and all interpretations respect the methodological boundaries between independent experimental models.*
