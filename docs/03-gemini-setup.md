# 03 - Gemini Setup

To enable the Gemini API in your OpenCode multi-model environment, you need an API key from Google AI Studio or Google Cloud Vertex AI.

## Requirements

Get your primary API Key from [Google AI Studio](https://aistudio.google.com/app/apikey).

1. Open `configs/.zshrc-exports.sh`.
2. Add the following command export:

   ```bash
   export GEMINI_API_KEY="AIzaSyXXXXXXXXXXXXXXXXXXXX"
   ```

3. Update the `opencode-config.json` configuration block:

   ```json
   {
     "models": {
       "gemini-pro": {
         "provider": "google",
         "model": "gemini-1.5-pro-latest",
         "apiKey": "${GEMINI_API_KEY}"
       },
       "gemini-flash": {
         "provider": "google",
         "model": "gemini-1.5-flash-latest",
         "apiKey": "${GEMINI_API_KEY}"
       }
     }
   }
   ```

### Validation

To test that Gemini endpoints are correctly communicating via OpenCode, ensure your environment variable `GEMINI_API_KEY` is loaded:
`echo $GEMINI_API_KEY`
