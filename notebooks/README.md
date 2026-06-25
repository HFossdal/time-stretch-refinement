# Notebooks

The notebooks were developed and run in **Google Colab** with data on Google Drive.
Each notebook mounts Drive, reads from a configurable `DRIVE_ROOT`, and uses the shared
prepared 70/30 speech/music split directory. Code outputs and execution counts are cleared.

The notebooks are split into the four **retained** notebooks behind the thesis's final
comparison and the **exploratory** variants that document the development path.

## `retained/`

These four notebooks correspond to the final compared methods and the evaluation.

| Notebook | Purpose |
|---|---|
| `fullskip_mel_unet_large_data_training.ipynb` | Trains the retained full-skip mel-domain 2D U-Net — the main learned mel refiner. |
| `residual_mined_bigvgan_adapter_training.ipynb` | Trains the residual-mined BigVGAN adapter, which targets post-vocoder artifacts. Uses a frozen earlier mel U-Net as context. |
| `complex_stft_crn_training.ipynb` | Trains the complex-STFT CRN-style U-Net — the main STFT-domain comparison, reconstructed with inverse STFT. |
| `main_listening_and_metric_evaluation.ipynb` | Renders the listening examples and computes the controlled 1× metrics for the final comparison. |

**Suggested run order:**

1. `fullskip_mel_unet_large_data_training.ipynb` — base mel U-Net.
2. `residual_mined_bigvgan_adapter_training.ipynb` — needs a trained mel U-Net checkpoint as context.
3. `complex_stft_crn_training.ipynb` — independent of the mel branches.
4. `main_listening_and_metric_evaluation.ipynb` — loads the frozen checkpoints and produces the metrics and listening examples.

Checkpoint prefixes and manual checkpoint paths are configuration fields in each notebook,
not fixed assumptions.

## `exploratory/`

These sixteen notebooks are development history. They are documented in the thesis as
exploratory implementation families and are **not** part of the final reported comparison.
They show which modeling directions were tried before the comparison was narrowed to the
retained set.

- Adversarial and vocoder-aware mel U-Net variants:
  `mel_unet_bigvgan_auxiliary_loss_training`,
  `mel_unet_discriminator_family_training`,
  `mel_unet_high_frequency_discriminator_training`,
  `mel_unet_vocoder_loop_high_frequency_training`,
  `supervisor_mel_vocoder_loop_high_frequency_training`,
  `discrepancy_guided_vocoder_focus_training`,
  `postvocoder_stft_high_frequency_discriminator_training`,
  `hybrid_bigvgan_vocoder_loop_training`.
- STFT-domain development:
  `complex_stft_unet_training`.
- Hybrid and gated mel–STFT variants:
  `complex_mask_mel_stft_blend_training`,
  `hybrid_mel_complex_fusion_training`,
  `hybrid_mel_complex_fusion_second_variant_training`,
  `mel_dominant_stft_assist_hybrid_training`,
  `melspace_gated_fusion_training`,
  `stretch_aware_melspace_gated_fusion_training`,
  `crn_teacher_melspace_gated_fusion_training`.
