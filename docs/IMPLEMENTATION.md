# Implementation Notes

This project currently centers on the temple divination flow. The most relevant source files are:

- `src/app/App.tsx`
  - Main client program for the experience
  - Owns the visible title and welcome message
  - Controls the realtime conversation UI and session behavior

- `src/app/api/session/route.ts`
  - Creates the OpenAI Realtime session
  - This project currently uses the Realtime v2 path
  - Requires `OPENAI_API_KEY` on the server side

- `src/app/agentConfigs/aigoCustomerService.ts`
  - Main temple-divination agent configuration
  - The `instructions` field is where the system-style prompt text is assembled before being passed into the agent config

## Deployment requirement

When deploying to Vercel, add `OPENAI_API_KEY` to the environment variables for the project. Without it, the session route cannot create a Realtime session.
