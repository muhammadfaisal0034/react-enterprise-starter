# Architecture – React Enterprise Starter

## 1. Overview

This starter is designed for modern, secure, scalable, and high-performance React apps.
It follows best practices for code organization, API access, error handling, UI, testing, and localization.

---

## 2. High-level Structure

```
src/
  components/    # Shared UI primitives (Button, Toaster, etc.)
  constants/     # Global constants (API endpoints, config)
  hooks/         # Generic and module-specific hooks
  layouts/       # App-wide layouts (MainLayout, AuthLayout)
  modules/       # Feature modules (collocated components/types/constants)
  pages/         # Route-level pages (Dashboard, Login, Home, 404, Unauthorized)
  providers/     # App-wide providers (Auth, Toaster, Query, i18n, etc.)
  routes/        # Route definitions and guards (SecureRoute, configs)
  services/      # API clients (Axios instance, service modules)
  types/         # Shared/global types/interfaces
  utils/         # Utilities/helpers
  i18n/          # Localization setup and translations
  App.tsx
  main.tsx
  index.css
```

---

## 3. Layers & Patterns

- **Collocation:** Types/constants/utilities live in the feature folder unless shared across modules.
- **API Layer:** Centralized Axios instance (`services/api.ts`) with interceptors; data fetching/mutations use React Query via custom hooks.
- **RBAC:** Route-level guards using `SecureRoute` (checks user roles/permissions from context).
- **Authentication:** HTTP-only cookies; `/me` endpoint for user/role info; context manages session.
- **Error Handling:** Root-level class-based error boundaries; Suspense for async/loading.
- **UI Components:** Composable, accessible components via shadcn/ui (copied to `components/ui/`).
- **Testing:** Vitest + Testing Library for unit/integration; Playwright for E2E.
- **Localization:** react-i18next, with translations in `src/i18n/`.
- **Extensibility:** Analytics, logging, and state management libs can be added as needed.

---

## 4. Design Decisions

- **Minimal global state:** Prefer React Query/context/hooks over global stores unless complexity demands otherwise.
- **RBAC enforced at both route and backend API layers.**
- **Strict separation:** UI, data, and business logic are separated for maintainability and testability.
- **Tree-shakability:** Only components used are present in the bundle (shadcn/ui, custom hooks, etc.).

---

## 5. Testing

- **Unit/Integration:** Vitest (`.test.ts(x)`) colocated with code or in `__tests__` folders.
- **E2E:** Playwright scripts in `e2e/` or `tests/e2e`.
- **Scripts:**
  ```json
  {
    "test": "vitest run",
    "test:ui": "vitest --ui",
    "test:e2e": "playwright test"
  }
  ```

---

## 6. Localization

- **Setup:** See `src/i18n/` for i18next config and translation files per language.
- **Usage:** Wrap app in `I18nextProvider` in `main.tsx`. Use the `useTranslation` hook in components.
- **Best Practice:** Use keys/namespaces, organize files by language/module.

---

## 7. Extending the Architecture

- Add advanced state management only as needed (e.g., Zustand, Redux Toolkit).
- Integrate analytics/logging per project requirements.
- For highly specialized UI (e.g., data grids), integrate TanStack Table or other libs.

---

## 8. References

- [shadcn/ui Docs](https://ui.shadcn.com/docs)
- [React Query Docs](https://tanstack.com/query/latest)
- [React Router Docs](https://reactrouter.com/en/main)
- [Vitest Docs](https://vitest.dev/)
- [Testing Library Docs](https://testing-library.com/docs/react-testing-library/intro/)
- [Playwright Docs](https://playwright.dev/)
- [react-i18next Docs](https://react.i18next.com/)

---

This architecture provides a robust, extensible foundation for modern React enterprise applications.
