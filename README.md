# LS-ViT: Least-Squares Hessian Based Block Reconstruction for Low-Bit Post-Training Quantization of Vision Transformers
This is the repository for the CVPR 2026 paper "[LS-ViT: Least-Squares Hessian Based Block Reconstruction for Low-Bit Post-Training Quantization of Vision Transformers](https://openaccess.thecvf.com/content/CVPR2026/papers/Hwang_LS-ViT_Least-Squares_Hessian_Based_Block_Reconstruction_for_Low-Bit_Post-Training_Quantization_CVPR_2026_paper.pdf)".

The implementation of our proposed method is built upon the official codebase of [FIMA-Q](https://github.com/ShiheWang/FIMA-Q/tree/main). We sincerely thank the authors for providing their codebase.

## Contents
`utils/block_recon.py` includes the implementation of the Least-Squares Hessian for LS-ViT.

## Usage
```bash
python test_quant.py --model <MODEL> --config <CONFIG_FILE> --dataset <DATA_DIR> [--calibrate] [--load-calibrate-checkpoint <CALIB_CKPT>] [--optimize]
```

- `--model <MODEL>`: Model architecture, which can be `deit_tiny`, `deit_small`, `deit_base`, `vit_tiny`, `vit_small`, `vit_base`, `swin_tiny`, `swin_small` and `swin_base`.

- `--config <CONFIG_FILE>`: Path to the model quantization configuration file.

- `--dataset <DATA_DIR>`: Path to ImageNet dataset.

- `--calibrate` and `--load-calibrate-checkpoint <CALIB_CKPT>`: A `mutually_exclusive_group` to choose between quantizing an existing model or directly load a calibrated model. The default selection is `--calibrate`.

- `--optimize`: Whether to perform Adaround optimization after calibration.




Example: Optimize the model after calibration.

```bash
python test_quant.py --model swin_small --config ./configs/w2a3.py --dataset ~/data/ILSVRC/Data/CLS-LOC --val-batch-size 500 --calibrate --optimize --optim-metric lsvit
```

## Results

Reported results on ImageNet-1K from the original paper are shown below. We also provide checkpoints from our reproduced experiments.  


| Methods     | Bits (W/A) | ViT-S | ViT-B | DeiT-T | DeiT-S | DeiT-B | Swin-S | Swin-B | Checkpoint |
|------------|------------|------:|------:|------:|------:|------:|------:|------:|:----------:|
| Full Prec. | 32/32      | 81.39 | 84.54 | 72.71 | 79.85 | 81.80 | 83.23 | 85.27 | - |
| LS-ViT     | 4/4        | 76.67 | 83.08 | 67.05 | 76.89 | 80.41 | 81.82 | 83.62 |[Download](https://drive.google.com/drive/folders/11IxoKMpn94w0uEbxGfJt0U24M-PLe1zl?usp=drive_link) |
| LS-ViT     | 3/3        | 64.10 | 77.65 | 55.72 | 69.41 | 76.57 | 77.39 | 79.40 |[Download](https://drive.google.com/drive/folders/18YGf4KnoCX4XWsjpCO2JTYdu1Mto58g7?usp=drive_link) |
| LS-ViT     | 2/4        | 58.48 | 74.91 | 52.12 | 65.66 | 73.78 | 73.89 | 74.95 |[Download](https://drive.google.com/drive/folders/1Ooco6YH-3A3_tEno2GNgDf0K-VUxazFL?usp=drive_link) |
| LS-ViT     | 2/3        | 42.05 | 62.89 | 39.28 | 53.86 | 67.06 | 65.77 | 67.73 |[Download](https://drive.google.com/drive/folders/1vtJAe1PWsUc1xBTVLJCCDqb0For4ta2C?usp=drive_link) |

*Note: The reproduced results may slightly differ from the reported numbers due to random calibration set sampling and minor variations in the reproduction environment.*

## Citation
```bibtex
@InProceedings{Hwang_2026_CVPR,
    author    = {Hwang, Hyunha and Nguyen, Xuan Truong and Lee, Hyuk-Jae},
    title     = {LS-ViT: Least-Squares Hessian Based Block Reconstruction for Low-Bit Post-Training Quantization of Vision Transformers},
    booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
    month     = {June},
    year      = {2026},
    pages     = {33588-33597}
}
```
