# Data Augmentation for Enhancing SQL Query Generation: A Natural Language Processing Approach

_Data augmentation for Text-to-SQL with NatSQL and T5-base on the Spider benchmark._

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](
https://colab.research.google.com/github/shalitha23CSE/text-to-sql-augmentation/blob/main/text_to_sql_augmentation.ipynb
)

This repository contains the source code and Google Colab notebook associated 
with the BSc thesis:

> **Data Augmentation for Enhancing SQL Query Generation:  
> A Natural Language Processing Approach**  
> E. W. S. Anuradha, 2026  

---

## Contents

| File                              | Description                                                        |
|-----------------------------------|--------------------------------------------------------------------|
| `text_to_sql_augmentation.ipynb`  | Main Colab notebook: preprocessing (Tok+Comp, ContextTok, AliasNorm), training, and evaluation |
| `README.md`                       | Project overview and usage instructions                           |
| `LICENSE`                         | MIT License for this repository                                   |
---

## How to Run

1. Open the notebook in Google Colab (use the **Open in Colab** badge above).
2. In Colab, go to **Runtime → Change runtime type**:
   - Set **Hardware accelerator** to **GPU**,
   - Select an **A100 High-RAM** runtime if available.
3. Restart the runtime.
4. Run the code cells sequentially from top to bottom, without skipping cells.
   - The setup cells will automatically install all required Python packages.
5. Follow the section headers in the notebook to train all stages and run evaluation.

---

## Dataset

This work is evaluated on the Spider Text-to-SQL benchmark:

- Spider: https://yale-lily.github.io/spider

You must obtain and use the dataset under its original license and terms.

---

## Requirements

The notebook is designed to run on **Google Colab** with GPU enabled.

**Tested configuration (recommended):**
- Colab Pro/Pro+ runtime with **NVIDIA A100 (High RAM)** GPU

The experiments and results reported in the thesis were obtained using this
configuration. Other GPUs such as T4 or L4 may work but may require smaller
batch sizes or fewer epochs to avoid out-of-memory errors.

---

## Key Results (Spider dev set)

Single-seed evaluation on the Spider validation set (1,034 examples).

| Stage | Description | EM (%) | Token F1 (%) | ΔEM vs Baseline |
|-------|-------------|--------|--------------|-----------------|
| 1. Baseline | Raw NatSQL, no augmentation | 6.09 | 63.42 | — |
| 2. Tok+Comp | Token preprocessing + boundary markers | 8.32 | 68.96 | +2.22 |
| 3. Tok+Comp + ContextTok | + schema-aware contextual token splitting | 23.50 | 70.92 | +17.41 |
| 4. Tok+Comp + AliasNorm | + alias normalization (no ContextTok) | **77.76** | **92.79** | +71.66 |
| 5. Tok+Comp + ContextTok + AliasNorm | Full pipeline | 77.27 | 92.50 | +71.18 |

**Key findings**

- AliasNorm is the dominant augmentation, yielding the largest EM improvement.
- ContextTok alone (Stage 3) is seed-sensitive and less stable without AliasNorm.
- The full pipeline (Stage 5) matches Stage 4 performance but does not consistently exceed it.

For detailed multi-seed analysis, ablation study, and error breakdown, see the thesis document.

---

## Citation

If you use this code or the reported results, please cite:

> E. W. S. Anuradha,  
> _Data Augmentation for Enhancing SQL Query Generation:  
> A Natural Language Processing Approach_,  
> BSc Thesis, Computer Science and Engineering, University of Moratuwa, 2026.

---

## License

> This repository is released under the MIT License. See `LICENSE` for details.
