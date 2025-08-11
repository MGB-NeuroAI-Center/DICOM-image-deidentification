# DICOM Image Deidentification (legacy pydicom and Presidio tools)

## Description
This project performs attempted DICOM image de-identification at both metadata and pixel levels. It uses the `pydicom` library to attempt to remove and pseudonymize DICOM tags and Microsoft’s `presidio-image-redactor` to redact PHI from pixel data, but it requires manual verification.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Configuration](#configuration)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites
- **Python** 3.8+
- **pydicom**
- **presidio-image-redactor**
- **OpenCV**, **matplotlib**, **skimage** (for image processing and visualization)
- **.env** configuration file
- Recommended IDE: **VSCode** or **Jupyter Lab**

## Installation

### Setup Instructions
1. Clone the repository
   ```bash
   git clone https://github.com/MGB-NeuroAI-Center/image-deidentification.git
   cd image-deidentification
   ```

2. Create virtual environment
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

3. Install dependencies
   ```bash
   pip install -r config/requirements.txt
   ```

4. Set environment variables
   - Copy `.env.example` to `.env` and configure paths (e.g., `INPUT_DIRECTORY`, `OUTPUT_DIRECTORY`, `IMAGES_PROCESSED`, etc.)

## Usage

### Quick Start

#### 1. Metadata Tag De-identification:
Run the notebook:
```bash
jupyter notebook src/image_tag_deidentification_pipeline.ipynb
```

Edit your `.env` to set:
- `INPUT_DIRECTORY`
- `OUTPUT_DIRECTORY`
- `IMAGES_PROCESSED`
- `SAMPLED_DATA_FOLDER_NAMES`

#### 2. Pixel-Level Redaction:
Run the notebook:
```bash
jupyter notebook src/presidio_image_redaction.ipynb
```

Make sure the following variables are set in your `.env`:
- `INPUT_PATH`
- `INPUT_PATH2`
- `OUTPUT_DIR`

### Common Use Cases

#### Use Case 1: Batch Process DICOM Folder
```python
df = batch_process_directory(INPUT_DIRECTORY, OUTPUT_DIRECTORY, skip_files=True)
```

#### Use Case 2: Redact Overlayed Text in Images
```python
engine = DicomImageRedactorEngine()
engine.redact(dicom_instance, fill="contrast", ocr_kwargs=ocr_kwargs, ad_hoc_recognizers=[name_recognizer, phone_number_recognizer])
```

## Project Structure
```
IMAGE-DEIDENTIFICATION/
├── config/
│   ├── .env.example                               # Sample environment variable file
│   └── requirements.txt                           # Python dependencies
├── src/
│   ├── image_tag_deidentification_pipeline.ipynb  # Notebook for tag-level deidentification
│   └── presidio_image_redaction.ipynb             # Notebook for image pixel redaction
├── .gitignore
├── LICENSE
└── README.md
```

## Configuration

### Environment Variables

Set up environment variables by creating a .env file based on the provided .env.example file.

## Data Requirements

### Input Format
- Standard `.dcm` DICOM image files in nested directory structure

### Output
- Anonymized `.dcm` files written to specified output folders
- Summary and tracking CSV file updated with image metadata

## Contributing
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -m 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Open a Pull Request

### Contribution Guidelines
- Follow notebook formatting best practices
- Keep DICOM file handling secure and PHI-compliant
- Document your logic clearly

## License
This project is licensed under the **Attribution Non-Commercial 4.0 International License** - see the [LICENSE](LICENSE) file for details.

© 2025 The General Hospital Corporation

## Acknowledgments
- [Presidio Image Redactor](https://github.com/microsoft/presidio) by Microsoft
- [pydicom](https://github.com/pydicom/pydicom) for DICOM handling

## Contact
- **Project Maintainer**: Siril Raj Singa (*ssinga@mgh.harvard.edu*)
- **Issues**: [WIP]

---
**Last Updated**: August 6, 2025 | **Version**: 1.0.0
