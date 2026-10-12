# Modular Expo Mobile App Master Template

This repository is a **folder skeleton**, not an initialized application. Optional services are intentionally inactive.

## Start here
1. Review [SETUP_CHECKLIST.md](SETUP_CHECKLIST.md).
2. From this root run `git init` and `git branch -M main` if not already a Git repository.
3. Remove the `frontend/.gitkeep` placeholder (and its otherwise-empty folder if create-expo-app rejects it), then run `npx create-expo-app@latest frontend` from the root.
4. Run Expo/npm/EAS commands **inside `frontend/`**.
5. Set up Docker Sandboxes for your agent; use the official CLI documentation to confirm installation and supported commands. Do not confuse Docker Sandbox with Dev Containers.
6. Install Android Studio and create an emulator on Windows. Use an Android development APK for emulator testing. iOS Simulator requires macOS; EAS builds iOS binaries but does not host a simulator.
7. Initialize optional modules only when needed.

## Scenarios
- **Basic:** `frontend/` only; optionally `expo-sqlite` or AsyncStorage.
- **Backend without cloud DB:** `frontend/` + `backend/` initialized with `uv init --no-vcs`.
- **Cloud DB without custom backend:** `frontend/` + Supabase SDK; optional `supabase/` migrations/config.
- **Full stack:** frontend + backend + Supabase.
- **Payments:** RevenueCat for in-app digital purchases/subscriptions; Stripe for eligible physical goods/services and applicable cases.

## Paths and responsibilities
- `frontend/`: React Native, Expo, TypeScript, EAS; npm and npx commands here after creation.
- `backend/`: optional FastAPI, uv, Python.
- `supabase/`: optional database migrations, local development config.
- `payments/`: design notes and integration docs only, **not a separate payment service by default**.
- `design/figma/`: exported assets and design notes; Figma source may stay in Figma cloud.
- `monitoring/`, `tests/`, `.github/workflows/`, `infra/`: optional supporting infrastructure.

## Security and connectivity
- Sandbox agents can still edit shared project files. Commit changes before granting access.
- Avoid mounting Docker socket, credentials, or entire home directories into the sandbox.
- `10.0.2.2` is the Android emulator address for the Windows host; other container/sandbox connections require explicit networking.
- Supabase publishable keys may be shipped with the app if RLS is configured; secret/service-role keys must not be.
- Never commit `.env` secrets.

## Useful official references
- https://docs.expo.dev/
- https://docs.expo.dev/develop/development-builds/introduction/
- https://docs.docker.com/ai/sandboxes/
- https://supabase.com/docs/guides/local-development
- https://www.revenuecat.com/docs/
