### Ing.Ekaterina Simonova (UCT Prague)

# The application of Deep Learning for cancer subtype identification

## **Abstract:**

Human cancer is a heterogeneous disease initiated by random somatic mutations and driven by multiple genomic alterations. Cancer subtype classification has the potential to significantly improve disease prognosis and move closer toward personalized cancer
treatment and prevention. The assumption behind molecular subtyping is that patients of similar gene expression patterns are likely to have similar responses to therapies and clinical outcomes due to the tumor microenvironment. Thus, molecular subtyping can reveal information valuable for a range of cancer studies from cancer initiation and tumor biology to prognosis and personalized medicine. Molecular subtyping was widely described in breast and colorectal cancer, however, it was not broadly explored in other indications. In this work, molecular subtypes are explored via deep learning models, specifically  autoencoder latent space. The analysis is performed on a range of publicly available datasets such as Gene Expression Omnibus (GEO), The Cancer Genome Atlas (TCGA) and the Molecular Taxonomy of Breast Cancer International Consortium (METABRIC).


![Project overview](./SVK.png)

## **Goals:**

* Prepare the data for modeling
* Implementation of autoencoder
* Clustering of latent space

## **Solution:**

* *Data preparation:* 
    * Convertion of Gene names/Affymetrix/Illumina/Agilent IDs to ENTREZ ID
    * filling of Null values with zero
    * removal of technical variation with conversion of genes to genesets
    * removal of normal tissue expression values from the data
    * checking consistancy of metadata (that contains labels for samples) and gene expression table (contains expression values for each sample)
* *Used models:*
    * Autoencoder
    * IPCA with poly and sigmoid kernels
    * PCA 
    * Baseline model - Data without compression

## **Data:**

* Input data is represented by a matrix, where columns are sample names and rows are ENTREZ ID; in some cases the data were directly downloaded from GEO database with GEOparse package, otherwise data were loaded from cBioPortals; colorectal cancer datasets were loaded from https://synapse.org
* Data collection was the most time consuming step as majority of GEO gene expression datasets have around 100 samples
* A list of datasets used for the project is shown below

| Cancer type | ID        | Technology                | Tissue type   | Normalization                                              | Number of labelled samples |
|-------------|-----------|---------------------------|---------------|------------------------------------------------------------|----------------------------|
| Colorectal  | GSE33113  | Affymetrix HG133plus2     | Fresh frozen  | fRMA                                                       | 80                         |
| Colorectal  | GSE39582  | Affymetrix HG133plus2     | Fresh frozen  | fRMA                                                       | 466                        |
| Colorectal  | KFSYSCC   | Affymetrix HG133plus2     | Fresh frozen  | fRMA                                                       | 229                        |
| Colorectal  | GSE35896  | Affymetrix HG133plus2     | Fresh frozen  | fRMA                                                       | 51                         |
| Colorectal  | PETACC3   | Almac's Affymetrix Array  | FFPE          | fRMA                                                       | 526                        |
| Colorectal  | GSE13067  | Affymetrix HG133plus2     | Fresh frozen  | fRMA                                                       | 56                         |
| Colorectal  | GSE20916  | Affymetrix HG133plus2     | Fresh frozen  | fRMA                                                       | 45                         |
| Colorectal  | GSE23878  | Affymetrix HG133plus2     | Fresh frozen  | fRMA                                                       | 24                         |
| Colorectal  | GSE14333  | Affymetrix HG133plus2     | Fresh frozen  | fRMA                                                       | 129                        |
| Colorectal  | GSE2109   | Affymetrix HG133plus2     | Fresh frozen  | RMA                                                        | 244                        |
| Colorectal  | GSE17536  | Affymetrix HG133plus2     | Fresh frozen  | fRMA                                                       | 147                        |
| Colorectal  | GSE13294  | Affymetrix HG133plus2     | Fresh frozen  | fRMA                                                       | 124                        |
| Colorectal  | GSE37892  | Affymetrix HG133plus2     | Fresh frozen  | fRMA                                                       | 107                        |
| Colorectal  | TCGA      | Illumina Array            | Primary Tumor | RSEM                                                       | 207                        |
| Breast      | GSE96058  | RNA sequencing            | Primary Tumor | FPKM                                                       | 3273                       |
| Breast      | GSE21653  | Affymetrix HG133plus2     | Primary Tumor | RMA and quantile normalization                             | 242                        |
| Breast      | GSE48390  | Affymetrix HG133plus2     | Primary Tumor | RMA and quantile normalization                             | 74                         |
| Breast      | GSE65194  | Affymetrix HG133plus2     | Primary Tumor | GC-RMA log2	                                                | 98                         |
| Breast      | GSE81538  | RNA sequencing            | Primary Tumor | FPKM                                                       | 405                        |
| Breast      | ROCK      | Affymetrix HG133plus2     | Primary Tumor | log2_RMA                                                   | 1468                       |
| Breast      | METABRIC  | Illumina Array            | Primary Tumor | N/A                                                        | 1898                       |
| Breast      | TCGA      | RNA sequencing            | Primary Tumor | RSEM                                                       | 981                        |
| Breast      | CPTAC     | RNA sequencing            | Primary Tumor | TPM                                                        | 122                        |
| Breast      | SMC       | RNA sequencing            | Primary Tumor | TPM                                                        | 168                        |
| Breast      | NKI       | Agilent Rosetta Array     | Primary Tumor | N/A                                                        | 337                        |
| Breast      | TRANSBIG  | Affymetrix HG U133A Array | Primary Tumor | MAS5 normalized                                            | 198                        |
| Breast      | UPP       | Affymetrix HG U133A Array | Primary Tumor | log transformed and scaled by adjusting the mean intensity | 190                        |
| Breast      | UNT       | Affymetrix HG U133A Array | Primary Tumor | RMA                                                        | 137                        |
| Breast      | GSE60789  | Illumina Array            | Primary Tumor | Illumina BeadStudio software                               | 110                        |
| Breast      | GSE59595  | Illumina Array            | Primary Tumor | RSN.                                                       | 190                        |
| Breast      | GSE58215  | Agilent Array             | Primary Tumor | log2-transformed and quantile normalize                    | 283                        |
| Breast      | GSE53031  | Affymetrix HG 219 Array   | Primary Tumor | RMA                                                        | 167                        |
| Breast      | GSE56493  | Rosetta/Merck HG2plus2    | FNA           | RMA                                                        | 120                        |
| Breast      | GSE78958  | Affymetrix HG133plus2     | Primary Tumor | Partek Genomics Suite software                             | 424                        |
| Breast      | GSE25066  | Affymetrix HG133plus2     | Primary Tumor | MAS5 normalized and log2 transformed                       | 508                        |
| Breast      | GSE21653  | Affymetrix HG133plus2     | Primary Tumor | RMA and quantile normalization                             | 242                        |
| Breast      | GSE48390  | Affymetrix HG133plus2     | Primary Tumor | RMA                                                        | 74                         |
| Breast      | GSE20711  | Affymetrix HG133plus2     | Primary Tumor | RMA                                                        | 88                         |
| Breast      | GSE45827  | Affymetrix HG133plus2     | Primary Tumor | REML                                                       | 130                        |
| Breast      | GSE135298 | RNA sequencing            | Primary Tumor | FPKM                                                       | 93                         |
| Breast      | GSE25066  | Affymetrix HG U133A Array | Primary Tumor | MAS5 normalized                                            | 105                        |
| Breast      | GSE80999  | Agilent Array             | Primary Tumor | log2-transformed and quantile normalize                    | 283                        |

*Tissue types:* 

* FFPE - a formalin-fixed paraffin-embedded tissue
* FNA - a fine needle aspiration biopsy.

*Normalization:*

* FPKM - Fragments Per Kilobase per Million mapped fragments
* REML - Restricted Maximum Likelihood
* (f)RMA - (frozen) Robust Multi-array Average
* RSEM - RNA-Seq by Expectation-Maximization
* RSN - Robust Spline Normalization

# Autoencoder models parameters:

|   | Inicialization       | Optimizer | Learn rate    | Layers                   | Epoch | Batch |   Silhouette  |       DB       | Loss / Val loss |
|---|----------------------|-----------|---------------|--------------------------|:-----:|:-----:|:-------------:|:--------------:|:---------------:|
| 1 | Variance Scaling 1/2 | SGD       | 0.2, Nesterov | [22596, 1000, 500, 128]  | 150   | 128   | -0.08+/-0.05  | 19.48+/- 6.99  | 0.03, 0.03      |
| 2 | Variance Scaling 1/2 | SGD       | 0.2, Nesterov | [22596, 128]             | 50    | 128   | -0.03+/-0.02  | 18.86+/-4.98   | 0.03, 0.03      |
| 3 | Variance Scaling 1/2 | SGD       | 0.2, Nesterov | [22576, 4000, 128]       | 100   | 128   | -0.04 +/-0.03 | 17.59 +/- 4.85 | 0.02, 0.02      |
| 4 | Variance Scaling 1/2 | SGD       | 0.2, Nesterov | [22596, 4000, 500, 64]   | 200   | 64    | -0.05+/-0.04  | 18.43+/- 5.75  | 0.03, 0.03      |
| 5 | Variance Scaling 1/2 | SGD       | 0.2, Nesterov | [22596, 4000, 2500, 128] | 150   | 256   | -0.06+/-0.04  | 18.55+/-6.33   | 0.02, 0.02      |

## Environment

* I used Google Colab CPU/GPU/High-RAM for running my code; one of my precesses (FunctionalSpectra class) was run locally on server with 1 TB RAM and 88 CPUs in order to speed up calculations; some other calculations that required more RAM were also running on the server.
* As many packages for gene expression analysis were written in R - r2py package was used to run R code in Python

## **Instructions for running the notebook:**

All notebooks are in notebooks folder:

*Preprocessing of the data:*
* BRCA (Breast) cBioPortals - [01a_BreastCancerSubtyping](notebooks/01a_BreastCancerSubtyping.ipynb)
* BRCA (Breast) GEO datasets - [01b_BreastCancerSubtypingGEO](notebooks/01b_BreastCancerSubtypingGEO.ipynb)
* CRC (Colorectal) - [01_ColorectalCancerSubtypeIdentification](notebooks/01_ColorectalCancerSubtypeIdentification.ipynb)

*Data splitting:* - [02b_split_train_test](notebooks/02b_split_train_test.ipynb)

*Baseline model implemetation:* - [03b_baseline_model](notebooks/03b_baseline_model.ipynb)

*Autoencoder implementation:* -  [03a_autoencoder_cancercells_expression](notebooks/03a_autoencoder_cancercells_expression.ipynb)

*A dataset used for baseline model implementation and autoencoder implemetation can be downloaded from here:*

https://drive.google.com/file/d/1vRbdlC7rT0npaxc4FrechFXUVtY8f45C/view?usp=sharing


To run it the script locally please ensure that you have at least 25 GB RAM.

## Summary presentation

**[Link](https://docs.google.com/presentation/d/1kA_77nYGWFi9jFi1xnQ4wwW6OjVK65CqiB4dKd9-bYY/edit?usp=sharing) for presentation** 


