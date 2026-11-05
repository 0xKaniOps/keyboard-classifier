# Keyboard Classifier - Project 01 ML

Image classifier that tells a mechanical keyboard from a laptop keyboard, built  with PyTorch and transfer learning (ResNet-18).

> Started as a school project and now developed as a personal ML engineering project. Progress tracked in ROADMAP.md

## Demo

*Demo coming in v3: a Gradio app with Grad-CAM heatmaps showing wha the model looks at*

## Results
| Version | Model | Validation | Test | Baseline (majority class) |
|---|---|---|---|---|
| v1 | ResNet-18, frozen backbone, no augmentation | 96% | **82%** | 68% |

Test set (28 images) : 4 mechanical keyboards predicted as laptop, 1 laptop predicted as mechanical

## Dataset
| | Mechanical | Laptop | Total |
|---|---|---|---|
| Train | 82 | 39 | 121 (70%) |
| Validation | 17 | 8 | 25 (14%) |
| Test | 19 | 9 | 28 (16%) |
| **Total** | **118** | **56** | **174** |

- **Source**: web images collected with `bing-image-downloader` (queries: `mechanical keyboard`, `mechanical keyboard photo`, `laptop keyboard close up`).
- **Cleaning**: exact duplicates removed with an MD5 hash (59 duplicates), unreadable files removed.
- **Split**: 70 / 15 / 15 per class, fixed seed, done **after** deduplication.
- `data/metadata.csv` lists every image: path, label, split, source query, original file name and hash.
- The images themselves are **not** included in the repo: many come from stock photo websites and are copyrighted.

## What I learned

## Limitations (v1)
- **Framing bias**: laptop keyboards are almost all close-ups, mechanical keyboards are mostly shown whole. The model partly relies on framing: a close-up of a mechanical keyboard is predicted "laptop" with 93% confidence.
- **Web-only data**: many images carry stock photo watermarks; the model has never seen a real phone photo.
- **Class imbalance**: 118 mechanical vs 56 laptop images.
- **Cleaning**: only exact duplicates are removed; one infographic remained in the test set.

## Project structure
 
```
keyboard-classifier/
├── app/            # Gradio demo (v3)
├── data/
│   └── metadata.csv
├── notebooks/
│   └── v1_school_project.ipynb   # archived v1, with outputs
├── src/            # training and evaluation scripts (v2)
├── requirements.txt
└── ROADMAP.md
```
## Setup
 
```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```
## Author
 
Cécile MATHIEU - [GitHub](https://github.com/0xKaniOps)
