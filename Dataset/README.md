# Dataset Information

The datasets used to train and validate this project are not distributed through this repository. It contains no raw clinical images, annotations, patient records, or dataset archives.

Access may be granted only by the dataset owner or originating institution under the applicable ethics, consent, privacy, and license conditions. Researchers should contact the project maintainers or dataset owners with an approved purpose and data-handling plan.

## Dataset Links

| Dataset | Official access page |
| --- | --- |
| APTOS 2019 Blindness Detection | [Kaggle competition page](https://www.kaggle.com/c/aptos2019-blindness-detection) |
| IDRiD — Indian Diabetic Retinopathy Image Dataset | [IEEE DataPort dataset page](https://ieeedataport.org/open-access/indian-diabetic-retinopathy-image-dataset-idrid) |
| DRIVE — Digital Retinal Images for Vessel Extraction | [Grand Challenge dataset page](https://drive.grand-challenge.org/) |
| Messidor-2 | [ADCIS dataset page](https://www.adcis.net/en/third-party/messidor2/) |

These links provide dataset information or access instructions. Users must follow each provider's license, account, citation, privacy, and redistribution requirements.

## Before Augmentation Statistics

| Dataset or task | Known source split | Average images per class |
| --- | --- | --- |
| APTOS DR grading | To be confirmed | To be confirmed |
| IDRiD lesion segmentation | 54 training and 27 test images referenced in the notebook | Not applicable to multilabel pixel masks |
| IDRiD landmark localization | 413 training and 103 test images referenced in the notebook | Not applicable to coordinate regression |
| IDRiD DME | To be confirmed | To be confirmed |
| Retinal vessel segmentation | To be confirmed | Not applicable to binary pixel masks |

## After Augmentation Statistics

The notebooks apply transformations during training, so augmentation does not necessarily create a fixed expanded dataset on disk.

| Dataset or task | Effective augmented-image count | Average images per class |
| --- | --- | --- |
| APTOS DR grading | To be confirmed from the final training run | To be confirmed |
| IDRiD lesion segmentation | Generated dynamically | Not applicable |
| IDRiD landmark localization | Generated dynamically | Not applicable |
| IDRiD DME | To be confirmed | To be confirmed |
| Retinal vessel segmentation | Generated dynamically | Not applicable |

## Class and Target Descriptions

### Diabetic Retinopathy Severity Grading

The APTOS grading workflow uses five severity labels:

- **0 — No DR:** no visible diabetic retinopathy.
- **1 — Mild:** mild non-proliferative diabetic retinopathy.
- **2 — Moderate:** moderate non-proliferative diabetic retinopathy.
- **3 — Severe:** severe non-proliferative diabetic retinopathy.
- **4 — Proliferative DR:** proliferative diabetic retinopathy.

### Retinal Lesion Segmentation

The IDRiD lesion-segmentation workflow uses four lesion masks:

- **MA — Microaneurysms:** small capillary outpouchings that can appear as tiny red dots.
- **HE — Haemorrhages:** retinal bleeding regions.
- **EX — Hard Exudates:** lipid-rich deposits with relatively sharp boundaries.
- **SE — Soft Exudates:** cotton-wool-like lesions associated with localized ischemia.

### Anatomical Landmark Localization

The IDRiD localization workflow predicts two coordinate targets:

- **OD — Optic Disc:** the retinal region where the optic nerve exits the eye.
- **FV — Fovea:** the central macular location responsible for high-acuity vision.

### Retinal Vessel Segmentation

The vessel workflow uses binary pixel labels:

- **Vessel:** retinal blood-vessel pixels.
- **Background:** all non-vessel pixels in the valid retinal field.

### Diabetic Macular Edema

An authoritative DME class dictionary was not present in the supplied folders. The labels must be recovered from the original training pipeline or dataset documentation and must not be inferred from the ONNX filename alone.

Return to the [main README](../README.md).
