# Mobile development master checklist

The sections are modular: A = foundation, B = local storage, C = optional backend, D = optional cloud database, E = authentication/payments, F = quality/release. Do not initialize optional folders until needed.

| Step | Section | Task | CLI / setup quick reference | Run where | When |
|---|---|---|---|---|---|
| A1 | Foundation | Verify installed tools | node -v; npm -v; git --version; docker version; sbx --help | Windows host | Required |
| A2 | Foundation | Initialize one Git repository | git init; git branch -M main | Root | Required |
| A3 | Foundation | Generate Expo project | npx create-expo-app@latest frontend | Root | Required; frontend placeholder must be empty/removed first |
| A4 | Foundation | First commit | git add .; git commit -m "Initial mobile app" | Root | Required; inspect git status and ignore files first |
| A5 | Agent isolation | Set up Docker Sandboxes | Install/configure Docker Sandboxes per official docs; sbx --help | Windows host | Required for your agent isolation; verify current CLI syntax |
| A6 | Agent isolation | Launch isolated coding agent | sbx run --name mobile-dev claude | Root / host terminal | Optional agent selection; verify sandbox mounts and networking |
| A7 | Emulator | Install Android Studio, SDK and create AVD | Android Studio > Device Manager; adb devices | Windows host | Required for local Android emulation |
| A8 | Expo dev | Install development client | npx expo install expo-dev-client | frontend/ | Recommended |
| A9 | Expo dev | Configure EAS | npx eas-cli login; npx eas-cli init; npx eas-cli build:configure | frontend/ | Recommended; use an emulator APK build profile |
| A10 | Expo dev | Build emulator APK | npx eas-cli build -p android --profile development | frontend/ | EAS profile must specify android.buildType=apk; alternatively local run:android |
| A11 | Expo dev | Install APK and run Metro | adb install PATH_TO_APK; npx expo start --dev-client | Windows host for adb; frontend/ for Metro | Configure host-to-emulator networking |
| A12 | Design | Figma project / optional MCP | Create Figma project; configure MCP per agent docs | Browser + agent | Optional; no npm package required for Figma itself |
| B1 | Local storage | SQLite for offline structured data | npx expo install expo-sqlite | frontend/ | Optional; database file created on device |
| B2 | Local storage | Simple key-value preferences | npx expo install @react-native-async-storage/async-storage | frontend/ | Optional alternative to SQLite |
| C1 | Backend | Initialize Python project | uv init backend --no-vcs | Root | Optional; remove empty backend placeholder first, or cd backend && uv init --no-vcs |
| C2 | Backend | Install API dependencies | uv add fastapi "uvicorn[standard]" | backend/ | Optional |
| C3 | Backend | Start FastAPI | uv run uvicorn main:app --reload --host 0.0.0.0 | backend/ | Requires a FastAPI app variable named app in main.py |
| D1 | Cloud DB | Create hosted Supabase project | Supabase dashboard | Browser | Optional; independent of FastAPI |
| D2 | Cloud DB | Install client SDK | npm install @supabase/supabase-js; npx expo install react-native-url-polyfill expo-sqlite | frontend/ | Optional; use publishable key + RLS |
| D3 | Cloud DB | Initialize migrations/config | npx supabase init | Root | Optional; remove supabase/.gitkeep if CLI requires empty folder |
| D4 | Cloud DB | Start local Supabase stack | npx supabase start | Root on Windows host | Optional; Docker Desktop required; this is not the on-device SQLite database |
| D5 | Cloud DB | Database migration | npx supabase migration new initial_schema | Root | Optional; review RLS policies and schema |
| E1 | Auth | Supabase Auth | Configure Auth providers, redirect URLs and RLS | Supabase dashboard + frontend/ | Optional; login not required for all database uses |
| E2 | Payments | RevenueCat subscriptions / IAP | npx expo install react-native-purchases | frontend/ | Optional; verify current RevenueCat Expo instructions; development build needed |
| E3 | Payments | Stripe for eligible physical goods/services | Install Stripe React Native SDK per current docs | frontend/ + backend/ if needed | Optional; never embed Stripe secret key in app |
| F1 | Quality | Lint and type checking | npm run lint; npx tsc --noEmit | frontend/ | When scripts/config are present |
| F2 | Quality | Unit/integration tests | Install and configure Jest or other compatible test runner | frontend/ and/or backend/ | Optional |
| F3 | Quality | E2E automation | Configure Maestro or Detox | tests/e2e + host | Optional |
| F4 | Operations | Crash monitoring and analytics | Configure Sentry or similar provider | frontend/ + dashboard | Optional |
| F5 | CI/CD | GitHub Actions | Add workflow YAML in .github/workflows/ | Root | Optional |
| F6 | Release | Build production binaries | npx eas-cli build --platform all --profile production | frontend/ | Requires store credentials/configuration |
| F7 | Release | Submit to stores | npx eas-cli submit -p android; npx eas-cli submit -p ios | frontend/ | Requires developer accounts and review |
