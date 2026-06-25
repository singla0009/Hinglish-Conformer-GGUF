# Hinglish Conformer-CTC GGUF

Welcome to the GitHub homepage for the highly optimized **GGUF** (float32) conversion of the `parthiv11/stt_hi_conformer_ctc_large_v2` model, a Conformer-CTC Automatic Speech Recognition (ASR) model specifically trained for **Hindi and Hinglish** (code-switched Hindi-English) speech.

🚀 **[DOWNLOAD THE MODEL FROM HUGGING FACE HERE](https://huggingface.co/Singla0009/Hinglish-Conformer-GGUF)** 🚀

---

⚡ **Powered by CAPIT** ⚡  
These highly-optimized `.gguf` models were explicitly designed and converted to be used seamlessly with **CAPIT**, our blazing-fast, privacy-first desktop transcription application. CAPIT is a state-of-the-art Rust & Tauri native app built by our team that lets you run these massive AI models entirely offline on your local machine with an incredible user interface.  
👉 **[Check out the CAPIT App on our GitHub!](https://github.com/singla0009)**

---

The model is designed for high-performance, local deployment with zero Python dependencies using the lightweight C++ `parakeet-cpp` engine (GGML backend). 

> [!IMPORTANT]
> The GGUF file is fully standalone. Configuration parameters and the 128-token sentencepiece vocabulary are embedded directly inside the binary.

## Model Details
*   **Architecture:** Conformer-CTC (Large)
*   **Parameter Count:** ~120M
*   **Vocabulary Size:** 128 tokens
*   **Training Data:** ~2,900 hours of combined Hindi and Hinglish speech from the ULCA and Europal corpora.
*   **Input Format:** 16,000 Hz mono-channel WAV audio.

---

## Evaluation & Analytics

### 1. Accuracy Benchmarks (WER & CER)
These metrics are calculated using Greedy Decoding (without KenLM rescoring).

| Dataset | Word Error Rate (WER) | Character Error Rate (CER) |
| :--- | :--- | :--- |
| **MUCS 2021 Blind Test** | **9.37%** | **2.74%** |
| **IITM 2020 Eval Set** | **12.93%** | **5.60%** |
| **Common Voice 6 Test** | **13.16%** | **4.50%** |
| **Common Voice 7 Test** | **13.50%** | **5.20%** |
| **Common Voice 8 Test** | **14.37%** | **5.95%** |

### 2. Local Performance & Speed Benchmarks
Tested on a local edge device (NVIDIA RTX GPU & AMD/Intel CPU).
*   **Test Audio Duration:** 7.26 seconds (mono, 16000Hz).
*   **Metric:** Real-Time Factor (RTF). Lower is faster.

| Configuration | Average Inference Time | Real-Time Factor (RTF) | CPU / RAM Footprint |
| :--- | :--- | :--- | :--- |
| **Hinglish CTC (GPU / CUDA)** | **0.481s** | **0.066x (15x speed)** | ~520 MB VRAM |
| **Hinglish CTC (CPU)** | **0.383s** | **0.053x (19x speed)** | ~140 MB RAM |

> [!TIP]
> The CTC architecture (Non-Autoregressive) is inherently much faster on CPU than traditional RNN-T or Seq2Seq decoders. For short clips, the CPU executes the model at nearly **20x real-time speed**!

### 3. Comparison vs. Heavyweight Models

| Feature / Model | Hinglish Conformer-CTC GGUF (Ours) | OpenAI Whisper Large V3 |
| :--- | :--- | :--- |
| **Parameter Count** | **~120M** | ~1.5B |
| **RAM/VRAM Footprint**| **~140 MB** | ~3.1 GB |
| **Code-Switching** | Excellent native Hinglish support | Tends to force-translate into pure English or pure Hindi |
| **Inference Mode** | Fast Greedy CTC Decoding | Batch-only (seq2seq autoregressive) |

---

## Usage Instructions

To run this model, you need the **parakeet-cli** C++ execution engine.

1. Go to the [parakeet.cpp GitHub Repository](https://github.com/PABannier/parakeet.cpp).
2. Follow their build instructions to compile the `parakeet-cli` executable for your specific operating system (Windows/Linux/macOS).
3. Once compiled, open your terminal and run the model using the following command:

```bash
parakeet-cli transcribe --model hinglish-conformer-ctc.f32.gguf --input audio.wav --decoder ctc --lang hi
```

## Credits and Licenses
*   **Original Checkpoint:** [parthiv11/stt_hi_conformer_ctc_large_v2](https://huggingface.co/parthiv11/stt_hi_conformer_ctc_large_v2)
*   **License:** Under NVIDIA NGC Terms of Use / CC-BY-4.0.
