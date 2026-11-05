# AI Screen Recording to SOP & Automation Spec Generator (Gemini + n8n)

Drop a screen recording of someone doing a task into a Google Drive folder. Gemini watches the screen and listens to the audio, then returns a strict JSON step log: every step, app, field and decision. A second Gemini pass turns that log into an n8n build prompt, a tool-agnostic automation spec and a list of open questions. The result is saved as a Google Doc and the link is sent to Telegram.

## How it is built (27 nodes)

1. **Intake and guard rails:** a Google Drive trigger watches the folder; an n8n Data Table run log makes sure each file is processed once; non-video files are rejected with a message; an audio-only path keeps cost down when the screen is not needed.
2. **Two AI passes, kept separate:** the first pass only describes what happened (structured JSON); the second only writes the spec from that description, so the analysis and the design never mix.
3. **Deliver and record:** a Google Doc with the step log, build prompt, spec and open questions; the link goes to Telegram; the run is recorded in the Data Table.
4. **Failures are visible:** the error outputs of every costly step record the failure and alert the owner instead of failing silently.

## Setup

Import `screen-recording-to-sop.json`, then create Google Drive, Google Docs, Gemini and Telegram credentials and replace the placeholders: `REPLACE_WITH_YOUR_DRIVE_FOLDER_ID`, `REPLACE_WITH_YOUR_DRIVE_ID`, `REPLACE_WITH_YOUR_DATA_TABLE_ID`, `REPLACE_WITH_YOUR_TELEGRAM_CHAT_ID` and the credential ids.

Built as a portfolio workflow; no client data is included.
