# assessment-for-internship

# Vedaz Astrology Assistant - Qwen2.5 Fine-tuning

## Overview

This project demonstrates fine-tuning the **Qwen2.5-3B-Instruct** model on a custom astrology conversation dataset using **LoRA** with **Unsloth**. The fine-tuned model is intended to provide empathetic, safety-aware Vedic astrology conversations.

---

## Model

- Base Model: Qwen2.5-3B-Instruct
- Fine-tuning Method: LoRA
- Framework: Unsloth
- Training Library: TRL (SFTTrainer)

---

## Dataset

- 55 multi-turn astrology conversations
- Topics include:
  - Marriage
  - Career
  - Business
  - Foreign travel
  - Relationships
  - Health safety
  - Emotional support

---

## Training Configuration

| Parameter | Value |
|----------|-------|
| Epochs | 3 |
| Learning Rate | 2e-4 |
| Batch Size | 2 |
| Gradient Accumulation | 4 |
| Max Sequence Length | 2048 |

---

## Project Structure

```
.
├── FineTune_Qwen.ipynb
├── dataset.json
├── vedaz_qwen_lora/
├── vedaz_qwen_merged/
├── hosting_vllm.md
├── sample_chats.md
├── training_logs.csv
└── README.md
```

---

## Running Inference

```python
from transformers import AutoTokenizer, AutoModelForCausalLM
```

Load the merged model and generate responses using the tokenizer's chat template.

---

## Deploying with vLLM

Install:

```bash
pip install vllm
```

Run:

```bash
python -m vllm.entrypoints.openai.api_server \
  --model vedaz_qwen_merged \
  --host 0.0.0.0 \
  --port 8000
```

---

## Results

- Successfully fine-tuned the model on 55 conversations.
- Generated astrology-style conversational responses.
- Merged LoRA weights for deployment.

---

## Future Improvements

- Increase training dataset size.
- Integrate Swiss Ephemeris for real kundli calculations.
- Add evaluation metrics.
- Improve multilingual performance.

---
## Model

Fine-tuned model is available on Hugging Face:

https://huggingface.co/prudvireddy-hug/vedaz-qwen2.5-astrologer

---

## Author

Allagadda Prudvi Reddy
