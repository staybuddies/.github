# StayBuddies

A student roommate platform with lifestyle matching, profiles, messaging,
and a student-card OCR companion service.

| Repository | Responsibility | Development branch |
| --- | --- | --- |
| [staybuddies-frontend](https://github.com/staybuddies/staybuddies-frontend/tree/new) | Vue 3 application | `new` |
| [staybuddies-backend](https://github.com/staybuddies/staybuddies-backend/tree/new) | Spring Boot APIs and administrator pages | `new` |
| [id_card_reader](https://github.com/staybuddies/id_card_reader/tree/new) | FastAPI / Tesseract student-card extraction | `new` |
| [.github](https://github.com/staybuddies/.github/tree/new) | Project overview and modernization plan | `new` |

All repositories were cloned with full history under
`/Users/zwenyanwin/Projects/Staybuddi`. Existing `main` and frontend `Su`
branches are preserved. Changes are developed on `new`, with no deployment or
default-branch change implied.

## Local preview

Run the backend using the disposable H2 command in its README, start OCR with
`uvicorn app:app --host 127.0.0.1 --port 8000`, and run `npm run dev` in the
frontend. Open <http://127.0.0.1:5173>. The database starts empty and resets when
the backend process stops. Persistent development needs PostgreSQL and the
backend's environment-based example configuration.

## First modernization pass

- Restrict administrator creation, user listings, and deletion.
- Separate signed administrator/student token roles and preserve revocation checks.
- Protect legacy admin writes with CSRF and replace destructive GET actions.
- Remove password hashes from API responses and fix invalid-login status codes.
- Replace the committed SMTP password with environment configuration. Its old
  value still needs revocation at the provider; history is preserved.
- Repair missing frontend dependencies, expired-session handling, direct SPA
  navigation, pagination, mobile header layout, and sign-in accessibility.
- Unify OCR entry points; preserve recognized IDs and confidence consistently;
  bound image inputs and reject malformed data with safe errors.
- Upgrade audited web dependencies, add regressions and CI, and document actual
  service behavior and setup requirements.

## Next engineering priorities

1. Audit remaining endpoint ownership checks, WebSocket subscriptions and
   public notification topics; add cross-user access tests.
2. Introduce PostgreSQL migrations, backup/restore checks, and real-database CI.
3. Review and upgrade the remaining Java dependency stack, including Spring Boot,
   AWS SDK v1, OpenAPI integration, and OCR libraries.
4. Add login/OTP throttling, expiration and replay tests, upload content validation,
   and a reviewed account-recovery flow.
5. Replace browser-persisted bearer tokens with a reviewed session strategy;
   evaluate cookie security and CSRF end to end before changing authentication.
6. Test full signup, email verification, matching, messaging and uploads against
   private test integrations. Add monitoring and structured, redacted logs.
7. Develop a consistent product design system across profiles, onboarding,
   matches, messaging and administration; expand keyboard/screen-reader coverage.
8. Validate OCR accuracy with consented institution data, add total inference
   deadlines/concurrency limits, and evaluate a real identity-verification flow.

The first pass is a tested foundation, not a claim that every repository is
production-ready. No cloud deployment or live customer data is needed for the
local preview.
