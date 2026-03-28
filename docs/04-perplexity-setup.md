# 04 - Perplexity Setup

Perplexity offers fast query-driven language models using Sonar, suitable for search-assisted reasoning. In your multi-model repository, integrate this by setting up its `PERPLEXITY_API_KEY`.

## Setup Checklist

1. Log into your Perplexity dashboard at [https://www.perplexity.ai/settings/api/](https://www.perplexity.ai/settings/api/).
2. Deposit trial credits or link payment to secure an active API wrapper.
3. Configure the underlying key.

Open `.zshrc-exports.sh` inside the `configs/` directory.

Add the corresponding secret line:

```bash
export PERPLEXITY_API_KEY="pplx-xxxxxxxxxxxxxxxxxxxxxxx"
```

## Adding into Config

Inside `configs/opencode-config.json`, Perplexity operates effectively as an OpenAI-compatible endpoint.

```json
{
  "models": {
    "sonar-pro": {
      "provider": "openai",
      "model": "llama-3.1-sonar-large-128k-online",
      "apiBase": "https://api.perplexity.ai/",
      "apiKey": "${PERPLEXITY_API_KEY}"
    }
  }
}
```

Reload your environment context to proceed.
```bash
source configs/.zshrc-exports.sh
```
