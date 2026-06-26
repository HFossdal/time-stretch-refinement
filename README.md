# time-stretch-refinement

Supplementary code and materials for the master's thesis
**Neural Refinement of Interpolated Time-Frequency Representations for Audio Time-Stretching**.

| | |
|---|---|
| **Author** | Håvard Fossdal |
| **Course** | TMA4900 – Industrial Mathematics, Master Thesis |
| **Institution** | Department of Mathematical Sciences, Norwegian University of Science and Technology (NTNU) |
| **Supervisor** | Erlend Aune |
| **Co-supervisor** | Daesoo Lee |
| **Submitted** | June 2026 |
| **Listening examples** | https://hfossdal.github.io/time-stretch-listening/ |

## Overview

This repository accompanies a master's thesis on **audio time-stretching** through
neural refinement of interpolated time-frequency representations. Interpolation
provides a first estimate of the frames between existing frames, and a learned model
then refines that estimate before waveform reconstruction.

The work is studied in two evaluation settings:

1. **Controlled 1× interpolation-refinement** — selected frames are replaced by linear
   interpolation and the model is trained to recover the original representation. Because
   the target is known, this setting supports direct representation-domain metrics.
2. **Rendered time-stretching** — the same refinement methods are inserted into a
   time-stretching pipeline and the output is judged through diagnostic listening, since
   lower representation error does not guarantee better reconstructed sound.

Three learned branches are compared against direct interpolation: a full-skip mel-domain
2D U-Net (reconstructed with the frozen BigVGAN vocoder), a complex-STFT CRN-style U-Net
(reconstructed with inverse STFT), and a residual-mined mel-domain adapter that targets
artifacts remaining after vocoder reconstruction.

## Repository structure

```
time-stretch-refinement/
├── README.md
├── LICENSE                       # MIT (code only; datasets keep their own licenses)
├── requirements.txt
├── notebooks/
│   ├── README.md                 # description and run order for every notebook
│   ├── retained/                 # the four thesis-facing notebooks
│   └── exploratory/              # development-history variants (not in the final comparison)
├── results/
│   ├── metrics/                  # exported metric files behind the controlled 1× tables
│   └── figures/                  # plots corresponding to the thesis figures
└── audio/
    └── README.md                 # source identifiers and redistribution notes for rendered audio
```

## Running the notebooks

The notebooks were developed and run in **Google Colab** (NVIDIA A100 / L4 runtimes) with
data stored on Google Drive. Each notebook mounts Drive and reads from a configurable
`DRIVE_ROOT`, using the shared prepared 70/30 speech/music split directory.

The mel-domain experiments use a frozen **BigVGAN** vocoder. The pretrained checkpoint is
`nvidia/bigvgan_v2_22khz_80band_fmax8k_256x`, and the shared mel frontend is
22.05 kHz, FFT size 1024, hop 256, window 1024, 80 mel bands, mel range 0–8000 Hz.

See [`notebooks/README.md`](notebooks/README.md) for what each notebook does and the
recommended run order.

## Data

The experiments combine speech and music sources:

- **Speech:** EARS, LibriTTS, VCTK
- **Music:** MUSDB18-HQ mixtures

These datasets are **not redistributed here** and remain subject to their original
licenses and terms. The repository documents the splits, source identifiers, and excerpt
boundaries needed to reproduce the comparisons; see [`audio/README.md`](audio/README.md).

## Results and listening material

`results/` holds the exported controlled-metric files and the plots used in the thesis.
Rendered audio examples are the primary evidence for the time-stretching claims. They are
hosted in a separate listening repository rather than in this code repository:

- **Listening page:** https://hfossdal.github.io/time-stretch-listening/
- **Listening repository:** https://github.com/HFossdal/time-stretch-listening

See [`audio/README.md`](audio/README.md) for details.

## Citation

If you refer to this work, please cite the thesis:

```bibtex
@mastersthesis{fossdal2026timestretch,
  author = {Håvard Fossdal},
  title  = {Neural Refinement of Interpolated Time-Frequency Representations for Audio Time-Stretching},
  school = {Norwegian University of Science and Technology (NTNU)},
  year   = {2026},
  note   = {TMA4900 -- Industrial Mathematics, Master Thesis}
}
```

## License

The code in this repository is released under the [MIT License](LICENSE). The datasets and
the pretrained BigVGAN vocoder are covered by their own respective licenses.
