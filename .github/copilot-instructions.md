
# Copilot Instructions for LocalAGI

## Project Overview
LocalAGI is a modular, agent-based platform for orchestrating LLMs, custom actions, and connectors. It is designed for extensibility, local-first operation, and integration with external services (Slack, Twitter, GitHub, LocalAI, etc.).

**Languages:**
- Backend: Go (main logic, agent orchestration)
- Frontend: React (Vite-based, in `webui/react-ui`)

## Architecture & Key Components
- **core/**: Agent logic, action definitions, state management, conversation tracking. Entry for new agent behaviors and custom actions.
- **services/**: Integrations and service connectors (GitHub, Twitter, image generation, etc.). Each subfolder/file implements a service or action.
- **pkg/**: Shared libraries for clients, LLMs, RAG, utilities, vector stores.
- **webui/**: Go web server and React UI (`webui/react-ui`).
- **example/**: Example custom actions for extension.

## Developer Workflows
- **Build:** Use `make` or VS Code build task (`msbuild`). For Docker: `docker compose up` (see `README.md`).
- **Test:** Go tests are colocated with code (`*_test.go`). Run all tests: `go test ./...` from repo root.
- **Run:** Main entry is `main.go`. Configure via environment variables (see `README.md`).
- **Web UI:** Develop React UI in `webui/react-ui` (uses Vite, see its `README.md`).

## Project Conventions
- **Actions:** Add new agent actions in `core/action/` or `services/actions/`. Use the `ActionDefinition` pattern. Example: `example/custom_actions/hello.go`.
- **Connectors:** Integrate new services in `services/connectors/`. Example: `services/connectors/twitter.go`.
- **State:** Shared agent state managed in `core/agent/state.go` and `core/state/`.
- **Configuration:** Use environment variables for runtime config. See `main.go` and `README.md` for options.
- **Testing:** Place tests alongside code. Use Go's standard testing tools.
- **React UI:** Use ESLint config in `webui/react-ui/eslint.config.js`.

## Integration Patterns
- **External APIs:** Use Go clients (e.g., `github.com/google/go-github`, Twitter API) in `services/`.
- **LLM/RAG:** Integrate LLMs via `pkg/llm/`, RAG via `pkg/localrag/`.
- **Observability:** Agent state/events observable (see `core/agent/observer.go`).

## Examples
- **Add a new action:** Copy `example/custom_actions/hello.go`, register in `core/action/`.
- **Add a connector:** See `services/connectors/twitter.go` for pattern.

## References
- [README.md](../README.md): Quickstart, environment variables, architecture summary
- [core/](../core/): Agent/action logic
- [services/](../services/): Integrations and actions
- [webui/react-ui/README.md](../webui/react-ui/README.md): React UI setup

---
For more, see code comments and referenced files. When in doubt, follow existing patterns and colocate related tests.
