# SignalAI Processing Workflow

## AI-Based Signal Analysis, Demodulation & Intelligence Platform

**Project Name:** SignalAI
**SIH 2026 Problem Statement ID:** SIH26147
**Problem Statement:** Automated model for analysis of `.IQ` and `.wav` files along with signal parameter extraction

---

## 1. Overview

SignalAI follows a structured end-to-end workflow for analyzing recorded `.IQ` and `.wav` signal files.

The workflow is designed to move from raw signal input to signal parameter identification, demodulation, decoding, bitstream analysis, visualization, and reporting.

```text id="k5r3xw"
┌───────────────┐
│ Signal Input  │
└───────┬───────┘
        ↓
┌───────────────┐
│ Preprocessing │
└───────┬───────┘
        ↓
┌──────────────────────┐
│ Parameter             │
│ Identification        │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ Demodulation &       │
│ Decoding             │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ Bitstream Analysis   │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ Visualization &      │
│ Results              │
└──────────────────────┘
```

This six-stage workflow follows the process defined in the SIH submission.

---

# 2. Complete Workflow

The complete SignalAI workflow consists of:

1. Signal Input
2. Signal Preprocessing
3. Feature Extraction
4. Signal Parameter Identification
5. Demodulation
6. De-Interleaving
7. FEC Decoding
8. Bitstream Analysis
9. Visualization
10. Report Generation

```text id="n8e5y2"
IQ / WAV
   ↓
Input Processing
   ↓
Preprocessing
   ↓
Feature Extraction
   ↓
Parameter Identification
   ↓
Modulation Identification
   ↓
Demodulation
   ↓
De-Interleaving
   ↓
FEC Decoding
   ↓
Bitstream Analysis
   ↓
Visualization
   ↓
Report
```

---

# 3. Stage 1 — Signal Input

The workflow begins when the user provides a recorded signal file.

### Supported Formats

```text id="f4uh2j"
.IQ
.WAV
```

### Input Process

```text id="5x3e8p"
User
 ↓
Select Signal File
 ↓
File Type Detection
 ↓
Read Signal Data
 ↓
Read Available Metadata
 ↓
Create Signal Representation
```

The SIH workflow specifies uploading IQ/WAV files and reading available metadata during the signal-input stage.

---

# 4. Stage 2 — Signal Preprocessing

The raw signal is prepared for analysis during the preprocessing stage.

The proposed preprocessing operations include:

* Filtering
* Normalization
* Signal conditioning
* Feature preparation

```text id="m1fs7q"
Raw Signal
    ↓
Filtering
    ↓
Normalization
    ↓
Processed Signal
```

The objective is to prepare a cleaner and more consistent signal representation for subsequent analysis.

---

# 5. Stage 3 — Feature Extraction

After preprocessing, relevant signal characteristics are extracted.

```text id="t0d3q4"
Processed Signal
      ↓
Feature Extraction
      ↓
┌────────────────────────┐
│ Time-Domain Features   │
│ Frequency Features     │
│ Spectral Features      │
│ Modulation Features    │
└────────────────────────┘
```

These features are used by the parameter-identification stage.

---

# 6. Stage 4 — Signal Parameter Identification

SignalAI analyzes the extracted signal characteristics to identify important parameters.

The target parameters include:

* Modulation type
* Sampling rate
* Symbol rate
* FEC
* Interleaving

```text id="h0g6ap"
Extracted Features
       ↓
AI-Assisted Analysis
       ↓
Signal Parameters
       ↓
┌──────────────────────┐
│ Modulation Type      │
│ Sampling Rate        │
│ Symbol Rate          │
│ FEC                  │
│ Interleaving         │
└──────────────────────┘
```

The SIH submission describes AI-assisted identification as a core stage of the proposed workflow.

---

# 7. Stage 5 — Modulation Identification

The system analyzes the signal to determine the possible modulation scheme.

The proposed scope includes:

* FSK
* PSK
* QAM

```text id="y1xjv9"
Signal
  ↓
Feature Analysis
  ↓
Modulation Identification
  ↓
┌─────┬─────┬─────┐
│ FSK │ PSK │ QAM │
└─────┴─────┴─────┘
```

The identified modulation type determines the next demodulation stage.

---

# 8. Stage 6 — Demodulation

The identified modulation type is used to select the appropriate demodulation process.

```text id="f8n6fj"
                 ┌──────────────┐
                 │ FSK          │
                 │ Demodulator  │
                 └──────┬───────┘
                        │
Signal ────────┬────────┼────────┐
               │        │        │
               ▼        ▼        ▼
          FSK Path   PSK Path   QAM Path
```

The objective is to recover symbol or data information from the modulated signal.

The SIH proposal includes FSK, PSK, and QAM demodulation within the proposed demodulation workflow.

---

# 9. FSK Processing Path

For an FSK signal:

```text id="v9l2df"
FSK Signal
    ↓
Frequency Analysis
    ↓
Frequency State Detection
    ↓
Symbol Recovery
    ↓
Recovered Data
```

---

# 10. PSK Processing Path

For a PSK signal:

```text id="m0w8sy"
PSK Signal
    ↓
Phase Analysis
    ↓
Symbol Detection
    ↓
Symbol Mapping
    ↓
Recovered Data
```

---

# 11. QAM Processing Path

For a QAM signal:

```text id="e6a3jk"
QAM Signal
    ↓
Symbol Extraction
    ↓
Constellation Analysis
    ↓
Symbol Mapping
    ↓
Recovered Data
```

---

# 12. Stage 7 — De-Interleaving

If interleaving is identified, the recovered data proceeds through the de-interleaving stage.

```text id="z7t4cx"
Demodulated Data
       ↓
Interleaving Information
       ↓
De-Interleaving
       ↓
Restored Data Order
```

The purpose is to restore the original data ordering before further decoding.

---

# 13. Stage 8 — FEC Decoding

If Forward Error Correction is identified, the system proceeds with the appropriate decoding stage.

```text id="9l3p1q"
Recovered Data
      ↓
FEC Identification
      ↓
FEC Decoder
      ↓
Error Correction
      ↓
Decoded Data
```

FEC decoding is part of the signal-recovery workflow defined in the SIH proposal.

---

# 14. Stage 9 — Bitstream Analysis

After demodulation and decoding, SignalAI analyzes the recovered bitstream.

The proposed analysis includes:

* Pattern detection
* Correlation
* Possible header identification
* Possible payload identification

```text id="2f3n7a"
Decoded Data
     ↓
Bitstream
     ↓
Pattern Detection
     ↓
Correlation Analysis
     ↓
Possible Structure
     ↓
Header / Payload Indicators
```

The SIH submission specifically identifies pattern detection, correlation, and possible header/payload identification as part of the bitstream-analysis stage.

---

# 15. Stage 10 — Visualization

SignalAI provides visual representations of the signal and processing results.

### Waveform

Shows signal behavior in the time domain.

```text id="1s2b5c"
Signal Samples
     ↓
Waveform
```

### FFT

Shows frequency-domain characteristics.

```text id="m6r5uk"
Signal
  ↓
FFT
  ↓
Frequency Spectrum
```

### Spectrogram

Shows frequency behavior over time.

```text id="q8s2vy"
Signal
  ↓
Time-Frequency Analysis
  ↓
Spectrogram
```

### Constellation

Shows symbol distribution for supported digital modulation.

```text id="r3q9bd"
Symbols
   ↓
Complex Plane
   ↓
Constellation
```

These visualization outputs are included in the SIH workflow and proposed system description.

---

# 16. Stage 11 — Result Generation

The system combines the results generated throughout the pipeline.

```text id="3q7n5a"
Input Information
       +
Signal Parameters
       +
Visualizations
       +
Demodulation Results
       +
Decoding Results
       +
Bitstream Analysis
       ↓
Final Analysis Result
```

---

# 17. Stage 12 — Report Generation

The final analysis can be organized into a structured report.

### Report Structure

```text id="d9x1pk"
Signal Information
│
├── File Type
├── Available Metadata
└── Signal Information
│
├── Parameter Analysis
│   ├── Modulation
│   ├── Sampling Rate
│   ├── Symbol Rate
│   ├── FEC
│   └── Interleaving
│
├── Signal Visualization
│   ├── Waveform
│   ├── FFT
│   ├── Spectrogram
│   └── Constellation
│
├── Recovery Results
│   ├── Demodulated Data
│   ├── De-Interleaved Data
│   └── FEC Decoded Data
│
└── Bitstream Analysis
    ├── Patterns
    ├── Correlations
    ├── Possible Header
    └── Possible Payload
```

---

# 18. Complete End-to-End Workflow

The complete workflow can be visualized as:

```text id="k8t6qn"
                    ┌───────────────┐
                    │   IQ / WAV    │
                    └───────┬───────┘
                            ↓
                    ┌───────────────┐
                    │ Signal Input  │
                    └───────┬───────┘
                            ↓
                    ┌───────────────┐
                    │ Preprocessing │
                    └───────┬───────┘
                            ↓
                    ┌───────────────┐
                    │   Features    │
                    └───────┬───────┘
                            ↓
              ┌─────────────────────────┐
              │ Parameter Identification│
              └────────────┬────────────┘
                           ↓
              ┌─────────────────────────┐
              │ Modulation Identification│
              └────────────┬────────────┘
                           ↓
              ┌─────────────────────────┐
              │      Demodulation       │
              │    FSK / PSK / QAM      │
              └────────────┬────────────┘
                           ↓
              ┌─────────────────────────┐
              │ De-Interleaving + FEC   │
              │        Decoding         │
              └────────────┬────────────┘
                           ↓
              ┌─────────────────────────┐
              │   Bitstream Analysis    │
              └────────────┬────────────┘
                           ↓
              ┌─────────────────────────┐
              │ Visualization & Report  │
              └─────────────────────────┘
```

---

# 19. Decision Flow

SignalAI uses the identified signal parameters to determine the appropriate processing path.

```text id="1r2b9w"
                 Signal
                    ↓
             Parameter Analysis
                    ↓
            Modulation Identified?
                 /       \
               YES        NO
                ↓          ↓
        Select Demodulator  Report
                │          │
                ↓          │
          Demodulation     │
                ↓          │
        Interleaving Found?│
             /      \      │
           YES       NO    │
            ↓         ↓    │
      De-Interleave    │    │
            │          │    │
            └────┬─────┘    │
                 ↓          │
             FEC Found?     │
              /     \       │
            YES      NO     │
             ↓        ↓     │
         FEC Decode   │     │
             │        │     │
             └────┬───┘     │
                  ↓         │
            Bitstream       │
              Analysis      │
                  ↓         │
             Visualization  │
                  ↓         │
               Report ◄─────┘
```

---

# 20. Uncertainty Handling

Not every signal parameter can always be identified with certainty.

SignalAI therefore uses different result states:

| Status     | Meaning                                         |
| ---------- | ----------------------------------------------- |
| Identified | Supported by available analysis                 |
| Estimated  | Derived from signal characteristics             |
| Possible   | Potential interpretation requiring verification |
| Unknown    | Insufficient information                        |

Example:

```text id="q0n5dr"
Modulation: QPSK
Status: Identified

Sampling Rate: 2.4 MHz
Status: Estimated

FEC: Unknown
Status: Unknown

Header Pattern: Possible Match
Status: Possible
```

The system should not fabricate missing signal metadata or unsupported confidence values.

---

# 21. Error Handling

The workflow should account for common processing conditions.

### Unsupported File

```text id="p3w5u9"
Invalid File
    ↓
Validation Error
    ↓
User Notification
```

### Corrupted Signal

```text id="z8a3kc"
Signal Read Failure
       ↓
Processing Error
       ↓
User Notification
```

### Insufficient Signal Quality

```text id="5c1m7n"
Poor Signal Quality
       ↓
Analysis Warning
       ↓
Continue Where Possible
```

### Unknown Parameter

```text id="g7k4q2"
Parameter Not Identified
       ↓
Mark as Unknown
       ↓
Continue Remaining Analysis
```

---

# 22. Large Signal Workflow

Large signal files may require special processing strategies.

The proposed workflow can divide the signal into manageable segments.

```text id="x5h3na"
Large Signal File
       ↓
Chunking
       ↓
┌─────────┬─────────┬─────────┐
│ Chunk 1 │ Chunk 2 │ Chunk 3 │ ...
└────┬────┴────┬────┴────┬────┘
     ↓         ↓         ↓
 Analysis   Analysis   Analysis
     │         │         │
     └─────────┴─────────┘
               ↓
        Combined Results
```

Chunk-based processing is one of the proposed approaches for handling large signal data.

---

# 23. User Interaction Workflow

From the user's perspective, the workflow is designed to be simple.

```text id="h9q2lm"
1. Open SignalAI
       ↓
2. Upload IQ / WAV File
       ↓
3. Start Analysis
       ↓
4. View Preprocessing
       ↓
5. View Signal Parameters
       ↓
6. Inspect Visualizations
       ↓
7. Run / View Demodulation
       ↓
8. View Decoding Results
       ↓
9. Analyze Bitstream
       ↓
10. Generate Report
```

---

# 24. Dashboard Workflow

The dashboard provides access to the major processing stages.

```text id="s3m8dz"
┌────────────────────────────────────────────┐
│                  SignalAI                  │
├────────────────────────────────────────────┤
│                                            │
│ Dashboard                                  │
│                                            │
│ Signal Input                               │
│     ↓                                      │
│ Signal Analysis                            │
│     ↓                                      │
│ Demodulation                               │
│     ↓                                      │
│ Bitstream Analysis                         │
│     ↓                                      │
│ Reports                                    │
│                                            │
└────────────────────────────────────────────┘
```

---

# 25. Workflow Output

At the end of the processing pipeline, SignalAI can provide:

### Signal Information

* Input file
* File type
* Available metadata

### Signal Parameters

* Modulation type
* Sampling rate
* Symbol rate
* FEC
* Interleaving

### Signal Visualizations

* Waveform
* FFT
* Spectrogram
* Constellation

### Recovery Information

* Demodulated data
* De-interleaved data
* FEC-decoded data

### Bitstream Information

* Detected patterns
* Correlations
* Possible headers
* Possible payloads

---

# 26. Workflow Summary

The SignalAI workflow can be summarized as:

```text id="v7m2ka"
INPUT
  │
  ▼
IQ / WAV
  │
  ▼
PREPROCESS
  │
  ▼
FILTER + NORMALIZE
  │
  ▼
EXTRACT FEATURES
  │
  ▼
IDENTIFY PARAMETERS
  │
  ├── Modulation
  ├── Sampling Rate
  ├── Symbol Rate
  ├── FEC
  └── Interleaving
  │
  ▼
DEMODULATE
  │
  ├── FSK
  ├── PSK
  └── QAM
  │
  ▼
DE-INTERLEAVE
  │
  ▼
FEC DECODE
  │
  ▼
BITSTREAM ANALYSIS
  │
  ├── Pattern Detection
  ├── Correlation
  ├── Possible Header
  └── Possible Payload
  │
  ▼
VISUALIZE
  │
  ├── Waveform
  ├── FFT
  ├── Spectrogram
  └── Constellation
  │
  ▼
REPORT
```

---

# 27. SIH Workflow Alignment

The SignalAI workflow follows the stages described in the SIH 2026 submission:

```text
Signal Input
      ↓
Preprocessing
      ↓
Parameter Identification
      ↓
Demodulation & Decoding
      ↓
Bitstream Analysis
      ↓
Interactive Dashboard
```

The submitted methodology describes this workflow as the core approach for the proposed system.

---

> **Prototype Notice:** This workflow documents the proposed processing flow for the SignalAI SIH 2026 idea and prototype showcase. It represents the intended system behavior and does not claim that every stage is currently implemented as a production-ready system.

---

**SignalAI — Analyze. Understand. Recover. Discover.**
