# Audio examples

The rendered audio examples are **not stored in this repository**. They live in the separate
listening repository, which also hosts the browsable listening page:

- **Listening page:** https://hfossdal.github.io/time-stretch-listening/
- **Repository:** https://github.com/HFossdal/time-stretch-listening

That repository is the canonical home for the rendered audio evidence behind the
time-stretching claims in the thesis. This folder exists only as a pointer so the code
repository stays self-explanatory.

## What is in the listening repository

The audio is organized by evaluation condition rather than by thesis prose:

- **Curated comparison** — the same held-out speech and music excerpts rendered with every
  compared method, in both the 1× inpainting and stretch (0.75× and 0.50×) settings.
- **Additional speech check** — separate held-out speech excerpts used to check whether the
  speech observations also hold outside the curated examples (1× and 0.50×).

The compared methods are original audio (where redistribution is permitted), linear
interpolation/stretch, the full-skip 2D U-Net, the complex-STFT CRN, and the residual-mined
adapter at the reported α settings.

## Redistribution

The underlying datasets (EARS, LibriTTS, VCTK, and MUSDB18-HQ) keep their own licenses and
terms. In the listening repository, rendered `.wav` files are published only where the
source license permits. Where redistribution is restricted, the listening repository
provides the source identifiers, split information, excerpt boundaries, and generation
commands needed to reproduce each example instead of redistributing the audio.
