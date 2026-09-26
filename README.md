# Beq-Cli

A minimal terminal agent powered by local (or remote) language models.

One tool: the shell. Optional image understanding. Optional int4/int8 quantization.
Works on **Linux**, **Windows**, and macOS.

## Quick Start

```bash
# Install dependencies
pip install -r requirements.txt

# Launch (small default model, downloads on first run)
python run.py
```

Pick any Hugging Face model or a local weights directory:

```bash
python run.py org/model-name
python run.py org/model-name --bits 4
python run.py weights/my-model-int4
```

Or point the same agent at any OpenAI-compatible endpoint:

```bash
python run.py --url https://api.example.com/v1/chat/completions \
              --api-key $BEQ_CLI_API_KEY --model some-model
```

## Use as a library

```python
from beq_cli import Model, Processor

model = Model.from_pretrained("weights/my-model")
processor = Processor.from_pretrained("weights/my-model")

messages = [
    {"role": "user", "content": [
        {"type": "text", "text": "Describe this image in one sentence."},
        {"type": "image", "image": "photos/cat.jpg"},
    ]},
]
inputs = processor(messages, add_generation_prompt=True, device="cpu")

for token_id in model.generate_stream(
    **inputs, max_new_tokens=256, stop_tokens=processor.stop_tokens
):
    print(processor.tokenizer.decode([token_id]), end="", flush=True)
```

## Packaging (Windows & Linux)

See [BUILD.md](BUILD.md) for producing standalone executables with PyInstaller.

## License

MIT
