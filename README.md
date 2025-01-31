# Alignment_project
This program is designed to **align English and Chinese texts** at the phrase level and analyze **Part-of-Speech (POS) shifts** between them. It automates the process of breaking down both languages into sentences, tokenizing words, and identifying how words or phrases in one language correspond to those in the other. 

To accomplish this, the program uses **spaCy** for English text processing and **jieba** for Chinese segmentation. It first reads the original text and its translation, splits them into sentences, and assigns linguistic properties to each word, such as **POS tags and syntactic dependencies**. Because sentence structures in English and Chinese can vary significantly, the program doesn’t rely on strict word-by-word matching. Instead, it **groups words into chunks** and sends them to OpenAI’s **GPT-3.5** for alignment. GPT predicts which Chinese phrase best corresponds to an English chunk, allowing for more flexible, context-aware alignment.

Once the alignment is established, the program **validates and applies the results**, marking tokens as **aligned or unaligned**. It then analyzes **POS shifts**, which helps understand how grammatical categories transform between languages—useful for studying **linguistic translation patterns**. 

The output includes:
- Sentence-aligned texts
- Token annotations with alignment data
- POS shift statistics, showing how words change categories during translation

This tool is particularly useful for **linguists, translation researchers, and NLP practitioners** looking to explore translation alignment in a more **data-driven** way.
# Text Alignment and POS Shift Analysis

This Python program performs **automatic text alignment and linguistic analysis** between English and Chinese translations. It leverages **spaCy** for tokenization and **OpenAI's GPT-3.5** for chunk-based alignment. The program also calculates **Part-of-Speech (POS) shift probabilities** to analyze translation shifts.

## Features
- **Sentence Splitting:** Uses `spaCy` for English and `jieba` for Chinese.
- **Tokenization & Annotation:** Each token is annotated with **POS tags, dependencies, and alignment properties**.
- **Chunk-Based Alignment:** Aligns smaller phrase chunks via **OpenAI GPT API**.
- **Alignment Validation & Application:** Stores alignment results for further linguistic analysis.
- **POS Shift Probability Calculation:** Analyzes **word category shifts** between source and target text.

## Dependencies
- Python 3.8+
- `spacy`
- `jieba`
- `openai`
- `pandas`
- `json`
- `logging`

## Installation
```bash
pip install spacy jieba openai pandas
python -m spacy download en_core_web_sm
python -m spacy download zh_core_web_sm
```

## Usage
1. **Prepare input text files:**
   - `original_text.txt` (English source text)
   - `german_translation.txt` (Chinese translation)

2. **Run the script**:
   ```bash
   python align_text.py
   ```

3. **Output Files**:
   - Sentence tokenized texts: `source_sentences.txt`, `target_sentences.txt`
   - Annotations: `source_annotations.jsonl`, `target_annotations.jsonl`
   - POS shift probabilities: `pos_shift_probabilities.csv`
   - Alignment statistics: `alignment_phenomena_probabilities.csv`

## Key Functions
- `read_text(file_path)`: Reads and normalizes text from input files.
- `split_sentences(nlp, text)`: Splits text into sentences using **spaCy**.
- `annotate_and_get_tokens_english(nlp, sentences)`: Tokenizes and annotates English text.
- `annotate_and_get_tokens_chinese(sentences)`: Tokenizes and annotates Chinese text using **jieba**.
- `chunk_tokens(tokens, max_chunk_size=10)`: Splits token sequences into smaller chunks.
- `align_chunks_with_chatgpt(source_chunks, target_chunks)`: Uses **OpenAI GPT** to align English and Chinese chunks.
- `apply_chunk_alignments(source_annotations, target_annotations, alignments)`: Applies alignments to token annotations.
- `compute_alignment_phenomena(source_annotations)`: Computes **POS shift probabilities**.

## Logging & Debugging
- Logs are saved to **`alignment_debug.log`**.
- Run with **`DEBUG`** level logging for detailed insights.

## Notes
- The OpenAI API key must be configured before running the script.
- The **source and target texts must be pre-aligned at the sentence level**.
- The program includes **error handling and retries** for OpenAI API requests.

This tool is useful for **computational translation studies, corpus linguistics, and NLP-based translation evaluation**. 🚀
