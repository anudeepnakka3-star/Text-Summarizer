# Text Summarizer

An AI-powered dialogue summarization application built with FastAPI and a fine-tuned T5 transformer model. The app accepts a conversation, cleans the input, and generates a concise summary through a simple web interface or a JSON API.

## Features

- Summarizes conversations and other dialogue-style text.
- Uses a locally saved T5 model for inference.
- Automatically uses available CUDA, Apple MPS, or CPU hardware.
- Provides a browser-based interface.
- Exposes a `/summarize/` API endpoint for programmatic use.
- Includes the SAMSum training, validation, and test datasets and the model-training notebook.

## Technology

- Python
- FastAPI
- PyTorch
- Hugging Face Transformers
- HTML, CSS, and JavaScript
- T5 text-to-text transformer model

## Project Structure

```text
app.py                    FastAPI application and summarization logic
index.html                Web interface
text_summarizer.ipynb     Model training and experimentation notebook
saved_summary_model/      Locally saved model and tokenizer files
samsum-train.csv         Training dataset
samsum-validation.csv    Validation dataset
samsum-test.csv          Test dataset
```

## Setup

1. Create and activate a virtual environment:

	```bash
	python -m venv .venv
	```

	Windows PowerShell:

	```powershell
	.\.venv\Scripts\Activate.ps1
	```

2. Install the dependencies:

	```bash
	pip install fastapi uvicorn torch transformers sentencepiece jinja2 python-multipart
	```

3. Make sure the `saved_summary_model` directory is present in the project root. The application loads the model from this directory when it starts.

4. Start the server:

	```bash
	uvicorn app:app --reload
	```

5. Open [http://127.0.0.1:8000](http://127.0.0.1:8000) in a browser.

## API Usage

Send a `POST` request to `/summarize/` with a JSON body containing a `dialogue` field:

```bash
curl -X POST http://127.0.0.1:8000/summarize/ ^
  -H "Content-Type: application/json" ^
  -d "{\"dialogue\":\"Alex: Are we meeting at 10? Jamie: Yes, see you then.\"}"
```

Example response:

```json
{
  "summary": "Alex and Jamie agree to meet at 10."
}
```

## Notes

- Input text is normalized and truncated to the model's 512-token input limit.
- The model and virtual environment are kept out of Git when listed in `.gitignore`. Ensure the model files are available locally before running the app.
