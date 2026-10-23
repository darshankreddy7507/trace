# UI Lens

**Turn a screenshot into a runnable React component with Gemma 4.**

UI Lens is an AI-powered screenshot-to-React tool. Upload a UI screenshot, provide instructions, and generate a React + TypeScript component that you can inspect, edit, and refine.

This project adapts the open-source [Trace](https://github.com/forbiddenlink/trace) codebase and integrates Gemma 4 into its screenshot-to-React generation workflow.

## What It Does

- **Screenshot-to-React:** Convert a screenshot and text instructions into structured output for React component generation.
- **Visual understanding:** Provide a screenshot to the model alongside instructions describing the desired interface.
- **Live preview:** Inspect generated components in the existing editable preview environment.
- **Code validation and repair:** Use the existing project's validation and repair workflow to help resolve generation errors.
- **Iterative refinement:** Improve generated interfaces through additional instructions using supported features of the application.
- **Accessibility analysis:** Use the existing accessibility analysis and remediation features where supported by the application.

## Gemma 4 Integration

UI Lens uses **Gemma 4 (`gemma-4-26b-a4b-it`)** through Google's Gemini API.

### Model details

- **Model:** `gemma-4-26b-a4b-it`
- **API provider:** Google Gemini API
- **Integration file:** `api/generate.ts`
- **Model configuration:** `GEMINI_MODEL`
- **Inputs:** Screenshot image and text instructions
- **Output:** Structured model output used by the existing React generation workflow

### How It Works

1. The user uploads a screenshot and provides instructions.
2. The backend prepares the image and prompt.
3. `api/generate.ts` calls the configured model using the Google provider from the AI SDK.
4. Gemma 4 processes the image and instructions and returns structured output.
5. UI Lens processes the output through the existing generation workflow to produce and preview a React interface.

The model is accessed through Google's hosted API; the model weights are not bundled with this repository.

### Why Gemma 4?

Screenshot-to-React generation requires visual understanding and structured, coding-oriented output. Gemma 4's multimodal capabilities make it suitable for this workflow.

This project demonstrates the use of Gemma 4 in a practical application rather than only as a conversational chatbot. No claim is made that Gemma 4 outperforms other models without comparative benchmark results.

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vite, React, TypeScript |
| Styling | Tailwind CSS |
| AI integration | Google AI SDK provider and AI SDK |
| Model | Gemma 4 — `gemma-4-26b-a4b-it` |
| Output validation | Zod |
| Live preview | Sandpack |
| Accessibility | axe-core |
| Backend integration | `api/generate.ts` and the existing Vite development middleware |

## Getting Started

### Prerequisites

- Node.js
- pnpm
- A Google Gemini API key with access to the configured model

### 1. Clone the repository

Clone your public UI Lens repository:

```bash
git clone YOUR_PUBLIC_UI_LENS_REPOSITORY_URL
cd YOUR_PROJECT_DIRECTORY
```

Replace the placeholders with your actual repository URL and directory name.

### 2. Install dependencies

```bash
pnpm install
```

### 3. Configure environment variables

Create a local environment file:

```bash
cp .env.example .env.local
```

Add the following settings to `.env.local`:

```env
GOOGLE_GENERATIVE_AI_API_KEY=your-api-key-here
GEMINI_MODEL=gemma-4-26b-a4b-it
```

Replace `YOUR_GOOGLE_API_KEY` with your own API key. Do not share the key or commit `.env.local` to Git.

### 4. Start the development server

```bash
pnpm dev
```

Open the local URL printed in the terminal, usually:

http://localhost:5173

### 5. Try the application

1. Open UI Lens.
2. Upload a screenshot or use an available example.
3. Enter instructions for the desired interface.
4. Generate the React UI.
5. Inspect the result in the preview.

An API key may not be required for examples that use previously cached results.

## Project Structure

```text
trace/
├── api/
│   └── generate.ts    # AI model integration
├── src/               # Frontend application
├── public/            # Static assets
├── .env.example       # Environment variable template
├── package.json       # Dependencies and scripts
└── README.md
```

The exact component and asset structure may vary as the project evolves.

## Security

- Keep `GOOGLE_GENERATIVE_AI_API_KEY` on the server side.
- Never expose the key in frontend code or public logs.
- Never commit `.env.local` or other files containing secrets.
- Configure the model and API key separately for deployed environments.

## Attribution and License

UI Lens is an adaptation of the open-source **Trace** project.

Original repository: https://github.com/forbiddenlink/trace

The original MIT license and applicable copyright notices are retained. UI Lens builds on that existing codebase and integrates Gemma 4 into the screenshot-to-React workflow.

The original Trace project was created by Liz Stein. See the upstream repository for its history, original implementation, and license.

This README describes the adapted project and its configured model integration; it does not claim that the entire underlying application was written from scratch.

## Future Improvements

Potential improvements include:

- Comparing generated UI quality across different models.
- Improving screenshot fidelity and responsive layouts.
- Adding more robust generation evaluation.
- Improving handling of low-confidence visual regions.
- Expanding test coverage for generated components.
