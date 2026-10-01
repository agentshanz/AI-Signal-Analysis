# System Architecture

## AI-Based Signal Analysis, Demodulation & Intelligence Platform

**Project Name:** SignalAI
**SIH 2026 Problem Statement ID:** SIH26147
**Problem Statement:** Automated model for analysis of `.IQ` and `.wav` files along with signal parameter extraction

---

## 1. Overview

SignalAI is designed as a modular signal-analysis platform that processes recorded `.IQ` and `.wav` signal files through multiple stages.

The architecture connects signal input, preprocessing, feature extraction, AI-assisted parameter identification, demodulation, decoding, bitstream analysis, visualization, and reporting into a single workflow.

The proposed architecture is based on the six major stages described in the SIH workflow:

1. Signal Input
2. Preprocessing
3. Parameter Identification
4. Demodulation & Decoding
5. Bitstream Analysis
6. Interactive Dashboard

---

# 2. High-Level Architecture

```text
┌─────────────────────────────────────────────────────────────┐
│                         SIGNALAI                            │
│      AI-Based Signal Analysis & Intelligence Platform       │
└─────────────────────────────────────────────────────────────┘

                         USER
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                    PRESENTATION LAYER                       │
│                                                             │
│  Dashboard │ Signal Input │ Analysis │ Demodulation        │
│  Bitstream Analysis │ Reports                              │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                     APPLICATION LAYER                       │
│                                                             │
│        Signal Processing Pipeline Controller                │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                      PROCESSING LAYER                       │
│                                                             │
│ ┌────────────┐   ┌──────────────┐   ┌────────────────────┐ │
│ │ Input      │ → │ Preprocessing│ → │ Feature Extraction │ │
│ └────────────┘   └──────────────┘   └─────────┬──────────┘ │
│                                               │            │
│                                               ▼            │
│                                  ┌────────────────────────┐│
│                                  │ Parameter Identification││
│                                  └───────────┬────────────┘│
│                                              │             │
│                                              ▼             │
│                                  ┌────────────────────────┐│
│                                  │    Demodulation        ││
│                                  │ FSK │ PSK │ QAM        ││
│                                  └───────────┬────────────┘│
│                                              │             │
│                                              ▼             │
│                                  ┌────────────────────────┐│
│                                  │ De-Interleaving & FEC  ││
│                                  │       Decoding         ││
│                                  └───────────┬────────────┘│
│                                              │             │
│                                              ▼             │
│                                  ┌────────────────────────┐│
│                                  │   Bitstream Analysis   ││
│                                  └────────────────────────┘│
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                     OUTPUT LAYER                            │
│                                                             │
│ Waveform │ FFT │ Spectrogram │ Constellation               │
│ Parameters │ Decoded Data │ Bitstream │ Reports            │
└─────────────────────────────────────────────────────────────┘
```

---

# 3. Architecture Layers

SignalAI can be organized into four primary architectural layers:

```text
Presentation Layer
        ↓
Application Layer
        ↓
Processing Layer
        ↓
Output / Visualization Layer
```

Each layer has a specific responsibility in the overall system.

---

# 4. Presentation Layer

The presentation layer provides the user interface through which users interact with SignalAI.

The proposed interface can be implemented using a Python-based UI framework such as:

* PyQt
* Streamlit

The SIH submission identifies Python with PyQt/Streamlit as the proposed application interface approach.

### Main Interface Sections

```text
┌─────────────────────────────────────┐
│              SignalAI               │
├─────────────────────────────────────┤
│ Dashboard                           │
│ Signal Input                        │
│ Signal Analysis                     │
│ Demodulation                        │
│ Bitstream Analysis                  │
│ Reports                             │
└─────────────────────────────────────┘
```

---

# 5. Signal Input Module

The Signal Input module is responsible for accepting signal recordings.

### Supported Input Types

```text
.IQ
.WAV
```

### Responsibilities

* File upload
* File-type detection
* Signal loading
* Metadata extraction
* Input validation
* Preparation for processing

### Data Flow

```text
User
 ↓
Upload IQ / WAV
 ↓
File Validation
 ↓
Signal Loader
 ↓
Signal Representation
```

---

# 6. Signal Preprocessing Module

The preprocessing module prepares raw signal data for analysis.

### Responsibilities

* Filtering
* Normalization
* Noise reduction
* Signal conditioning
* Feature preparation

### Data Flow

```text
Raw Signal
     ↓
Filtering
     ↓
Normalization
     ↓
Conditioned Signal
```

The SIH workflow explicitly identifies filtering, normalization, and feature extraction within the preprocessing stage.

---

# 7. Feature Extraction Module

The feature extraction module converts processed signal data into useful characteristics for further analysis.

### Feature Categories

```text
Signal
  │
  ├── Time-Domain Features
  │
  ├── Frequency-Domain Features
  │
  ├── Time-Frequency Features
  │
  └── Modulation-Related Features
```

These features can be passed to the parameter-identification module.

---

# 8. Parameter Identification Module

This module is responsible for identifying important characteristics of the signal.

### Target Parameters

* Modulation type
* Sampling rate
* Symbol rate
* FEC
* Interleaving

The SIH submission identifies AI-assisted identification as a key stage for extracting these signal parameters.

### Architecture

```text
Processed Signal
       ↓
Feature Extraction
       ↓
AI-Assisted Analysis
       ↓
Parameter Identification
       ↓
┌───────────────────────────────┐
│ Modulation Type               │
│ Sampling Rate                 │
│ Symbol Rate                   │
│ FEC                           │
│ Interleaving                  │
└───────────────────────────────┘
```

---

# 9. Modulation Analysis Module

The modulation-analysis module assists in identifying the modulation scheme.

The proposed scope includes:

* FSK
* PSK
* QAM

### Processing Flow

```text
Signal Features
      ↓
Modulation Analysis
      ↓
┌─────┬─────┬─────┐
│ FSK │ PSK │ QAM │
└─────┴─────┴─────┘
```

The identified modulation type determines the appropriate demodulation path.

---

# 10. Demodulation Module

The demodulation module converts the identified modulated signal into recovered symbol or data information.

### Supported Paths

```text
                 ┌──→ FSK Demodulation
                 │
Signal ──────────┼──→ PSK Demodulation
                 │
                 └──→ QAM Demodulation
```

### Responsibilities

* Select appropriate demodulation method
* Process signal symbols
* Recover data representation
* Pass recovered information to decoding stages

---

# 11. De-Interleaving Module

The de-interleaving module restores the ordering of data when interleaving is identified.

```text
Demodulated Data
       ↓
Interleaving Information
       ↓
De-Interleaving
       ↓
Restored Data
```

This module operates before FEC decoding when the identified signal structure requires de-interleaving.

---

# 12. FEC Decoding Module

The FEC decoding module processes recovered data using the identified Forward Error Correction scheme where applicable.

```text
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

The exact decoding process depends on the FEC information available from the signal analysis.

---

# 13. Bitstream Analysis Module

After demodulation and decoding, the resulting data is passed to the bitstream-analysis module.

### Responsibilities

* Pattern detection
* Bitstream inspection
* Correlation analysis
* Possible header identification
* Possible payload identification

```text
Decoded Data
     ↓
Bitstream
     ↓
Pattern Detection
     ↓
Correlation
     ↓
Possible Structure
```

The SIH proposal specifically includes pattern detection, correlation, and possible header/payload identification.

---

# 14. Visualization Module

The visualization module presents signal and analysis information to the user.

### Supported Visualizations

| Visualization  | Purpose                           |
| -------------- | --------------------------------- |
| Waveform       | Time-domain signal representation |
| FFT            | Frequency-domain analysis         |
| Spectrogram    | Time-frequency analysis           |
| Constellation  | Symbol distribution               |
| Bitstream View | Binary data inspection            |

The SIH workflow identifies waveform, spectrum, and constellation visualization as part of the analysis process.

---

# 15. Reporting Module

The reporting module organizes the analysis results into a structured report.

### Report Information

```text
Signal Information
├── Input File
├── File Type
└── Available Metadata

Signal Parameters
├── Modulation
├── Sampling Rate
├── Symbol Rate
├── FEC
└── Interleaving

Signal Analysis
├── Waveform
├── FFT
├── Spectrogram
└── Constellation

Recovery Results
├── Demodulated Data
├── De-Interleaved Data
└── FEC Decoded Data

Bitstream Results
├── Patterns
├── Correlations
├── Possible Header
└── Possible Payload
```

---

# 16. Application Layer

The application layer coordinates the different processing modules.

Its primary responsibility is to control the movement of signal data through the analysis pipeline.

```text
Input
  ↓
Preprocessing
  ↓
Feature Extraction
  ↓
Parameter Identification
  ↓
Demodulation
  ↓
Decoding
  ↓
Bitstream Analysis
  ↓
Results
```

The application layer acts as the central coordinator between the user interface and signal-processing components.

---

# 17. Processing Pipeline

The complete data flow can be represented as:

```text
┌──────────────┐
│ IQ / WAV     │
│ Input        │
└──────┬───────┘
       ↓
┌──────────────┐
│ Preprocessing│
└──────┬───────┘
       ↓
┌──────────────┐
│ Feature      │
│ Extraction   │
└──────┬───────┘
       ↓
┌──────────────┐
│ Parameter    │
│ Identification│
└──────┬───────┘
       ↓
┌──────────────┐
│ Demodulation │
└──────┬───────┘
       ↓
┌──────────────┐
│ De-Interleave│
│ + FEC        │
└──────┬───────┘
       ↓
┌──────────────┐
│ Bitstream    │
│ Analysis     │
└──────┬───────┘
       ↓
┌──────────────┐
│ Visualization│
│ & Reporting  │
└──────────────┘
```

---

# 18. Data Flow

The system processes signal data through a sequential flow.

### Level 1 — Input

```text
IQ / WAV File
```

### Level 2 — Signal Representation

```text
Raw Samples
```

### Level 3 — Processed Signal

```text
Filtered + Normalized Signal
```

### Level 4 — Extracted Features

```text
Time / Frequency / Signal Features
```

### Level 5 — Signal Parameters

```text
Modulation
Sampling Rate
Symbol Rate
FEC
Interleaving
```

### Level 6 — Recovered Data

```text
Demodulated
     ↓
De-Interleaved
     ↓
FEC Decoded
```

### Level 7 — Intelligence

```text
Bitstream Patterns
Correlation
Possible Header
Possible Payload
```

---

# 19. Technology Architecture

The proposed technology architecture follows the stack described in the SIH submission.

```text
┌─────────────────────────────┐
│        User Interface       │
│       PyQt / Streamlit     │
└──────────────┬──────────────┘
               ↓
┌─────────────────────────────┐
│      Application Logic      │
│          Python             │
└──────────────┬──────────────┘
               ↓
┌─────────────────────────────┐
│     Signal Processing       │
│     NumPy + SciPy           │
└──────────────┬──────────────┘
               ↓
┌─────────────────────────────┐
│       AI / ML Layer         │
│         TensorFlow          │
└──────────────┬──────────────┘
               ↓
┌─────────────────────────────┐
│      Visualization          │
│        Matplotlib            │
│        OpenCV                │
└─────────────────────────────┘
```

The SIH proposal identifies Python, NumPy, SciPy, TensorFlow, Matplotlib, OpenCV, VS Code/Jupyter, and PyQt/Streamlit as the proposed technologies.

---

# 20. Module Interaction

The major modules interact as follows:

```text
                         ┌───────────────┐
                         │  Signal Input │
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
                  ┌──────────────────────────┐
                  │ Parameter Identification│
                  └────────────┬─────────────┘
                               ↓
                  ┌──────────────────────────┐
                  │      Demodulation        │
                  └────────────┬─────────────┘
                               ↓
                  ┌──────────────────────────┐
                  │ De-Interleaving + FEC    │
                  └────────────┬─────────────┘
                               ↓
                  ┌──────────────────────────┐
                  │   Bitstream Analysis     │
                  └────────────┬─────────────┘
                               ↓
                  ┌──────────────────────────┐
                  │ Visualization + Reports  │
                  └──────────────────────────┘
```

---

# 21. Error and Uncertainty Handling

Signal analysis may not always produce a definitive result.

The architecture therefore supports result states such as:

```text
┌──────────────────────┐
│ Identified           │
│ Confirmed by analysis│
└──────────────────────┘

┌──────────────────────┐
│ Estimated            │
│ Derived estimate     │
└──────────────────────┘

┌──────────────────────┐
│ Possible             │
│ Requires verification│
└──────────────────────┘

┌──────────────────────┐
│ Unknown              │
│ Insufficient data    │
└──────────────────────┘
```

This prevents the system from presenting unsupported information as confirmed signal metadata.

---

# 22. Large Data Processing

Large signal recordings may require significant memory and processing resources.

The proposed architecture can support:

* Chunk-based processing
* Efficient signal storage
* Selective processing
* GPU acceleration where appropriate

These approaches are aligned with the mitigation strategies identified in the SIH proposal for handling large datasets and real-time performance challenges.

---

# 23. Scalability Considerations

The modular architecture allows individual processing components to be improved independently.

For example:

```text
Current
  ↓
FSK / PSK / QAM
  ↓
Future
  ↓
Additional Modulation Schemes
```

Similarly:

```text
Current
  ↓
Basic Bitstream Analysis
  ↓
Future
  ↓
Advanced Pattern & Protocol Analysis
```

This allows the platform to evolve without requiring a complete architectural redesign.

---

# 24. Security and Data Handling

Signal files may contain sensitive or proprietary information.

The prototype architecture should therefore consider:

* Local processing where possible
* Controlled file handling
* Temporary-file cleanup
* Restricted access to uploaded data
* Avoiding unnecessary external transmission of signal recordings

The exact security implementation is outside the current SIH prototype documentation scope.

---

# 25. Prototype Architecture

The current repository represents an **SIH 2026 idea and prototype showcase**.

Therefore, the architecture documented here represents the proposed system design rather than a claim that every module has been implemented as a production-ready service.

```text
             SIGNALAI PROTOTYPE
                    │
       ┌────────────┴────────────┐
       │                         │
   Documentation             UI Prototype
       │                         │
       ├── Problem              ├── Dashboard
       ├── Solution             ├── Signal Input
       ├── Architecture         ├── Analysis
       ├── Technical Approach   ├── Demodulation
       └── Workflow             ├── Bitstream
                                └── Reports
```

---

# 26. Architecture Summary

SignalAI uses a modular architecture that connects:

```text
Input
 ↓
Preprocessing
 ↓
Feature Extraction
 ↓
AI-Assisted Parameter Identification
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
Reporting
```

The architecture is designed to provide a unified environment for analyzing recorded IQ/WAV signals and extracting useful signal information.

---

## 27. Reference

The architecture is derived from the workflow, methodology, technical approach, and system requirements described in the SIH 2026 submission for Problem Statement **SIH26147**.

> **Prototype Notice:** This architecture describes the proposed design of SignalAI for the SIH 2026 idea and prototype. It does not represent a completed production implementation.

---

**SignalAI — Analyze. Understand. Recover. Discover.**
