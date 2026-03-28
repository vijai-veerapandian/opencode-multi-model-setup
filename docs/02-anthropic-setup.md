# 02 - Anthropic Setup

To integrate the Anthropic API with OpenCode, you need an API key from your Anthropic Console. This enables access to powerful Claude 3 models.

## API Setup

1. **Obtain API Key**: Navigate to [https://console.anthropic.com/](https://console.anthropic.com/), sign in, and create a new API key.
2. **Environment Variable**: Configure the `ANTHROPIC_API_KEY` in `configs/.zshrc-exports.sh`. Add the following line:

   ```bash
   export ANTHROPIC_API_KEY="sk-ant-xxxxxxxxxxxxxxxxxxxxxxxx"
   ```

3. **Source Configuration**: Reload your shell config:

   ```bash
   source configs/.zshrc-exports.sh
   ```

## Configuration in OpenCode JSON

If you use `opencode-config.json`, configure the endpoint/keys like so under the specific models block:

```json
{
  "models": {
    "claude3-opus": {
      "provider": "anthropic",
      "model": "claude-3-opus-20240229",
      "apiKey": "${ANTHROPIC_API_KEY}"
    },
    "claude3-sonnet": {
     "provider": "anthropic",
     "model": "claude-3-5-sonnet-20240620",
     "apiKey": "${ANTHROPIC_API_KEY}"
    }
  }
}
```

Once defined, you can seamlessly switch to testing your multi-model deployment utilizing Claude.
