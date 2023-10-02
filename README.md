# Foundation Models Meet Imbalanced Single-Cell Data When Learning Cell Type Annotations

## Abstarct 
With the emergence of single-cell foundation models, an important question arises: how do these models perform when trained on datasets having an imbalance in cell type distribution due to rare cell types or biased sampling? Using skewed single-cell cell-type distribution, we benchmark foundation models, scGPT, scBERT, and Geneformer, for cell-type annotation. While all models had reduced performance when challenged with rare cell types, scGPT, scBERT, performed better than Geneformer. Notably, in contrast to scGPT and scBERT, Geneformer uses ordinal positions of the tokenized genes rather than actual raw gene expression values. To mitigate the effect of a skewed distribution, we find that random oversampling, but not random undersampling, improved the performance for all three foundation models. Finally, scGPT, using FlashAttention, has the fastest computational speed, whereas scBERT is much more memory-efficient. We conclude that tokenization and data representation are essential areas of research, and new strategies are needed to mitigate the effects of imbalanced learning in single-cell foundation models.

In this repository, we share the code and data for reproducability.

## Setup
Although each foundation model has its own configuration steps, we provide you with a universal configuration as follows:
* Python version: `3.8.17`.
* Cuda version: `11.7`.
* GPU: NVIDIA A100.
* All dependencies are available in `requirements.txt`, just run `pip install -r requirements.txt`.
* To install FlashAttention without any problems, use the Pytorch Docker container. We used Singularity as follows:
  ```
  singularity pull docker://nvcr.io/nvidia/pytorch:22.08-py3
  singularity run --nv pytorch_2.0.0-cuda11.7-cudnn8-devel.sif
  ```

## Models
For simplicity, we provide Jupyter notebooks containing codes for the cell type annotation task for each foundation model inside `models` directory. To access the more broader code for each foundation model and their papers, please refer to the links as follows:
* [scGPT repository](https://github.com/bowang-lab/scGPT), and [scGPT paper](https://www.biorxiv.org/content/10.1101/2023.04.30.538439v2).
* [scBERT repository](https://github.com/TencentAILabHealthcare/scBERT), and [scBERT paper](https://www.nature.com/articles/s42256-022-00534-z).
* [Geneformer repository](https://huggingface.co/ctheodoris/Geneformer), and [Geneformer paper](https://www.nature.com/articles/s41586-023-06139-9).

## Datasets & Preprocessing
Datasets (MS and Zheng68K) and their sampling variations (undersampled, oversampled, and imputed) can be found inside the `data` directory. You can also find the preprocessing code for upsampling, downsampling, imputation, and converting the gene expression matrix into ordinal gene tokens (for Geneformer) in `data/preprocessing.ipynb`.
