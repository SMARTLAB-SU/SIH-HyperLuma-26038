# HyperLuma: Multi-Task Retinal Image Analysis

HyperLuma is a research-oriented deep-learning project for analyzing retinal fundus images. The supplied work covers diabetic retinopathy severity grading, retinal lesion segmentation, optic-disc and fovea localization, diabetic macular edema inference, and retinal vessel segmentation.

This repository consolidates the supplied Jupyter notebooks and deployment-ready ONNX checkpoints into the required Smart India Hackathon structure. Raw clinical images and annotations are intentionally excluded.

## Problem Statement

Retinal diseases can cause preventable visual impairment when they are not identified and assessed early. Manual examination is specialist-intensive, and a complete assessment may require several complementary tasks: disease grading, lesion delineation, anatomical landmark localization, and vessel segmentation.

## Proposed Solution

HyperLuma uses task-specific convolutional neural networks to support multiple retinal-analysis workflows:

- five-class diabetic retinopathy severity grading;
- segmentation of microaneurysms, haemorrhages, hard exudates, and soft exudates;
- localization of the optic disc and fovea;
- diabetic macular edema inference; and
- binary retinal vessel segmentation.

The notebooks contain the available training and evaluation workflows. The `Model` directory contains the supplied ONNX checkpoints for portable inference.

## Repository Structure

```text
SIH-HyperLuma-SIH26038/
|-- Dataset/
|   `-- README.md
|-- Model/
|   |-- aptos_resnet34_fast_best.onnx
|   |-- idrid_densenet121_attention_unet_best.onnx
|   |-- idrid_densenet121_localization_best.onnx
|   |-- idrid_dme_densenet121_best_macro_f1.onnx
|   `-- vessel_densenet121_attention_unet_final.onnx
|-- SRC/
|   |-- Installer/
|   |-- aptos_resnet34_dr_grading.ipynb
|   |-- aptos_resnet50_dr_grading.ipynb
|   |-- idrid_lesion_segmentation_densenet121.ipynb
|   |-- idrid_localization_densenet121.ipynb
|   `-- retinal_vessel_segmentation_densenet121.ipynb
|-- Screenshot/
|-- Documentation/
|-- LICENSE
|-- requirements.txt
`-- README.md
```

`SRC/Installer`, `Screenshot`, and `Documentation` are currently empty because the supplied source folders contained no installer, media, report, paper, or presentation files.

## Models

| Model file | Task | Related notebook |
| --- | --- | --- |
| `aptos_resnet34_fast_best.onnx` | APTOS diabetic retinopathy severity grading | `aptos_resnet34_dr_grading.ipynb` |
| `idrid_densenet121_attention_unet_best.onnx` | IDRiD retinal lesion segmentation | `idrid_lesion_segmentation_densenet121.ipynb` |
| `idrid_densenet121_localization_best.onnx` | IDRiD optic-disc and fovea localization | `idrid_localization_densenet121.ipynb` |
| `idrid_dme_densenet121_best_macro_f1.onnx` | Diabetic macular edema inference | Not supplied |
| `vessel_densenet121_attention_unet_final.onnx` | Retinal vessel segmentation | `retinal_vessel_segmentation_densenet121.ipynb` |

The supplied ResNet50 APTOS notebook is an additional grading experiment; its architecture does not match the supplied ResNet34 ONNX checkpoint.

## Installation

Python 3.10 or 3.11 is recommended. Create and activate a virtual environment, then install the combined dependencies:

```bash
pip install -r requirements.txt
```

For notebook work, start JupyterLab from the repository root:

```bash
jupyter lab
```

## Usage

1. Obtain authorized access to the required datasets.
2. Update dataset paths and environment-specific settings in the relevant notebook.
3. Review preprocessing, image size, label mapping, and normalization before training or inference.
4. Run the selected notebook from `SRC` for experimentation or evaluation.
5. For deployment, load the matching checkpoint from `Model` with ONNX Runtime and supply input tensors using the preprocessing defined by its related notebook.

Example model-loading pattern:

```python
import onnxruntime as ort

session = ort.InferenceSession("Model/aptos_resnet34_fast_best.onnx")
input_name = session.get_inputs()[0].name
# outputs = session.run(None, {input_name: preprocessed_batch})
```

The DME checkpoint does not have a supplied training notebook. Its exact input preprocessing, label dictionary, and decision logic must be confirmed before use.

## Dataset

No raw dataset is included. The project references the following retinal-image datasets:

- [APTOS 2019 Blindness Detection](https://www.kaggle.com/c/aptos2019-blindness-detection)
- [IDRiD — Indian Diabetic Retinopathy Image Dataset](https://ieeedataport.org/open-access/indian-diabetic-retinopathy-image-dataset-idrid)
- [DRIVE — Digital Retinal Images for Vessel Extraction](https://drive.grand-challenge.org/)
- [Messidor-2](https://www.adcis.net/en/third-party/messidor2/)

Access requirements, available statistics, and known class definitions are documented in [Dataset/README.md](Dataset/README.md).

## Reported Results

The following values were extracted from saved notebook outputs. They have not been independently reproduced during repository assembly.

| Task | Reported result |
| --- | --- |
| APTOS ResNet34 grading | Test accuracy 0.81199; macro F1 0.62895; quadratic weighted kappa 0.91342 |
| IDRiD lesion segmentation | Test macro Dice 0.62811; test macro IoU 0.46915 |
| IDRiD landmark localization | Test macro mean NME 0.005989; macro mean error 30.831619 px |
| Retinal vessel segmentation | OOF Dice 0.81164; IoU 0.68300; ROC AUC 0.97324 |

For the lesion-segmentation test set, the reported Dice scores are 0.423552 for microaneurysms, 0.635482 for haemorrhages, 0.746638 for hard exudates, and 0.706758 for soft exudates. The vessel notebook reports out-of-fold metrics because official test ground truth was unavailable.

## Important Limitations

- These models are research prototypes and are not medical devices.
- Outputs must not be used as a diagnosis or a substitute for qualified clinical judgment.
- Dataset licenses, privacy requirements, patient consent, and institutional approvals must be respected.
- Model performance may change across cameras, populations, acquisition conditions, and preprocessing pipelines.
- ONNX input/output execution was not re-run during repository assembly; use the related notebook as the preprocessing reference.

## Missing Project Items

- DME training notebook and authoritative DME class dictionary
- Application installer
- Application screenshots and result images
- Demo video
- SIH presentation
- Project report, research paper, and supporting documentation

## Team Information

- Team: HyperLuma
- SIH ID: SIH26038

Add member names, institute details, contact information, mentor information, and the official problem-statement title before submission.

## License

This repository is distributed under the MIT License. See [LICENSE](LICENSE). Dataset and pretrained-weight usage may also be subject to separate terms imposed by their owners.
