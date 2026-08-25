---
name: local-dev-runner
description: "Start or run a local development environment, frontend, backend, or development servers with minimal discovery and ownership-safe lifecycle management."
license: MIT
---

# Run local development services

## When to use

Use when asked to start requested local frontend, backend, or other development services. Prevent broad project exploration, undocumented command guesses, and unsafe process cleanup.

## Requirements and boundaries

- Requires the capability to execute local project commands, manage child processes, inspect local port ownership, and perform local readiness checks.
- Starting services creates child processes and may bind local ports. Readiness probes may make local network connections. Documented environment variables, credentials, network access, or other prerequisites may be required; obtain or report them without exposing secret values.
- Use only repository-documented run commands. Do not install or update dependencies, modify configuration, run migrations, or start extra infrastructure unless it is documented as required and authorized. Report missing prerequisites instead of broadening scope.
- Never run a long-lived server through the agent's foreground terminal or tool channel. The launcher must detach the service from agent standard input, output, and error, return immediately after process creation, and leave no stream or child handle that keeps the agent call open.
- Do not open visible terminal windows by default. Use one managed environment session with captured, service-labeled logs. When a visible terminal is necessary, open at most one window for the environment, render the full operational report there, and keep the agent's conversational reply minimal. Use additional windows only after explaining a technical limitation and receiving explicit approval.

## Workflow

1. Discover only what is needed, in this order: local instructions; concise run sections in README or docs; root or workspace task manifests and service manifests. Open these known files directly instead of starting with broad or semantic source search. Stop searching once the commands, exact working directories, and required environment are known. Do not inspect unrelated source, architecture, dependencies, or history.
2. Prefer one aggregate entry point documented by the project when it covers the requested services. If it also starts unrequested services or meaningful side effects, list them and obtain approval before launch. Do not invent an aggregate command or install a process manager.
3. When no suitable aggregate entry point exists, place the requested commands in one runtime-managed environment session with separate child-process ownership and service-labeled logs. Do not create one terminal window per service. If the runtime cannot safely group them, report the limitation before proposing additional windows.
4. Start only the requested and approved services. Before launch, identify already-running relevant services and the owners of relevant ports. Never stop, restart, or claim ownership of a pre-existing or unknown process; report conflicts clearly.
5. Before launch, establish one environment-session identity, child-process ownership, a cleanup path, a readiness deadline, and the persistence mode from the user's explicit wording. A request to start or launch an environment means keep successful services running. Treat a run as temporary only when the user explicitly asks to close it after verification or use.
6. Launch the environment through a runtime-native detached session or supervisor in the documented working directories. Redirect logs to storage independent from the agent channel. If the runtime cannot detach the session and return from the launch operation immediately, report that limitation and do not start the environment through a foreground fallback.
7. The launch operation performs no sleeps, readiness loops, HTTP probes, or live-log reads. Return `starting` as soon as the session and process identities are known, including any URL or port available without waiting; never keep the current agent turn open to obtain readiness.
8. For a visible-terminal fallback, print a session header in that terminal before service output and keep all detailed status there: session identity, grouped commands, approved extra services, working directories, process identities, URL roles, URLs or ports, readiness state, logs, and shutdown guidance.
9. Check readiness only through an independently running monitor that delivers completion without blocking the agent, or through a separate bounded status operation when the user requests it or later work needs the service. An independent monitor uses the repository-documented deadline or 60 seconds when none exists, never extends it silently, and stops an unusable owned startup tree on timeout.
10. Probe an endpoint that proves each service's intended role; a listening port or arbitrary HTTP response alone does not prove a usable application. Never assume conventional ports. Classify discovered URLs as user-facing application, API, asset or hot-reload server, or internal service. Do not present an asset server as the frontend application merely because it is listening; report its role and readiness separately.

## Lifecycle and cleanup

- Keep every successfully launched service running unless the user explicitly requested a temporary run or explicitly asks to stop it. Do not reinterpret a launch request as a readiness-only test, and do not stop services merely because the current task or response is ending.
- Report active services and how the user can request their shutdown during the current interaction. Do not promise future cleanup after the interaction ends.
- Before readiness, clean up failed, timed-out, cancelled, or otherwise unusable owned startup processes. This failure handling does not authorize stopping services that already reached readiness.
- Prepare the exact cleanup operation before spawning services. Invoke it for a ready service only after an explicit temporary-run or shutdown instruction.
- Clean up by attempting graceful termination of the owned process group first. Escalate only when necessary and only for the same owned process. Verify process exit and release of ports attributable to those processes. Never use broad name-based termination.

## Expected report

When no terminal is visible, report the environment-session identity, aggregate entry point or grouped commands, approved additional services, launch mode, terminal visibility, and whether the session remains running. For each service, report its working directory, status (`starting`, `ready`, or `failed`), URL role, actual or pending URL or port, child-process identity, readiness deadline, and monitoring mode. Also report failures or missing prerequisites, timeout diagnostics, and cleanup.

When a visible terminal carries the operational report, keep the conversational response to one short instruction: say the environment is `starting` and ask the user to review the terminal, or say it is `ready` only after readiness evidence exists and ask the user to review the terminal. Never claim `ready` merely because the terminal or process was created.
