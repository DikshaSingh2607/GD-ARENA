::: {align="center"}
# 🎙️ GD Arena

### AI-Powered Group Discussion Practice for Campus Placements

**Practise speaking. Build confidence. Get placement-ready.**

[🚀 Open Live App](https://gdarena-bzwhpycy.manus.space)
:::📌 About the Project
GD Arena is a voice-first web application that helps students and
early-career job seekers practise campus-placement Group Discussions
(GDs) with AI participants and an AI moderator.
Choose a topic, language, discussion format, and session duration. Then
speak or type your responses while the AI-led discussion unfolds. After
the session, review your transcript, performance metrics,
evidence-linked feedback, and suggestions for improvement.
Transparency: All other participants and the moderator are AI.
Only you are human. The Recruiter Panel Verdict is simulated practice
feedback, not a real hiring prediction.

✨ Key Features
<table>
<tr>
<td width="50%" valign="top">
🗣️ Realistic GD Practice
- Voice-first discussion with typed fallback
- AI moderator and multiple AI participants
- Turn management to reduce overlapping speech
- Preset and custom topics
- Standard and Fishbowl formats
- English and Hinglish
- 5-, 8-, and 10-minute sessions
</td>
<td width="50%" valign="top">
📊 Feedback & Improvement
- Transcript-linked performance report
- Performance metrics and improvement suggestions
- Simulated Recruiter Panel Verdict
- Live GD Pulse for in-session cues
- Pressure Dial to adjust practice intensity
- Optional Topic Primer before a session
- Retry the Moment to practise again
</td>
</tr>
<tr>
<td width="50%" valign="top">
🎧 Voice Controls
- Tap the microphone to start and stop
- Hold Space for push-to-talk
- Natural pauses do not automatically submit a turn
- Brief wait for final browser-recognised words
- AI voice output through browser speech synthesis
</td>
<td width="50%" valign="top">
📈 Progress Tracking
- Local session history
- Saved preferences and transcripts
- Review past practice sessions
- Identify recurring strengths and improvement areas
- No sign-in required
</td>
</tr>
</table>
🔄 How It Works
1. Choose your setup --- Select a preset or custom topic, language,
   format, and duration.
2. Prepare --- Optionally read the Topic Primer and adjust the
   Pressure Dial.
3. Join the discussion --- Speak through your microphone or type
   your response.
4. Interact with AI --- Practise entering the discussion,
   supporting ideas, and responding to others.
5. Complete the closing round --- Practise summarising your key
   points.
6. Review your report --- Read your transcript, feedback,
   performance metrics, and improvement suggestions.
7. Practise again --- Retry a moment, choose another topic, and
   review your local history.
🧰 Tech Stack
  Layer                   Technology              Role
  Frontend                React 18, TypeScript,   User interface and
                          Vite                    application logic
  Styling                 Tailwind CSS            Responsive layouts and
                                                  styling
  Backend                 Node.js, Express 5      Server-side API
                                                  endpoint
  AI                      Platform-provided LLM   Topic packs, live
                          service                 discussion, and report
                                                  analysis
  AI models               gpt-5-nano,           Discussion generation
                          gpt-5-mini            and structured feedback
  Speech input            Web Speech API          Browser-based speech
                          (SpeechRecognition)   recognition
  Speech output           speechSynthesis       AI participant and
                                                  moderator voice
  Icons                   Lucide React            Interface icons
  Local storage           Browser localStorage  Preferences and session
                                                  history
  Tooling                 pnpm, concurrently      Dependency management
                                              and development scripts
🏗️ Architecture
┌──────────────────────────────────────┐
│          React + TypeScript          │
│   Setup · Live GD Room · Transcript  │
│             · Report                 │
└──────────────────┬───────────────────┘
                   │
                   ▼
┌──────────────────────────────────────┐
│        Node.js + Express 5           │
│             POST /api/llm            │
│  Server-side credentials · Timeout  │
│       Queue · Fallback handling      │
└──────────────────┬───────────────────┘
                   │
                   ▼
┌──────────────────────────────────────┐
│       Platform-provided LLM API      │
│  gpt-5-nano: topics and live turns    │
│  gpt-5-mini: structured report       │
└──────────────────────────────────────┘

Browser APIs: SpeechRecognition + speechSynthesis
Local data:   localStorage
Frontend
React, TypeScript, Vite, and Tailwind CSS power the setup flow, live
room, captions, transcript, and post-session report.
Backend and AI
The Express server provides a same-origin POST /api/llm endpoint. AI
credentials remain on the server rather than being exposed in browser
code. Requests are queued and limited by a timeout; prepared topic-bank
or local fallback content can keep a session moving if the AI service is
unavailable.
AI response generation
- gpt-5-nano prepares topic packs and live participant
  responses.
- gpt-5-mini generates structured report judgments and feedback.
Structured JSON helps the app validate responses and link feedback to
transcript evidence. Discussion content does not use web-search tools.
Voice and data
The app uses browser speech recognition for input and browser speech
synthesis for AI voice output, where supported. Turns are serialised to
reduce overlapping speech. Preferences, transcripts, and session history
are stored in browser localStorage, so there is no account or database
requirement for normal practice sessions.
🚀 Run Locally
Prerequisites
- Node.js: 22 or later
- pnpm: 11.25.0
1. Clone the repository
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd <YOUR_PROJECT_DIRECTORY>
Replace the placeholders with your actual repository URL and project
directory.
2. Install dependencies
pnpm install
3. Start the development servers
pnpm dev
Open http://localhost:3000 in your browser.
During development: - Vite serves the frontend on port 3000. - Express
serves the API on port 3001. - /api requests are proxied to the
backend.
4. Configure AI access
For live AI responses locally, provide the server process with one
of these environment-variable pairs:
- BUILT_IN_FORGE_API_URL and BUILT_IN_FORGE_API_KEY
- MANUS_API_URL and MANUS_API_KEY
Keep credentials in server-side environment variables. Never commit
API keys or expose secrets through client-side variables. Without the
LLM service, prepared or local fallback responses may still be
available.
5. Useful commands
pnpm check   # TypeScript and server syntax checks
pnpm build   # Type-check and build the frontend into dist/
🌐 Live Deployment
Try GD Arena: https://gdarena-bzwhpycy.manus.space
No test login is required. Open the application and enter the setup
screen.
The project uses a React frontend with a Node.js/Express backend and
includes a root-level Dockerfile for container-based deployment.
Configure server credentials through your hosting platform's environment
settings.
✅ Development Status
Implemented
- [x] Setup flow, live discussion room, AI moderator, and AI
  participants
- [x] Typed fallback, transcript, and post-session report
- [x] English/Hinglish, Standard/Fishbowl, and 5/8/10-minute options
- [x] Preset and custom topics, captions, and speech controls
- [x] Pressure Dial, live GD Pulse, Topic Primer, and Retry the Moment
- [x] Simulated Recruiter Panel Verdict and local session history
- [x] Tap-to-toggle microphone and Spacebar push-to-talk
- [x] Natural-pause handling and final transcript collection window
- [x] Server-side LLM proxy and fallback responses
- [x] TypeScript checks and production build passing
Next priorities
- [ ] Verify long spoken turns and complete transcripts in desktop
  Chrome
- [ ] Investigate AI request timeouts and improve fallback handoff
- [ ] Test preset/custom topics, Fishbowl, interruptions, and closing
  rounds
- [ ] Validate report quotes, evidence IDs, scoring, and computed
  metrics
- [ ] Complete responsive and keyboard-accessibility checks
Planned 16-hour testing schedule
  Time                                Focus
  Hours 0--4                          Test microphone controls, long
                                      turns, natural pauses, and
                                      interruption recovery
  Hours 4--8                          Investigate AI timeouts and improve
                                      latency and fallback behaviour
  Hours 8--12                         Run UPI, work-from-home,
                                      custom-topic, and Fishbowl
                                      sessions; validate reports
  Hours 12--16                        Check responsiveness and keyboard
                                      accessibility, fix issues, and
                                  publish a verified update
🔐 Privacy & Limitations
- GD Arena does not save microphone recordings.
- Browser speech-recognition processing follows the browser provider's
  own service and privacy terms.
- Transcript text is sent to the configured LLM service for live
  replies and report analysis.
- Speech-recognition quality and available voices vary by browser,
  microphone, and device.
- AI responses and scores may be imperfect. Use them as practice
  guidance, not as an authoritative evaluation or hiring decision.
- Preferences and session history are stored locally in the browser
  and are not synchronised across devices by the app.
🎯 Who Is It For?
GD Arena is designed for students and early-career job seekers preparing
for campus placements. It helps users practise:
- Speaking clearly and confidently
- Entering a discussion at the right moment
- Supporting ideas with reasons and examples
- Responding constructively to other participants
- Handling interruptions and discussion pressure
- Summarising and closing a discussion confidently
It is especially useful for learners who do not have a group available
for repeated practice or prefer a low-pressure environment to rehearse.
🧩 Libraries & Tools
React · TypeScript · Vite · Tailwind CSS · Node.js ·
Express 5 · Lucide React · concurrently · pnpm ·
Web Speech API · Platform-provided LLM API
::: {align="center"}
**🎙️ Practise your ideas. Improve your voice. Enter your next GD with
confidence.**

[Open GD Arena](https://gdarena-bzwhpycy.manus.space)
:::
