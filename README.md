# GD-ARENA
What it does
GD Arena (Problem Statement #2) is a voice-first web app for practising campus-placement Group Discussions with AI participants and a moderator. Students choose a topic, language, format, and duration, then speak or type while a turn-managed discussion unfolds. After the GD and closing round finish, the app presents transcript-linked feedback, performance metrics, and practice suggestions.

Done / Left / Plan
Done
•	Shipped the setup, live discussion room, AI moderator and participants, typed fallback, transcript, and post-session report.
•	Added English and Hinglish settings, Standard and Fishbowl formats, 5/8/10-minute sessions, adjustable captions and speech controls, and topic selection/custom topics.
•	Added the simulated Recruiter Panel Verdict, Pressure Dial, live GD Pulse, optional Topic Primer, Retry the Moment, and local progress history.
•	Updated microphone interaction: tap to start and tap again to finish, or hold Space for push-to-talk. Natural pauses no longer automatically submit the student’s turn, and the app waits briefly for final browser-recognized words before AI resumes.
•	Added server-side LLM calls with topic-specific bank/local fallbacks. TypeScript checks and the production build pass.
•	Deployed at gdarena-bzwhpycy.manus.space.

Left for the next 16 hours
•	Verify long spoken turns with pauses on desktop Chrome and check that the final transcript contains the full statement. Speech recognition quality still depends on the browser and microphone.
•	Improve live LLM reliability. Topic-pack or response calls can time out; the fallback keeps a session going but may produce less varied dialogue.
•	Run end-to-end sessions for preset and custom topics, including Fishbowl, interruptions, the closing round, and quote-linked report evidence.
•	Review report scoring and transcript metrics against sample sessions, and fix any inaccuracies found during testing.

Plan to finish
1	Hours 0–4: Test tap-to-toggle and Spacebar capture with long turns, natural pauses, and interruption recovery in desktop Chrome; inspect the resulting transcript.
2	Hours 4–8: Profile LLM timeouts and refine request latency or fallback handoff without weakening the on-topic checks.
3	Hours 8–12: Exercise UPI, work-from-home, custom-topic, and Fishbowl sessions through the closing round; verify report quotes, IDs, and computed metrics.
4	Hours 12–16: Complete responsive and keyboard-accessibility checks, fix issues from the session runs, and publish the verified update.

Architecture and why
•	Frontend — React 18, TypeScript, Vite, and Tailwind CSS. This keeps the interface responsive and supports the live setup, room, transcript, and report without a large application framework.
•	Backend — Node.js and Express 5. A small same-origin POST /api/llm proxy keeps model credentials on the server instead of exposing them in browser code. Calls are queued, bounded by a timeout, and handled with topic-bank or local fallbacks when the service is unavailable.
•	AI — the platform-provided LLM service. gpt-5-nano prepares topic packs and live participant lines; gpt-5-mini generates the structured report judgments. Structured JSON helps the app validate content and attach feedback to transcript evidence. No web-search tools are used for discussion content.
•	Real-time voice — browser Web Speech APIs. SpeechRecognition provides speech input where supported, while speechSynthesis speaks AI lines. The app serializes turns so speakers do not overlap and uses typed replies when speech input is unavailable. This avoids a separate audio-streaming or neural-TTS service.
•	Data — browser localStorage. Preferences, transcripts, and session history remain available on the same device without account setup or a database. This keeps the app simple for practice sessions.

What we added
Beyond the original core GD-practice brief, the app includes a Pressure Dial, live GD Pulse, silent Topic Primer, simulated Recruiter Panel Verdict, Retry the Moment, and local progress history. These additions make practice intensity adjustable, provide in-session cues, let students retry missed openings, and help them notice patterns across sessions.

We also refined the microphone flow with tap-to-toggle and a final-transcript collection window, while preserving Spacebar push-to-talk. This helps students finish a complete thought without needing to hold a button through every natural pause.

How to run it
Live app
•	URL: https://gdarena-bzwhpycy.manus.space
•	Test login: None. GD Arena has no sign-in or account requirement; open the site and enter the setup screen.

Local development
Requirements: Node.js 22 or later and pnpm 11.25.0.

From the project directory:

pnpm install
pnpm dev

Open http://localhost:3000. Vite serves the frontend on port 3000; Express serves the API on port 3001, with /api requests proxied during development.

For live AI locally, provide the server process with either the platform-provided BUILT_IN_FORGE_API_URL and BUILT_IN_FORGE_API_KEY, or the supported MANUS_API_URL and MANUS_API_KEY pair. Configure these as server-side environment variables; never commit credentials or expose them through client-side variables. Without the LLM service, the room can use prepared or local fallback lines.

Useful commands:

pnpm check   # TypeScript and server syntax checks
pnpm build   # Type-check and create the production frontend in dist/

Tools and AI used
•	Libraries: React, TypeScript, Vite, Tailwind CSS, Express, Lucide React, and concurrently.
•	Browser APIs: Web Speech API (SpeechRecognition) for voice input and speechSynthesis for AI voice output.
•	AI service/models: platform-provided LLM API; gpt-5-nano for topic packs and live discussion turns, and gpt-5-mini for report analysis.
•	Server endpoint: Express POST /api/llm proxies AI requests; credentials stay server-side.
•	Disclosure: Setup and room screens state: “All other participants and the moderator are AI. Only you are human.” The Recruiter Panel Verdict is labelled as practice feedback, not a real hiring prediction.

Speech-recognition support and available voices vary by browser. GD Arena does not save microphone recordings; browser speech-recognition processing follows the browser provider’s own service and privacy terms. Transcript text is sent to the configured LLM service for live replies and report analysis.

Who it is for
GD Arena is for students and early-career job seekers preparing for campus placements who want to practise speaking clearly, entering a discussion, supporting an idea, responding to others, and closing confidently. It is useful for learners who do not have a group available for repeated practice or who want a low-pressure space to rehearse.

Users can return to try different topics and pressure settings, retry missed moments, and review locally saved session history for recurring strengths and improvement areas. The AI scores and recruiter-style verdict are practice 
