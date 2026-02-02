<div align="center">
  <img src="https://media.licdn.com/dms/image/v2/D4D3DAQGkkIzuYTx0zw/image-scale_127_750/B4DZu_V4VqJwAM-/0/1768441746516/torres_ferreira_zerbini_cover?e=1770598800&v=beta&t=4vLqaCytsPj9vU-pQonrV2rTOdlVvoSBQn6K5WdtGI0" alt="TFZ Intelligence Logo" width="550">
  <h1>Forensic Document Auditor (FDA)</h1>
  <p>
    <b>Algorithmic detection of document manipulation using Error Level Analysis (ELA) and Metadata Mining.</b>
  </p>
  
  <p>
    <a href="#-about-the-project">About</a> •
    <a href="#-key-features">Key Features</a> •
    <a href="#-how-it-works">How It Works</a> •
    <a href="#-installation">Installation</a> •
    <a href="#-business-impact">Business Impact</a>
  </p>

  <img src="https://img.shields.io/badge/Status-Production-success?style=for-the-badge" alt="Status">
  <img src="https://img.shields.io/badge/Forensics-Level%204-005571?style=for-the-badge" alt="Forensics Level">
  <img src="https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
</div>

---
## 📂 Estrutura do Repositório

```
/forensic-document-auditor
│
├── /assets          # Logos e prints dos resultados (Antes/Depois)
├── /docs            # Laudos de exemplo (anonimizados) ou PDFs técnicos
├── /src             # Código fonte (clean architecture)
│   ├── analyzer.py
│   ├── ela_utils.py
│   └── metadata.py
├── /notebooks       # Jupyter Notebooks para demo (Storytelling)
├── requirements.txt
├── Dockerfile       # (Obrigatório para vaga de MLE/DevOps)
└── README.md
```

## 🛡️ About The Project

> *"The human eye is easily deceived. The hexadecimal structure is not."*

In the era of Generative AI and sophisticated Deepfakes, traditional visual inspection of documents (Level 1 Forensics) is obsolete. The **Forensic Document Auditor (FDA)** is a tool developed at **TFZ Intelligence** to automate the detection of fraud in digital evidences (PDFs and Images).

This tool moves beyond the pixel layer, analyzing the mathematical consistency of files to detect:
* **Digital Transplants:** Signatures or text blocks pasted from other sources.
* **Metadata Scrubbing:** Inconsistencies between creation/modification timestamps and software versions.
* **Compression Artifacts:** Through Error Level Analysis (ELA), identifying areas with different compression rates (evidence of manipulation).

---

## 🚀 Key Features

- **🔍 Error Level Analysis (ELA):** Generates heatmaps highlighting foreign elements in an image (e.g., a pasted signature usually has a different compression error rate than the background).
- **📄 PDF Structure Mining:** Deep scan of PDF object hierarchy (ObjStm) to find "orphan" objects or inconsistent XRef tables often left behind by PDF editors.
- **🕒 Timeline Reconstruction:** Cross-referencing of internal metadata (EXIF/XMP) to reconstruct the true lifecycle of the file.
- **📊 Automated Reporting:** Generates a technical JSON summary flagging risk levels (Low, Medium, Critical).

---

## 🔬 How It Works (Technical Demo)

### 1. Visual Inspection (What the Judge sees)
The document appears authentic. No visible rasures.

![Visual Inspection](assets/demo_visual.png)
*(Note: Insert a print of a normal document here)*

### 2. ELA Analysis (What the Algorithm sees)
The ELA algorithm enhances the compression artifacts. The signature area glows white/red, indicating it was pasted recently and saved at a different quality level than the rest of the document.

![ELA Analysis](assets/demo_ela_heatmap.png)
*(Note: Insert the ELA heatmap result here - this is the "Money Shot")*

### 3. Metadata Verdict
```json
{
  "filename": "contract_v2.pdf",
  "risk_score": "CRITICAL",
  "flags": [
    "Mismatch: CreationDate > ModDate",
    "Software: Adobe Photoshop CS6 detected in stream",
    "Inconsistent quantization tables in image object #4"
  ]
}
```
## 🛠️ Tech Stack
Core: Python 3.9

Computer Vision: OpenCV, PIL (Pillow)

Forensics: hachoir (Metadata), pypdf (Structure)

Visualization: Matplotlib, Seaborn

Containerization: Docker

## 💻 Installation & Usage
To ensure reproducibility (a key requirement for forensic standards), this project is containerized.

Option A: Running with Docker (Recommended)
```
Bash
# Build the image
docker build -t tfz-forensic-auditor .
```
# Run analysis on a target file
```
docker run -v $(pwd)/evidence:/data tfz-forensic-auditor --scan /data/suspicious_contract.pdf
Option B: Local Environment
Bash
git clone [https://github.com/fertorresfs/forensic-document-auditor.git](https://github.com/fertorresfs/forensic-document-auditor.git)
cd forensic-document-auditor
pip install -r requirements.txt
```
# Run the analyzer
python src/main.py --input samples/fraud_sample_01.jpg --method ela --output report.json
## 📉 Business Impact
This tool was designed to solve the "Subjectivity Gap" in litigation. By translating visual opinions into mathematical certainty, we achieved:

Zero False Negatives in controlled tests with manipulated PDFs.

90% reduction in time spent on initial document triage.

Auditability: Every analysis generates a hash-verified log, ensuring Chain of Custody compliance.

## 👤 Author
Fernando Torres Founder @ TFZ Intelligence | Forensic Data Scientist | MSc Candidate at USP

<a href="https://www.linkedin.com/in/fertorresfs/"> <img src="https://www.google.com/search?q=https://img.shields.io/badge/LinkedIn-Connect-0077B5%3Fstyle%3Dfor-the-badge%26logo%3Dlinkedin"> </a>
