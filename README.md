# Omnis AI web upload

This folder is a trimmed deployment copy of Omnis. It includes the web interface and Python API. It does not include local AI models, Ollama, the bundled Python runtime, personal data, tests, or secrets.

## Deploy on Vercel

1. Upload the contents of this folder to the root of a **private** GitHub repository, or replace the files at the root of the Omnis repository with these deployment files. Do not upload `.env` files, API keys, model folders, or runtime folders.
2. In Vercel, import the repository. Set the project root to the folder containing `app.py` and `vercel.json` (usually `.`), then deploy.
3. In the Vercel project settings, add these environment variables and redeploy:

   - `OMNIS_MODEL_API_URL` = `https://generativelanguage.googleapis.com/v1beta/openai`
   - `OMNIS_MODEL_API_KEY` = your Google AI Studio API key. Enter it only in Vercel's private environment-variable settings.
   - `OMNIS_HOSTED_MODEL` = the model ID shown as available in your AI Studio account.

The included `api-config.js` is intentionally set to an empty API base. On Vercel, this makes the page call the API on the same origin. Do not put provider keys in this file.

Image and video generation are optional and may incur provider charges. To enable them, configure `OMNIS_REPLICATE_API_TOKEN` and the appropriate `OMNIS_REPLICATE_IMAGE_MODEL` and/or `OMNIS_REPLICATE_VIDEO_MODEL` in Vercel. Review provider pricing and limits first.

## If using GitHub Pages for the interface

GitHub Pages cannot run the Python API. Deploy this project to Vercel first, then set `api-config.js` to the Vercel HTTPS origin:

```js
window.OMNIS_API_BASE = "https://YOUR-VERCEL-PROJECT.vercel.app";
```

Set `OMNIS_CORS_ORIGINS` in Vercel to the exact GitHub Pages origin, such as `https://YOUR-USERNAME.github.io` (no repository path), and redeploy both services.

Never upload local model files, Ollama, the bundled Python runtime, `.env`, or API credentials.
