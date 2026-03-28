# 05 - Local Models setup with Ollama for OpenCode

To configure `opencode` (or any compatible OpenAI API client) to talk to your locally hosted models via Ollama, you must set the endpoint URL and specify the downloaded model name.

## Configuration

For local development where you've deployed Ollama using our Kubernetes Gateway or MetalLB configurations on an IP such as `192.168.2.240`, configure `opencode` to route requests to that endpoint.

### Method 1: Environment Variables

Set the environment variables in your terminal session or add them to your `~/.zshrc-exports.sh`:

```bash
export OPENAI_API_BASE="http://192.168.2.240/v1"
export OPENAI_API_KEY="ollama" # Provide a dummy key
export OPENAI_MODEL_NAME="qwen2.5-coder:7b"
```

### Method 2: OpenCode Config JSON

Open `configs/opencode-config.json` and declare your model details within the providers array:

```json
{
  "models": {
    "local-ollama": {
      "provider": "openai",
      "model": "qwen2.5-coder:7b",
      "apiBase": "http://192.168.2.240/v1",
      "apiKey": "ollama"
    }
  },
  "defaultModel": "local-ollama"
}
```

## Supported Local Models

In our current deployment, we are pulling `qwen2.5-coder:7b`. You can update `ollama-k8s/deployment.yaml` or `helm/ollama-values.yaml` to pull additional models such as `llama3:8b` or `mistral-nemo`.

Wait for the deployment to spin up the container and successfully download your new model, then adjust `OPENAI_MODEL_NAME` accordingly.
