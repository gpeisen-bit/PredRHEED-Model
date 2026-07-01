# PredRHEED

Model code for **PredRHEED**, a cascaded deep-learning framework for in situ RHEED
monitoring during ScAlN molecular beam epitaxy. It pairs a surface-state classifier
with a future-frame predictor, so the upcoming surface state can be recognized about
5-30 seconds before it is directly observed.

This repository contains the model code and the cascade only. Datasets and trained
weights are available from the corresponding author upon reasonable request.

## Models

Classification, three surface states (streaky, transition, spotty).

- `classification/cnn_transformer.ipynb`. CNN-Transformer hybrid classifier.
- `classification/cnn.ipynb`. CNN baseline.
- `classification/transformer.ipynb`. Transformer baseline.

Future-frame prediction.

- `prediction/msam_convlstm.ipynb`. MSAM-ConvLSTM predictor.
- `prediction/sa_convlstm.ipynb`. SA-ConvLSTM baseline.
- `prediction/simvp.py`. SimVP baseline.

## Cascade

- `cascade/cascade_inference.py`. Runs the predictor and then the classifier on the predicted frames to give the anticipated surface state. See the paper for the full protocol.

```
python cascade/cascade_inference.py --predictor msam_convlstm.pth --classifier cnn_transformer.pth --frames window15.npy
```

## Environment

Python 3.10, PyTorch 2.9.1 with CUDA 13.0, single NVIDIA RTX 5090, global seed 2025.
Install with `pip install -r requirements.txt`.

## Citation

P. Gao, M. M. H. Tanim, W. Wang, G. Baker, J. Chen, Z. Wang, J. Liu, Y. Wei,
D. Wang, Q. Qu, Z. Mi. Deep Learning Assisted Prediction of Reflection High-Energy
Electron Diffraction Patterns During Heteroepitaxy.
