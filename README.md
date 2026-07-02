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

Multi-seed evaluation (3 seeds) on the Spider validation set (1,034 examples).  
Results reported as **mean ± standard deviation** across seeds.

| Stage | Description | EM (%) | Token F1 (%) | ΔEM vs Baseline |
|-------|-------------|--------|--------------|-----------------|
| 1. Baseline (T5–NatSQL) | Raw NatSQL, no augmentation | 4.55 ± 3.27 | 43.34 ± 30.67 | — |
| 2. Tok+Comp | Token preprocessing + boundary markers | 8.51 ± 0.16 | 68.51 ± 0.32 | +3.96 |
| 3. Tok+Comp + ContextTok | + schema-aware contextual token splitting | 15.60 ± 11.05 | 46.84 ± 33.12 | +11.05 |
| 4. Tok+Comp + AliasNorm | + alias normalization (no ContextTok) | **78.27 ± 0.73** | **92.79 ± 0.07** | **+73.72** |
| 5. Tok+Comp + ContextTok + AliasNorm | Full pipeline | 77.56 ± 0.85 | 92.59 ± 0.09 | +73.01 |

**Key findings**

- AliasNorm is the dominant augmentation, yielding the largest and most stable EM improvement.
- ContextTok alone (Stage 3) is seed-sensitive — high variance (±11.05 EM, ±33.12 F1) without AliasNorm.
- The full pipeline (Stage 5) matches Stage 4 performance but does not consistently exceed it.
- Tok+Comp (Stage 2) substantially reduces variance compared to the baseline, confirming its stabilising effect.

For detailed ablation study, difficulty-level breakdown, and error analysis, see the thesis document.

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
