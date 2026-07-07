## v0.1 Initial Prototype

### Summary

First rough prototype of Division 1 OS / OZ Theory app.

### Notes

* Initial screen and world-model experiment
* Gateway / Channel / Report / Archive concept exploration
* Stitch-based visual flow testing
* Not stable enough for real use
* Served as the foundation for v0.2 routing stabilization

---

## v0.2 Routing Stabilization

### Fixed
- App entry now starts from Gateway / Morning Briefing
- Gateway CONNECT routes to Secure Channel
- Secure Channel is treated as main home after check-in
- Bottom navigation restored: Channel / Missions / Archive
- Missions restored as secondary tab, not app root
- Mission status dropdown restored
- Mission text readability improved
- Archive → Archived Report Detail route repaired

### Remaining
- UI copy consistency: Korean / English mixed labels
- Akane dialogue quality
- Final report generation logic
- Mission generation from conversation
- AI response tone and world-model alignment

### Next
- Move to AI Studio
- Build Akane system prompt
- Test Channel conversation response
- Define report output schema

---

## v0.2.1 Flow Complete / First Deployment

### Completed

* Moved from Stitch routing prototype to AI Studio build
* Deployed Division 1 OS to Cloud Run
* Gemini API key and server-side connection configured
* Gateway / Morning Briefing works as app entry
* Gateway CONNECT generates briefing and routes to Secure Channel
* Secure Channel works as main home after check-in
* Akane persona and Division 1 world-model partially restored
* Mission Archive generates missions from daily input
* Mission status dropdown now updates visible card state
* Mission statuses are reflected in Final Case Report
* Final Case Report generation works
* Save to Archive works
* Archive list persists across sessions
* Archived Report Detail opens correctly
* Mobile readability verified and better than desktop preview
* The v0.2 Flow Complete application source code has been exported and archived in a separate private repository.

### Confirmed Flow

Gateway → Secure Channel → Mission Archive → Final Case Report → Archive → Archived Report Detail

### Observations

* The mobile app experience is stronger than the desktop/web preview
* The core loop is now functional:
  Daily input → Akane interpretation → Missions → Status updates → Final Report → Archive
* Archive is becoming the long-term memory layer of the system
* Missions and chat behave like daily session/cache data
* Akane persona works at a basic level, but dialogue richness still requires more testing
* Current fixed report categories feel too rigid for actual daily records

### Issues Found

* Active day session can be lost after browser refresh or cache reset
* When the active session is lost, the app returns to Gateway and today’s chat/missions disappear
* Archive persists, but unarchived daily session data is not yet protected
* Final report format needs to shift from fixed four-category assessment to dynamic case-entry generation
* Akane should identify the day’s key events/keywords from missions and chat, then write flexible case records

### Next

* Implement Active Session Persistence
* Add Session Restore button on Gateway
* Add explicit End Session / 공안국 접속 종료 action
* Preserve today’s chat, missions, mission statuses, and current screen until explicit session close or report archive
* Revise Final Case Report schema from fixed categories to dynamic case entries
* Continue refining Akane persona through real use

### Notes
- Public repository keeps concept notes, progress logs, and screenshots.
- The v0.2 Flow Complete application source code has been exported and archived in a separate private repository.


---

## v0.3 Stable Checkpoint — Active Session Persistence / Mission Context

### Goal

Preserve the current day’s active operation session and allow Akane to access the current mission context during Secure Channel conversations.

### Completed

- Save active session to localStorage
- Restore unfinished session after refresh or browser reload
- Preserve:
  - Gateway input
  - generated briefing
  - chat history
  - missions
  - mission statuses
  - current screen
- Show `이전 작전 세션 복구` button on Gateway when a recoverable session exists
- Add explicit `공안국 접속 종료` action
- Clear active session only after successful Archive save or explicit End Session
- Keep Archive data separate from the active session cache
- Inject current mission data into Secure Channel conversations
- Fix duplicate message transmission
- Add an in-flight send guard to prevent overlapping Send / Enter requests

### Known Issues

- Secure Channel does not always auto-scroll to the latest message after returning from Missions or Archive.
- Mission drafting from conversation was tested but intentionally excluded from this stable checkpoint.
- Final Case Report still uses the fixed-category format and should later transition to dynamic case entries.

### Notes

This checkpoint represents the last stable version before the Secure Channel auto-scroll and mission drafting experiments.

### Design Principle

Archive is the long-term case record.
Active Session is the current day’s operation cache.
The current operation must not disappear unless the user explicitly ends it.
