# Agent instructions
- This is a modular Expo/React Native monorepo. `frontend/` is the mobile app; `backend/` is optional Python/FastAPI; `supabase/` is optional database configuration.
- Do not initialize optional modules without approval.
- Prefer TypeScript and Expo-supported packages.
- Do not read or expose secrets, execute destructive commands, publish, or deploy without explicit approval.
- Never mount the host Docker socket or broad home directories into agent isolation.
- Run appropriate lint, tests, and type checking for modified code.
- Confirm working directory before npm/npx/uv commands.
