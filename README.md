GD Arena
Voice-first AI-powered Group Discussion practice for campus
placements.
Live app: https://gdarena-bzwhpycy.manus.space
GD Arena helps students and early-career job seekers practise
campus-placement Group Discussions (GDs) in a low-pressure environment.
Choose a topic, language, format, and session duration, then speak or
type while AI participants and an AI moderator guide the discussion.
After the discussion and closing round, review transcript-linked
feedback, performance metrics, and suggestions for improvement.
Practice-only disclosure: All other participants and the moderator
are AI. Only you are human. The Recruiter Panel Verdict is simulated
practice feedback, not a real hiring prediction.

Features
GD practice room
- Voice-first discussions with a typed-reply fallback.
- AI moderator and multiple AI participants, with turn management to
  reduce overlapping speech.
- Preset topics and custom topics.
- English and Hinglish language settings.
- Standard and Fishbowl discussion formats.
- Session durations of 5, 8, or 10 minutes.
- Live transcript, adjustable captions, and speech controls.
- A closing round to practise summarising and finishing confidently.
Feedback and practice tools
- Transcript-linked report: Review feedback supported by
  discussion evidence.
- Performance metrics: See indicators of discussion performance
  and areas to improve.
- Recruiter Panel Verdict: A simulated, practice-oriented verdict.
- Pressure Dial: Adjust the intensity of the practice session.
- Live GD Pulse: Get in-session cues about the discussion.
- Topic Primer: Optionally review a brief topic introduction
  before starting.
- Retry the Moment: Rehearse a missed opening or discussion
  moment.
- Local progress history: Review previous sessions saved on the
  same device.
Voice interaction
- Tap the microphone to start speaking and tap again to finish.
- Hold Space for push-to-talk.
- Natural pauses do not automatically submit a turn.
- After you finish speaking, the app briefly waits for final
  browser-recognised words before the AI continues.
- AI lines can be spoken using the browser's speech synthesis where
  supported.
Speech recognition quality and available voices depend on the browser,
microphone, and device.
How it works
1. Open GD Arena and select a topic or enter a custom topic.
2. Choose English or Hinglish, Standard or Fishbowl format, and a 5-,
   8-, or 10-minute session.
3. Optionally read the Topic Primer and adjust practice pressure and
   speech settings.
4. Join the discussion. Speak using the microphone controls or type
   your response.
5. Participate in the discussion and closing round.
6. Review the transcript, feedback, performance metrics, and suggested
   next steps.
7. Return later to practise another topic and review local session
   history.
Technology stack
  Layer                   Technology              Purpose
  Frontend                React 18, TypeScript,   Responsive setup,
                          Vite, Tailwind CSS      discussion room,
                                                  transcript, and report
                                                  interface
  Backend                 Node.js, Express 5      Server endpoint for AI
                                                  requests
  AI                      Platform-provided LLM   Topic packs, live
                          service                 participant turns, and
                                                  structured report
                                                  analysis
  Voice input             Browser Web Speech API  Converts supported
                          (SpeechRecognition)   browser speech input
                                                  into text
  Voice output            Browser                 Speaks AI participant
                          speechSynthesis       and moderator lines
  Icons                   Lucide React            Interface icons
  Local persistence       Browser localStorage  Stores preferences and
                                                  session history on the
                                                  current device
  Development scripts     concurrently and pnpm Runs and manages
                                              development tasks
Architecture
Frontend
The React and TypeScript frontend is built with Vite and styled using
Tailwind CSS. It manages setup options, the live room, captions,
transcript, and post-session report.
Backend and AI requests
The Node.js and Express server exposes a same-origin POST /api/llm
endpoint. This proxy keeps AI service credentials on the server instead
of exposing them in browser code. Requests are queued and bounded by a
timeout. If the AI service is unavailable or a request times out, the
app can use prepared topic-bank or local fallback content to keep a
practice session moving.
Models and structured output
The platform-provided LLM service uses: - gpt-5-nano for topic
packs and live discussion turns. - gpt-5-mini for structured
report judgments and feedback.
Structured JSON responses help the application validate generated
content and connect report feedback to transcript evidence. Discussion
content does not use web-search tools.
Voice and turn management
The app uses browser speech recognition for voice input where supported
and browser speech synthesis for AI voice output. Turns are serialised
to reduce overlapping speakers. Typed replies remain available when
speech input is unavailable or unsuitable.
Data storage
Preferences, transcripts, and session history are saved in browser
localStorage. There is no account or database requirement for normal
practice sessions, and the saved history is local to the browser/device.
Development status
Completed
- Setup flow, live discussion room, AI moderator and participants,
  typed fallback, transcript, and post-session report.
- English and Hinglish settings; Standard and Fishbowl formats; 5-,
  8-, and 10-minute sessions.
- Adjustable captions and speech controls, preset topic selection, and
  custom topics.
- Recruiter Panel Verdict, Pressure Dial, live GD Pulse, optional
  Topic Primer, Retry the Moment, and local progress history.
- Tap-to-toggle microphone interaction and Spacebar push-to-talk.
- Improved handling of natural pauses and a short wait for final
  browser-recognised words before AI continuation.
- Server-side LLM proxy and topic-bank/local fallbacks.
- TypeScript checks and production build pass.
Remaining validation and improvement work
- Test long spoken turns with natural pauses in desktop Chrome and
  verify that the full statement appears in the transcript.
- Investigate AI request timeouts and improve latency or fallback
  handoff while preserving topic relevance.
- Run end-to-end tests for preset and custom topics, Fishbowl
  sessions, interruptions, the closing round, and quote-linked report
  evidence.
- Compare report scoring and transcript metrics against sample
  sessions and correct inaccuracies.
- Complete responsive-layout and keyboard-accessibility checks, fix
  issues found during testing, and publish a verified update.
Planned testing schedule
1. Hours 0--4: Test tap-to-toggle and Spacebar capture with long
   turns, natural pauses, and interruption recovery in desktop Chrome;
   inspect transcripts.
2. Hours 4--8: Profile LLM timeouts and refine latency or fallback
   handoff without weakening on-topic checks.
3. Hours 8--12: Test UPI, work-from-home, custom-topic, and
   Fishbowl sessions through the closing round; verify report quotes,
   IDs, and computed metrics.
4. Hours 12--16: Complete responsive and keyboard-accessibility
   checks, fix issues found during testing, and publish the verified
   update.
Run locally
Requirements
- Node.js 22 or later
- pnpm 11.25.0
Install dependencies
From the project root:
pnpm install
Start development servers
pnpm dev
Open http://localhost:3000.
During development, Vite serves the frontend on port 3000, Express
serves the API on port 3001, and /api requests are proxied to the
backend.
Configure AI access
For live AI responses locally, provide the server process with either: -
BUILT_IN_FORGE_API_URL and BUILT_IN_FORGE_API_KEY, or -
MANUS_API_URL and MANUS_API_KEY.
Configure these as server-side environment variables. Never commit
credentials, put secrets in source control, or expose them through
client-side environment variables. Without the LLM service, the room can
use prepared or local fallback lines.
Useful commands
pnpm check   # Run TypeScript and server syntax checks
pnpm build   # Type-check and build the production frontend into dist/
Deployment
The current live deployment is available at:
https://gdarena-bzwhpycy.manus.space
The project is configured as a Node.js/Express application with a React
frontend. The repository includes a root-level Dockerfile for
container-based deployment. Keep server credentials configured in the
deployment environment rather than in the repository or client bundle.
Privacy and limitations
- GD Arena does not save microphone recordings.
- Browser speech-recognition processing follows the browser provider's
  own service and privacy terms.
- Transcript text is sent to the configured LLM service for live
  replies and report analysis.
- Speech-recognition support and available voices vary by browser and
  device.
- AI-generated responses and report scores may be imperfect. Treat
  them as practice guidance, not authoritative evaluation or a hiring
  decision.
- Preferences and session history are stored locally in the browser
  and are not synchronised across devices by the app.
Intended users
GD Arena is designed for students and early-career job seekers preparing
for campus placements. It helps users practise: - Speaking clearly and
confidently. - Entering a discussion at an appropriate moment. -
Supporting ideas with reasons and examples. - Responding to other
participants. - Managing interruptions and discussion pressure. -
Summarising and closing a discussion confidently.
It is especially useful for learners who do not have a group available
for repeated practice or who want a low-pressure space to rehearse.
Libraries and tools
- React
- TypeScript
- Vite
- Tailwind CSS
- Node.js
- Express 5
- Lucide React
- concurrently
- pnpm
- Browser Web Speech API (SpeechRecognition and speechSynthesis)
- Platform-provided LLM API (gpt-5-nano and gpt-5-mini)
GD Arena --- practise your ideas, improve your voice, and enter your
next Group Discussion with more confidence.
