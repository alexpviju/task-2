# 🕒 Date-Time Extraction with LLM and Regex

This project extracts structured date and time information (e.g., exact datetime or time range) from natural language inputs using a lightweight language model (`flan-t5-base`) and custom regular expressions.

---

## 🚀 Overview

The goal is to convert vague human-readable expressions like:

> "yesterday evening around 9:30"  
> "next Friday between 3–5 pm"  

into structured **JSON** outputs like:

```json
{
  "date": "yesterday",
  "time": "9:30 pm"
}
```

---

## 🧱 Components

### ✅ 1. Language Model (LLM)
- **Model**: `google/flan-t5-base`
- **Framework**: [Hugging Face Transformers](https://huggingface.co/docs/transformers)
- Purpose: Generates normalized datetime expressions from messy user input.

### ✅ 2. Regex Parser
- Uses `re` module to extract:
  - 📅 Date (full/short month names, "yesterday", "today", etc.)
  - ⏰ Time (e.g., "9:30 pm", "3–4 pm")
  - ☀️ Time of day inference (e.g., "evening" → PM)

---

## 📦 Installation

Make sure you have Python 3.8+ and run:

```bash
pip install transformers
pip install torch
pip install python-dotenv
```

---

## 🧪 Usage

### Step 1: Load Model

```python
from transformers import pipeline
llm = pipeline("text2text-generation", model="google/flan-t5-base", max_length=256)
```

### Step 2: Prompt and Response

```python
prompt = "Extract the exact datetime or time range from this: yesterday evening around 9:30"
response = llm(prompt)[0]['generated_text']
print("📤 Raw response:", response)
```

### Step 3: Parse Response

```python
parsed_output = parse_time_response(response)
print("🗓️ Parsed JSON:", json.dumps(parsed_output, indent=2))
```

---

## 📜 `parse_time_response()` Logic

- Extracts `date`, `time`, or `time_range` from the model's response.
- Handles short and long month names.
- Infers AM/PM using keywords like `evening`, `morning`, etc.
- Fallback error message if nothing is parsed.

---

## 📂 Example Output

Input:  
`"yesterday evening around 9:30"`

Output:
```json
{
  "date": "yesterday",
  "time": "9:30 pm"
}
```

---

## 📌 Notes

- No fine-tuning required — uses pre-trained lightweight LLM.
- Inference can be run locally on CPU.
- You may customize prompts for better precision.

---

## 🧠 Future Improvements

- Use `datetime` module to resolve relative dates (e.g., convert `"yesterday"` to ISO format).
- Improve accuracy with fuzzy date/time matching.
- Integrate into a Gradio or Streamlit app for easy UI.

---

## 🧑‍💻 Author
##  ALEX P V
## EMAIL : alexpviju26@gmail.com

Built with ❤️ using Hugging Face and Python.
