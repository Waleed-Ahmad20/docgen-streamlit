# DocGen — Integrated Documentation Generation System

A Streamlit web application that automatically generates docstrings and summaries for Python functions using a Seq2Seq model with attention, BPE tokenization, and Word2Vec embeddings.

---

## Features

- **Automatic docstring generation** — paste or upload a Python file and get instant documentation for any function
- **BPE tokenization** — Byte Pair Encoding tokenizers for both source code and documentation vocabulary
- **Word2Vec embeddings** — pre-trained embeddings used to initialize the encoder and decoder
- **Attention-based Seq2Seq model** — LSTM encoder–decoder with additive attention for generation
- **Context retrieval** — find the nearest-neighbor examples from the training corpus (cosine similarity over Word2Vec vectors) and feed them as additional context
- **Configurable generation** — choose between a short summary or a full docstring; set the maximum output length
- **Download results** — export the generated documentation as a plain-text file

---

## Project structure

```
docgen-streamlit/
├── app_streamlit_docgen.py        # Main Streamlit application
├── requirements.txt               # Python dependencies
├── streamlit/
│   └── config.toml                # Streamlit server configuration
└── model_artifacts/               # Pre-trained model files (Git LFS)
    ├── bpe_code_tokenizer.pkl
    ├── bpe_doc_tokenizer.pkl
    ├── word2vec_code.pkl
    ├── word2vec_doc.pkl
    ├── tokenized_sample.pkl
    └── seq2seq_attention_state.pt
```

---

## Requirements

- Python 3.8 or later
- [Git LFS](https://git-lfs.com/) (to pull the model artifacts)

---

## Installation

1. **Clone the repository** (Git LFS required for model files):

   ```bash
   git lfs install
   git clone https://github.com/Waleed-Ahmad20/docgen-streamlit.git
   cd docgen-streamlit
   ```

2. **Create and activate a virtual environment** (recommended):

   ```bash
   python -m venv .venv
   source .venv/bin/activate   # Windows: .venv\Scripts\activate
   ```

3. **Install dependencies**:

   ```bash
   pip install -r requirements.txt
   ```

---

## Running the app

```bash
streamlit run app_streamlit_docgen.py
```

Open [http://localhost:8501](http://localhost:8501) in your browser.

---

## Usage

1. **Paste** a Python function directly into the text area **or** click *Upload a .py file* to load a file.
2. If multiple functions are found, select the one you want to document from the dropdown.
3. Adjust the generation options in the **sidebar**:
   - *What to generate* — short summary or full docstring
   - *Max generated length* — maximum number of output tokens
   - *Use context retrieval* — toggle Word2Vec nearest-neighbor context
   - *Nearest neighbors* — how many similar examples to include as context
4. Click **Generate documentation**.
5. The generated text appears on the right side. Use **Download .txt** to save it.

---

## Deployment on Streamlit Cloud

1. Push this repository (including all Git LFS objects) to GitHub.
2. Go to [share.streamlit.io](https://share.streamlit.io) and connect the repository.
3. Set the main file to `app_streamlit_docgen.py`.
4. Streamlit Cloud will install `requirements.txt` automatically.

> **Note:** Streamlit Cloud supports Git LFS. Make sure all files in `model_artifacts/` are tracked by LFS before deploying.

---

## Model details

| Component | Details |
|-----------|---------|
| Encoder | Single-layer LSTM |
| Decoder | LSTMCell with additive (Bahdanau-style) attention |
| Embedding dim | 128 (from Word2Vec) |
| Hidden dim | 256 |
| Vocabulary | BPE sub-word tokenization for both code and documentation |
| Inference | Greedy decoding |

---

## Dependencies

| Package | Version |
|---------|---------|
| streamlit | 1.29.0 |
| torch | ≥ 1.13.0 |
| numpy | latest |
| pandas | latest |
| scikit-learn | latest |
| tqdm | latest |

---

## License

This project is released for educational and research purposes.
