## Project Roadmap & Backlog

This roadmap summarises the current state of the app, highlights unfinished areas (TODOs/TMP mocks), and proposes the next development steps to deliver a polished experience for school / university tournaments.

---

### Current Status (2025-11)

**Implemented**
- Authentication mock (no real auth yet) for joining/creating events.
- Event lifecycle:
  - Simple + advanced event creation.
  - Join event via link / public list.
  - Lobby view with participants and quick actions.
  - “Active games” dashboard.
- Tournament features (single elimination / round robin scaffolding).
- Team management & active match display (mock data in several places).
- Institution & class entities + UI to browse institutions and classes.
- Seed script that creates demo events on first launch.
- Light & dark theme with custom palettes (dark default).
- App-wide localization infrastructure (RU/EN) – wording still needs completeness.
- Security: placeholder PIN-code management in settings (UI & storage).

**Known placeholders / TODOs in code**
- Auth: everywhere we use `Uuid().v4()` or hardcoded IDs (event creation, tournament actions).
- Tournament operations: `_startTournament`, score update flows, bracket creation uses TODOs + mock team IDs.
- Teams/class navigation: TODO to navigate into detailed team page.
- Active games refresh logic (marked as TODO).
- Notification toggles removed; push/Email notifications absent.
- QR share: links generated, but no in-app scanner for joining via QR.
- Build configs: applicationId/signing TODOs in Android gradle files (expected).
- Windows test app TODOs (can ignore for mobile milestone).

---

### Product Vision Recap

1. **Fast event creation for schools / universities** – minimal friction for an admin to set up an event and invite participants.
2. **Roles** – Admin (score update), Participant, Spectator are sufficient.
3. **Discoverability** – easy to find active, upcoming, and past events.
4. **Secure access where needed** – optional PIN lock, maybe later SSO.
5. **Invite flows** – QR + links must work seamlessly.

---

### Immediate Priorities (Next Sprint)

1. ✅ **Authentication backbone**
   - Integrate Firebase Auth (email+password or anonymous with upgrade) so `createdBy`, `startedBy`, etc. use real user IDs.
   - Provide current user context across notifiers.

2. ✅ **Event states & filtering**
   - Extend event model to store `startDate`, `endDate`, `status`.
   - Implement views for:
     - Active events (already partially done).
     - Upcoming (startDate in future).
     - Past events (finished or endDate < now).
   - Add filtering tabs or a segmented control on home or dedicated screen.

3. ✅ **QR invitation flow**
   - Integrate a QR scanner (e.g., `mobile_scanner` or `qr_code_scanner`) on the join screen.
   - Deep link / universal link handling for invites.
   - Ensure generated QR includes event ID (already via `EventLinkUtils`) and scanner resolves it.

4. ✅ **Institutional data UX**
   - Allow admin to link events to an institution / class during creation.
   - Show institution-filtered event lists (cross institution page now only list events; allow auto filter by selected institution).

5. ✅ **Remove mock placeholders**
   - Replace `['team-1', 'team-2']` in bracket creation with actual teams.
   - Replace hard-coded admin IDs in tournament actions with logged-in user ID.
   - Implement navigation for `_navigateToTeamDetails`.
   - Implement refresh logic in `ActiveGamesPage`.

---

### High Priority Enhancements

1. **Participant experience**
   - Allow quick join by scanning QR → prefill event + prompt for name.
   - Allow participants to see upcoming matches, results (read-only view).

2. **Admin tools**
   - Score entry UI: nice two-team scoreboard with per-set/per-match logging.
   - “Start tournament” should validate requirements (teams, participants) before launching bracket.
   - Event analytics: participants count, match counts, winners, etc.

3. **Team management**
   - Create dedicated team detail page (roster, stats, add/remove members).
   - Assign team captains (optional).

4. **Notifications (future)**
   - Push notifications for match start / updates (FCM topics per event).
   - Email / in-app notifications using a notification center UI.

5. **Offline & caching**
   - Cache event data for quick load.
   - Background sync to refresh active games.

---

### UI / UX Improvements

- **Dashboard revamp**: home screen should surface “Active now”, “Upcoming”, “Recently finished” cards.
- **Event creation wizard**: multi-step (Basic info → Teams → Schedule → Confirmation).
- **PIN code UX**:
  - Confirm PIN with inline numeric keypad (use `PinCodeTextField`-style UI).
  - Auto-lock app after inactivity (optional in settings).
- **Accessibility**: large fonts, high contrast, screen reader labels.
- **Localization**: finish translating remaining hard-coded strings (many still in Russian in UI code).

---

### Technical Debt / Housekeeping

1. **Refactor mock auth**:
   - Move all `Uuid().v4()` to auth service once real auth is added.
2. **Repository cleanup**:
   - Normalize `settings` field across entity/model (currently dynamic map vs. EventSettings).
3. **State management**:
   - Use `AsyncNotifier` for flows that load data (institutions, events, active games) to better control refreshing and error states.
4. **Testing**:
   - Unit tests for repositories (Firebase integration via emulator).
   - Widget tests for create/join flows.
   - Integration test covering QR join.
5. **CI / CD**:
   - Add GitHub actions pipeline (formatting, `flutter analyze`, tests, `build_runner`).

---

### Suggested Development Order

1. **Auth integration + user context** – everything else becomes easier when we have real user IDs.
2. **Event statuses & filtering** – improves UX, minimal dependencies.
3. **QR scanning + invite flow polish** – critical for quick joining.
4. **Remove mock data / hard-coded IDs** – ensures production readiness.
5. **Tournament operations** – bracket creation, score entry, tournament start logic.
6. **Admin dashboards & analytics** – value-add once core flow stable.
7. **Notifications & offline support** – advanced features after MVP solidified.

---

### Backlog Ideas (Nice-to-have / Future)

- **Leaderboard & rankings** for classes / faculties.
- **Certificates / badges** for participants (shareable).
- **Photo gallery** integration for event highlights.
- **Live commentary / streaming links** support.
- **Parent/teacher approval workflow** for minors.
- **Role-based dashboards** (admin vs. participant views).
- **Multi-language admin console** (English, Russian, +others).

---

Keep this roadmap under version control and update per sprint. Use it alongside in-code TODOs to track progress. For each item, create GitHub issues / project tasks with acceptance criteria and owners.




