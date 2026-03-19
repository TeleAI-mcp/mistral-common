# Mistral Common

[![PyPI](https://img.shields.io/pypi/v/mistral-common)](https://pypi.org/project/mistral-common/)
[![License](https://img.shields.io/pypi/l/mistral-common)](LICENSE)

Language, tooling and potential even some model weight for Mistral AI.

## Installation

You can install `mistral-common` via pip:

```bash
pip install mistral-common
```

## Usage

```python
from mistral_common.protocol.base import *
from mistral_common.tokens.tokenizers import Tokenizer
from mistral_common.inference.chat_completion import ChatCompletion
```

## Documentation

Documentation is available at https://docs.mistral.ai/.

## Development

### Install development dependencies

You can install development dependencies using [uv](https://github.com/astral-sh/uv):

```bash
uv sync --all-extras
```

### Running tests

You can run tests with pytest:

```bash
pytest tests/
```

### Running linting

We use [ruff](https://docs.astral.sh/ruff/) for linting and formatting:

```bash
ruff check .
ruff format .
```

We use [mypy](https://mypy-lang.org/) for type checking:

```bash
mypy .
```

### Release

For releasing we use [Commitlint](https://commitlint.js.org/#/) and [semantic-release](https://github.com/semantic-release/semantic-release).

This project adheres to the [Conventional Commits](https://www.conventionalcommits.org/) specification.

Use `git cz` or `npm commit` (after running `npm install`) to make commits.

Releases are done automatically on the CI when a commit message with specific format is pushed to the `main` branch or a PR is merged.
The release process is handled by [semantic-release](https://github.com/semantic-release/semantic-release) which will automatically create a CHANGELOG and bump the version for you.

## Related projects

1. related project [openai-python](https://github.com/openai/openai-python)
2. related project [anthropic-sdk-python](https://github.com/anthropics/anthropic-sdk-python)