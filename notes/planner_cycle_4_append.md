Planner Cycle 4: Repo, Shared Code, Packaging & Sync

- Repository layout: Single repository with top-level subfolders: `pi/`, `windows/`, and a shared package `alpha_common/` for protocol definitions, models, and logging utilities.
- Shared code: `alpha_common` will contain unified protocol definitions, message models, and logging helpers. Laptop-specific modules may extend and provide additional capabilities.
- Packaging/dependencies: Use a simple `requirements.txt` and `pip` for both Pi and Windows; no virtual environments by preference.
- Logging: Extensive local logging on the Pi (raw CAN/OBD frames, decoded messages, user actions, errors). Logs are queued on the Pi until sync.
- Sync policy: Pi pushes queued logs when the laptop becomes reachable. The laptop runs a lightweight HTTP(S) receiver endpoint (e.g., `POST /api/sync/logs`) to accept pushes. Use a simple token header (e.g., `X-Auth-Token`) for authentication in prototype; fallback to SCP/SSH if needed.
- Notes: Laptop will provide richer tooling and may run analysis/AI tasks; shared package ensures consistency across platforms.
