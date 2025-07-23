# End-to-End Multichannel Speaker-Attributed ASR (MC-SA-ASR)

This folder contains the code and training scripts for the paper:  
**[End-to-End Multichannel Speaker-Attributed ASR: Speaker Guided Decoder and Input Feature Analysis](https://arxiv.org/abs/2310.10106)** (ASRU 2023).

Our proposed model, **Multichannel Speaker-Attributed ASR (MC-SA-ASR)**, integrates a Conformer-based encoder with multi-frame cross-channel attention and a speaker-attributed Transformer-based decoder.

---

## 🔧 Core Model Implementation

- [TransformerMC_SA_ASR.py](https://github.com/can-cui/speechbrain-related/blob/main/speechbrain/lobes/models/transformer/TransformerMC_SA_ASR.py)

---

## 🧪 LibriSpeech Experiments (Table 1 in the paper)

### Baseline Models

- **SC-SA-ASR (Single-channel Speaker-Attributed ASR)**  
  [`conformer_large_spk.yaml`](https://github.com/can-cui/speechbrain-related/blob/main/recipes/LibriSpeech/ASR/transformer/hparams/conformer_large_spk.yaml)

- **MC-ASR (Multichannel ASR)**  
  [`conformer_large_MC.yaml`](https://github.com/can-cui/speechbrain-related/blob/main/recipes/LibriSpeech/ASR/transformer/hparams/conformer_large_MC.yaml)

### Proposed Model: MC-SA-ASR

- Config file:  
  [`conformer_large_MC_spk.yaml`](https://github.com/can-cui/speechbrain-related/blob/main/recipes/LibriSpeech/ASR/transformer/hparams/conformer_large_MC_spk.yaml)

- Core training script:  
  [`train_dynMix_MC_spk.py`](https://github.com/can-cui/speechbrain-related/blob/main/recipes/LibriSpeech/ASR/transformer/train_dynMix_MC_spk.py)  
  *(also includes dataset generation functions for the multichannel multi-speaker LibriSpeech dataset)*

#### 🔍 Input Feature Settings

In `conformer_large_MC_spk.yaml`:

- **Mel Filter Bank**:  
  Uncomment lines 160–168

- **Magnitude-Phase**:  
  Uncomment lines 171–172  
  Comment out line 177  
  Uncomment line 178

In `train_dynMix_MC_spk.py`:

- **Mel Filter Bank**: uncomment lines 78–97  
- **Magnitude-Phase**: uncomment lines 99–133  

⚠️ **Do not enable both at the same time.**

#### 🛠️ Configuration

- Change **number of channels**: edit `max_mics` in the YAML config  
- Change **number of speakers**: edit `num_spks`  
- If `rand_spk = True`: number of speakers will be randomly sampled between 1 and `num_spks` at each training step

- All training config combinations:  
  [`run.sh`](https://github.com/can-cui/speechbrain-related/blob/main/recipes/LibriSpeech/ASR/transformer/run.sh)

---

## 🎙️ AMI Experiments (Tables 3–5 in the paper)

### Baseline

- **SC-SA-ASR**:  
  [`conformer_large_spk.yaml`](https://github.com/can-cui/speechbrain-related/blob/main/recipes/AMI/ASR/transformer/hparams/conformer_large_spk.yaml)

### Proposed

- **MC-SA-ASR**:  
  [`conformer_large_MC_spk.yaml`](https://github.com/can-cui/speechbrain-related/blob/main/recipes/AMI/ASR/transformer/hparams/conformer_large_MC_spk.yaml)

- All training config combinations:  
  [`run.sh`](https://github.com/can-cui/speechbrain-related/blob/main/recipes/AMI/ASR/transformer/run.sh)

---

## 📖 Citation

If you use this code, please cite the following paper:

```bibtex
@inproceedings{cui2023,
  title={End-to-end Multichannel Speaker-Attributed {ASR}: Speaker Guided Decoder and Input Feature Analysis},
  author={Cui, Can and Sheikh, Imran and Sadeghi, Mostafa and Vincent, Emmanuel},
  booktitle={IEEE Automatic Speech Recognition and Understanding Workshop (ASRU)},
  year={2023},
  pages={1--8},
}
