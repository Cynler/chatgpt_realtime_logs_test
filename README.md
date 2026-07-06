# 宮廟解籤 Realtime Demo

This project is a Next.js + OpenAI Realtime voice app that has been redirected from a generic multi-agent demo toward a **宮廟解籤** experience.

The current focus is a Traditional Chinese, voice-friendly temple divination assistant that helps users:
- ask for a 籤號
- receive a concise, plain-language interpretation of the 籤意
- continue the same divination thread with follow-up questions
- keep the conversation structured, short, and suitable for speech

The current app centers on:
- `宮廟解籤` as the primary interaction pattern
- Traditional Chinese responses
- concise spoken replies
- strict sign-number handling and flow control
- a stateful conversation structure for asking the sign number, interpreting the sign, and then narrowing the user's topic

## Features

- Realtime voice conversation through OpenAI Realtime
- Temple-divination prompt flow built around `解籤`
- Transcript view and event log for debugging
- Audio playback controls and push-to-talk / voice activity detection options
- Multiple agent configs remain available for experimentation, but the temple divination flow is the current default direction

## Setup

1. Install dependencies:

   ```bash
   npm install
   ```

2. Add your `OPENAI_API_KEY` to the environment.

   You can use a local `.env` file or your shell profile.

3. Start the development server:

   ```bash
   npm run dev
   ```

4. Open the app in your browser:

   ```text
   http://localhost:3000
   ```

## Usage

The current experience is designed around a temple-style oracle flow.

Typical entry points:
- tell the assistant which籤 you drew
- ask for a plain-language explanation of the sign
- continue with the same sign if you want to ask about career, relationships, money, health, or other concerns

The assistant is instructed to keep answers:
- in Traditional Chinese
- short enough for voice playback
- direct and non-ornamental
- focused on interpretation, not on unrelated conversation

## Repository layout

- `src/app/api/session/route.ts` creates the Realtime session and returns the ephemeral token
- `src/app/App.tsx` contains the main client experience
- `src/app/agentConfigs/` contains the agent prompt sets and flow logic
- `src/app/components/` contains the transcript, event log, toolbar, and related UI pieces
- `src/app/hooks/` contains event handling and audio helpers
- `src/app/lib/` contains Realtime connection and utility code

## Temple-divination flow

The temple flow is organized as a structured conversation:

1. Ask for the sign number
2. Interpret the sign in plain language
3. Ask what area the user wants to understand
4. Collect the minimum context needed for the follow-up explanation
5. Deliver the final reading in one clear pass

The prompt set also includes guardrails for:
- sign-number locking
- translation and rephrasing of the latest divination content
- one-question-at-a-time behavior
- avoiding unrelated topics
- keeping replies suitable for speech

## Notes

- This repo is still an agent playground under the hood, but the current product direction is clearly temple divination rather than customer-service simulations.
- The UI includes transcript and event panels for inspecting the realtime exchange while developing or debugging the flow.

## Current implementation notes

- `src/app/App.tsx` is the main application entry point for the live experience. It owns the visible title, the welcome message, and the conversation behavior.
- `src/app/api/session/route.ts` now targets the Realtime API v2 flow used by this project. The session creation logic is handled there.
- `src/app/agentConfigs/aigoCustomerService.ts` holds the main temple-divination prompt set. The `instructions` field is where the system-style prompt text is assembled and passed into the agent config.
- Vercel deployment must include `OPENAI_API_KEY` in the environment, or the session route cannot create a Realtime session.

## Deployment

For Vercel:

1. Add `OPENAI_API_KEY` in the project environment variables.
2. Confirm the Realtime model setting used by `src/app/api/session/route.ts` matches the account capability you want to deploy with.
3. Deploy the app normally through Vercel after the secret is set.

## License

MIT
