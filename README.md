# Data Augmentation for Text-to-SQL

This repository contains the source code and Google Colab notebook associated 
with the BSc thesis:

> **"Data Augmentation for Enhancing SQL Query Generation: A Natural Language Processing Approach"**  
> E. W. S. Anuradha, 2026

## Contents

| File | Description |
|------|-------------|
| `text_to_sql_augmentation.ipynb` | Main Colab notebook: preprocessing (Tok+Comp, ContextTok, AliasNorm), training, and evaluation |

## How to Run

1. Open the notebook in Google Colab: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/shalitha23CSE/text-to-sql-augmentation/blob/main/text_to_sql_augmentation.ipynb)
2. Mount Google Drive when prompted
3. Follow the section headers in the notebook (Stage 1 → Stage 5)

## Dataset

Spider benchmark: [https://yale-lily.github.io/spider](https://yale-lily.github.io/spider)

## Requirements

- Python 3.8+
- PyTorch
- HuggingFace Transformers
- Google Colab (recommended for GPU access)
