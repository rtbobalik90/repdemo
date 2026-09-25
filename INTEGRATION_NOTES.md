# Connect V818 — Crown Bot integration

The complete V817 demo is retained. The V817 resizable three-column calendar
script is unchanged. All original style blocks remain unchanged; mascot-only
styles and controls are added inside the existing isolated CROWN component.
The supplied WebP and PNG assets are copied byte for byte. No replacement
artwork, body alterations, extra chest logos, or background rectangles were made.

## Event mapping

| Existing state or event | Crown Bot pose / behavior |
| --- | --- |
| Default | Neutral / Ready |
| Existing welcome notice | Friendly Wave |
| Explanations, FAQ responses | Pointing Up |
| Guided resource control | Pointing Left / Right / Up according to target position |
| Open chat awaiting a question | Thinking poster |
| Next Best Action / desktop | Idea / Recommendation |
| Chat processing, project answers, meeting document jobs | Working / Analyzing while active |
| Workspace search input | Search / Investigating during search input |
| General committed demo updates | Attention |
| Open loyalty blocker or urgent overdue/error work item | Urgent Attention; poster remains while issue is open |
| Incoming demo call / call workspace | Phone / Call Now |
| Follow-up work item / saved call reminder | Follow-Up |
| Email workspace / draft / email-related answer | Email / Message |
| Successful task, call, demo email, or document completion | Success / Completed |
| Daily call target crossed through actual saved activity; lesson completed | Celebration |
| Required-field validation or missing-information work item | Warning / Concerned |
| Reported action, AI, recording, or document failure | Error / Stop |
| Existing short-deadline work item / saved customer event | Clock / Time Sensitive |
| Existing loyalty work item | Priority / VIP |
| Quote / revenue-opportunity context | Money / Opportunity |
| Orders, saved draft order, production | Order / Package |
| Artwork work item | Artwork, with urgent/loyalty priority when applicable |
| Learning Center, lesson and help | Learning / Help |
| Existing quiet/snooze mode | Quiet / Sleeping poster |
| Unread message-board posts | One reaction per post; persistent board badge until opened |
| Meeting recording / transcription | Working / Analyzing |
| Meeting paused | Thinking poster |
| Meeting ended | Success / Completed |
| 35–60 seconds of inactivity, then 90–150 second gaps | All ten funny idle actions, shuffled without immediate repeats |

Pose priority comes from the loaded record and real interface state. Task
completion and goal reactions use the existing saved demo activity. The mascot
does not create tasks, orders, sales, messages, milestones, or recording sessions.

## Controller and controls

- `window.CrownMotion` is the single animation owner. It reads the embedded copy
  of the supplied animations.json so local file opening does not require a JSON
  fetch. Original manifest filenames and durations determine playback.
- Source-level hooks report UI state, task commits, validation, meeting status,
  document jobs, lesson completion, and demo email results. Navigation and open
  call/task state are checked by one lightweight scheduler.
- Urgent/error reactions preempt lower-priority behavior. Processing holds its
  state until it ends. Short reactions play for the supplied duration after the
  image loads; persistent alerts return to a poster rather than looping forever.
- Only the current image is displayed. Other assets load on demand. Stale image
  callbacks cannot replace a newer state. WebP failures fall back to the supplied
  matching poster, then the neutral poster, then an embedded exact neutral PNG.
- Reduced motion, Pause, hidden tabs, and a hidden mascot use posters. Idle is
  suppressed during typing, chat/settings/notices, modals, alerts and processing.
- The complete square canvas uses object-fit: contain. Mobile width at or below
  600px caps the mascot at 112px. Existing keyboard activation, drag positioning,
  left/right docking, accessible labels and chat behavior are retained.
- Board notification IDs are remembered across reloads. The unread badge opens
  the existing Message Board; it does not mark posts read on its own. Opening
  each post uses the board's original read behavior.
- Testing controls live in the existing CROWN controls area. Board preview is
  explicitly a preview and does not add a business post or alter read receipts.
- Sound starts OFF each page session. The separately saved original three-second
  bubble WAV was recovered and included; the attached ZIP did not contain it.
  Enabling the toggle preloads this one audio source. Bubble playback starts it
  alongside the loaded WebP after user opt-in. No other poses receive sound and
  no WebM or MP4 audio player is used. Browser rejection is handled. Disabling
  sound, changing poses, pausing, reduced motion, and hidden tabs stop audio.

## Boundaries and optional assets

This HTML is the supplied **Alex Morgan standalone demo**. No other rep workspace
was created or modified. The message board is an existing local snapshot, not a
live server subscription. Its loaded unread posts are integrated; the tester can
preview a new-post reaction without creating a fictional business update.

There is no new automatic after-hours schedule because this demo's business
records use a fixed scenario date. Quiet mode is the reliable existing signal.
No live telephony, inbox feed, CRM stream, or external milestone source was added.

There are no required missing mascot assets after recovering the bubble WAV.
A dedicated **Listening / Transcribing** pose is optional; the existing Working /
Analyzing artwork is a usable substitute. Recording pause, errors, and processing
already have suitable supplied poses.

## Verification performed

- All 267 inline script blocks compile.
- 18 deterministic controller suites pass, including all 36 mappings, priorities,
  delayed image loads, fallback, one-shot timing, unread deduplication, all ten
  idle actions, suppression, pause, reduced motion, meeting states, and milestones.
- The WAV decodes as three-second, 48 kHz mono PCM audio. Single-source opt-in
  playback, default silence, pause and reduced-motion suppression pass controller
  simulation. Actual audible playback remains part of the browser check below.
- Original demo service loaded with 24 tasks and 52 accounts. Validation failure,
  actual completion, duplicate-completion prevention, and undo retained their
  original outcomes and emitted the expected new mascot hooks.
- 96 desktop/mobile/landscape geometry cases keep the full square mascot and
  chat bubble within the viewport.
- All 2,460 animation frames decode with transparency, full 640×640 dimensions,
  and timing matching the supplier manifest. All 72 copied images match the
  supplied bytes. CSS uses no opaque mascot background in either theme.

**Not completed:** live browser rendering, device visual inspection, audible
playback, pointer collision checks against every screen, and microphone permission/audio
capture. The browser preview service blocked the local preview. The checks above
are asset, source, geometry, and JavaScript simulation checks, not a claim of a
completed end-to-end browser session.
