## 1. Queue and capture

- [ ] 1.1 Implement per-user IndexedDB queue in lib/offline with stable IDs and ordered entries; verify refresh persistence and account isolation.
- [ ] 1.2 Add Driver OfflineIndicator, toggle, pending count and queued status/location controls; connect photo-upload availability to the simulated offline state; verify offline actions do not update server views and photo upload is unavailable while the toggle is Offline.

## 2. Replay and recovery

- [ ] 2.1 Implement single-worker automatic reconnect sync and manual Retry using existing command deduplication; verify capture order and lost-acknowledgement retries.
- [ ] 2.2 Handle expired sessions, stale versions, changed permissions and explicit stale-item discard; verify unresolved updates remain visible without overwriting server progress.
- [ ] 2.3 Keep route delay visible through checkpoint replay and reject delivery while closed; verify retry can succeed after reopening when progress is still valid.
- [ ] 2.4 Run offline-updates scenarios in separate role sessions, including interruption mid-sync; record results and AI corrections.
