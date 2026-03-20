# Mistral Common

[![pypi](https://img.shields.io/pypi/v/mistral-common)](https://pypi.org/project/mistral-common/)
[![License: Apache 2](https://img.shields.io/github/license/mistralai/mistral-common)](LICENSE)

The Mistral Common library contains the utilities and watertight tokenizers that we use in our internal work.

It contains:
- a [tokenizer](./mistral_common/tokens) based on [ tiktoken](https://github.com/openai/tiktoken) and [ sentencepiece](https://github.com/google/sentencepiece) with the official chat templates.
- a [vision tokenizer](./mistral_common/tokens/vision) to tokenize images
- [integration](./mistral_common/insiders) with huggingface hub to load models from the hub and convert weights.
- utilities to handle [batch](./mistral_common/serialization) inference.

## Installation

You can install mistral-common via pip:

```bash
pip install mistral-common
```

## Usage

### Tokenization

To tokenize text using the official Mistral tokenizer:

```python
from mistral_common.tokens.tokenizer import MistralTokenizer

tokenizer = MistralTokenizer.from_model("mistral-large-latest")
tokenizer.encode("A random string")
```

If you want to use the tokenizer for the open model:

```python
from mistral_common.tokens.tokenizer import MistralTokenizer

tokenizer = MistralTokenizer.from_model("open-mistral-7b")
tokenizer.encode("A random string")
```

### Chat Templates

We also provide the official chat templates.

For the instruction fine-tuning (like Mistral 7B):
```python
from mistral_common.tokens.tokenizer import MistralTokenizer

tokenizer = MistralTokenizer.from_model("open-mistral-7b")

# messages as a list of tuples (role, content)
messages = [("user", "Hello"), ("assistant", "Hi")]
tokenizer.encode_chat(messages)
```

For the function calling models (like Mistral Large):
```python
from mistral_common.tokens.tokenizer import MistralTokenizer

tokenizer = MistralTokenizer.from_model("mistral-large-latest")

# messages as a list of tuples (role, content)
messages = [("user", "Hello"), ("assistant", "Hi")]
tools = [...] # tool call definitions
tokenizer.encode_chat(messages, tools=tools)
```

### Using the tokenizers from HuggingFace

It is possible to instantiate the tokenizer from HuggingFace in a couple of ways:

1. By using the model name:
```python
from transformers import AutoTokenizer
from mistral_common.tokens.huggingface import mistral_tokenizer_choices

tokenizer = AutoTokenizer.from_model("mistralai/Mistral-7B-Instruct-v0.2", **mistral_tokenizer_choices)
```

2. By passing the tokenizer configuration:
```python
from transformers import AutoTokenizer
from mistral_common.tokens.huggingface import MistralHuggingFaceTokenizer

tokenizer = AutoTokenizer.from_pretrained(
    "mistralai/Mistral-7B-Instruct-v0.2",
    tokenizer_class=MistralHuggingFaceTokenizer,
)
```

## Developing

To develop on this repo, you'll need to have [Rye](https://github.com/astral-sh/rye) installed.
If you're on macOS, you can use `brew install rye`.

Then, you can install the dependencies with:

```bash
rye sync
```

And run the tests with:

```bash
rye run pytest
```

To format and lint the code:

```bash
rye run fmt
rye run lint
```

## Community

Discover the official [Mistral docs](https://docs.mistral.ai/), the community [Discord](https://discord.com/invite/mistralai) for troubleshooting and general discussion, and explore our [community license](LICENSE.md) for using Mistral models.

## Related projects

1. related project [openai-python](https://github.com/openai/openai-python)
2. related project [anthropic-sdk-python](https://github.com/anthropics/anthropic-sdk-python)
