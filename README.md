# Leaf-Scan

The processed leaf-image dataset is available in the
[Processed Dataset v1 release](https://github.com/Janci-Kundana/Leaf-Scan/releases/tag/processed-dataset-v1).

The original `Proccessed Dataset.zip` archive is 7,668,619,852 bytes
(7.14 GiB). It is stored as four release assets, each smaller than 2 GiB,
to keep the Git repository small. Download all four parts before extracting.

## Download and extract with the CLI

Requirements: GitHub CLI (`gh`), `sha256sum`, and `unzip`. Use a new directory
with at least 24 GiB of free space for the parts, joined ZIP, and extracted data.

```bash
mkdir leaf-scan-dataset
cd leaf-scan-dataset

gh release download processed-dataset-v1 \
  --repo Janci-Kundana/Leaf-Scan \
  --pattern 'processed-dataset.zip.part-*' \
  --pattern SHA256SUMS \
  --pattern processed-dataset.zip.sha256

sha256sum --check SHA256SUMS && \
  cat processed-dataset.zip.part-001 \
      processed-dataset.zip.part-002 \
      processed-dataset.zip.part-003 \
      processed-dataset.zip.part-004 > processed-dataset.zip && \
  sha256sum --check processed-dataset.zip.sha256 && \
  unzip processed-dataset.zip
```

On macOS, replace `sha256sum --check` with `shasum -a 256 --check`.
Parts are byte ranges of one ZIP, not independently extractable archives.
Cloning this repository downloads the documentation and manifest; use the
release command above to download the images.

## Contents

The original folder names are preserved:

```text
Proccessed Dataset/
├── Test Set/                         # 72,707 JPEG images, 15 class folders
└── plantvillage_train_128x128/        # 15,154 JPEG images, 15 class folders
```

There are 87,861 dataset JPEG images in total. Original macOS metadata
(`__MACOSX`, `.DS_Store`, and AppleDouble files) is also preserved in the ZIP;
these files are not included in the image counts.

See [dataset-manifest.json](dataset-manifest.json) for class counts, exact
part sizes, and SHA-256 checksums. Every entry in the source ZIP passed CRC
validation before upload.
