## Agent Notes

- Use the provided scripts and package manager (SwiftPM); avoid adding dependencies or tooling without confirmation.
- Validate behavior against the freshly built bundle; restart via the pkill+open command above to avoid running stale binaries.
- To guarantee the right bundle is running after a rebuild, use: `pkill -x CodexBar || pkill -f CodexBar.app || true; cd /Users/steipete/Projects/codexbar && open -n /Users/steipete/Projects/codexbar/CodexBar.app`.
- After any code change that affects the app, always rebuild with `Scripts/package_app.sh` and restart the app using the command above before validating behavior.
- If you edited code, run `scripts/compile_and_run.sh` before handoff; it kills old instances, builds, tests, packages, relaunches, and verifies the app stays running.
- Per user request: after every edit (code or docs), rebuild and restart using `./Scripts/compile_and_run.sh` so the running app reflects the latest changes.
- Release script: keep it in the foreground; do not background it—wait until it finishes.
- Release keys: find in `~/.profile` if missing (Sparkle + App Store Connect).
- Prefer modern SwiftUI/Observation macros: use `@Observable` models with `@State` ownership and `@Bindable` in views; avoid `ObservableObject`, `@ObservedObject`, and `@StateObject`.
- Favor modern macOS 15+ APIs over legacy/deprecated counterparts when refactoring (Observation, new display link APIs, updated menu item styling, etc.).
- Keep provider data siloed: when rendering usage or account info for a provider (Claude vs Codex), never display identity/plan fields sourced from a different provider.\*\*\*
- Claude CLI status line is custom + user-configurable; never rely on it for usage parsing.
- Cookie imports: default Chrome-only when possible to avoid other browser prompts; override via browser list when needed.
