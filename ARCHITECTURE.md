# Architecture – React Enterprise Starter

## 1. Overview

This starter is built to enable modern, secure, scalable, and high-performance React applications in any enterprise context.  
It follows industry best practices for code organization, API access, error handling, UI, testing, localization, and maintainability.

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
.env              # Environment variables (never committed)
.env.example      # Example env file for reference
.editorconfig     # EditorConfig file for code consistency
.eslintrc         # ESLint config for code quality
.prettierrc       # Prettier config for formatting
```

---

## 3. Essential Architecture Layers & Design Patterns

### a. **Collocation**
- Types/constants/utilities live in their feature folder unless reused across modules.
- Promote to shared folders only if reused.

### b. **API Layer**
- **Centralized Axios instance** (`services/api.ts`) with interceptors for:
  - attaching credentials (cookies)
  - global error handling (see Error Handling)
  - logging (in dev)
- **React Query** handles all data fetching/mutations for caching, retries, and performance via custom hooks.

### c. **Authentication & RBAC**
- **Authentication:** HTTP-only cookies, never use localStorage/sessionStorage for tokens.
- **User/role info** is loaded from a `/me` endpoint and stored in context.
- **RBAC:** Route-level guards using `SecureRoute` that check user roles and redirect unauthorized users to `/unauthorized`.

### d. **Error Handling**
- **Error Boundary:** Implemented at the application root as a class component, per React 19.1+ standards. It catches rendering errors in the component tree, logs them (dev: `console.error`, prod: pluggable for Sentry/Datadog), and displays a user-friendly fallback UI.
- **API Error Handling:** Axios interceptors globally catch and handle API errors. Use React Query’s `onError` handlers in hooks/components to show user-facing notifications (e.g., via Toaster).
- **Consistent error surfaces:** Always show errors in the UI using toast notifications or error components, never silent failures.
- **Logging:** All caught errors in production should be reported to an error monitoring tool.

### e. **UI Components**
- **shadcn/ui:** For all UI primitives, copied into `components/ui/` for full control and easy customization.
- **Toaster:** Use shadcn/ui’s Toaster for app notifications.
- **Accessibility:** All UI components must be accessible by default (Radix/shadcn/ui ensures this).

### f. **Testing**
- **Unit/Integration:** [Vitest](https://vitest.dev/) + [@testing-library/react](https://testing-library.com/docs/react-testing-library/intro/)
- **E2E:** [Playwright](https://playwright.dev/)
- Tests are colocated with code or in `__tests__` folders for discoverability.

### g. **Localization (i18n)**
- **Library:** [react-i18next](https://react.i18next.com/)
- **Structure:** `src/i18n/` for all translation files and configuration.
- **Usage:** App is wrapped in `I18nextProvider`; use the `useTranslation` hook in components.
- **Best Practice:** Use keys/namespaces, organize files by language/module. Always provide a fallback language.

### h. **Environment Management**
- **.env.example**: Documents all required environment variables.
- **.env**: Used for local development, never committed.
- **Vite** automatically injects env vars prefixed with `VITE_` into the client app.

### i. **Consistent Code Quality**
- **ESLint**: Enforces JavaScript/TypeScript standards and code smells.
- **Prettier**: Enforces consistent formatting.
- **EditorConfig**: Ensures consistent editor settings across IDEs.
- **Stylelint** (optional): For CSS/Tailwind best practices.
- **Pre-commit hooks**: Use Husky + lint-staged to enforce linting/formatting before code is committed.

### j. **Dependency Management**
- **Dependabot/Renovate**: Automated dependency update PRs.
- **Security scanning**: Enable npm audit and GitHub’s built-in security alerts.

---

## 4. Error Handling – In Detail

- **Application-level errors:**  
  - Wrap your app in a root-level Error Boundary. This catches JS errors in any child component and prevents the app from crashing the whole UI.
  - Log errors appropriately (dev: console, prod: Sentry/logging service).
  - Show a generic error UI, but never reveal sensitive error details to end-users in production.

- **API/network errors:**  
  - Globally catch with Axios interceptors.
  - Use React Query’s `onError` to surface errors via Toaster notifications or error banners.
  - Always guide the user on what action to take if possible (e.g., retry, contact support).

---

## 5. Example Scripts

```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "lint": "eslint . --ext .ts,.tsx",
    "format": "prettier --write .",
    "test": "vitest run",
    "test:ui": "vitest --ui",
    "test:e2e": "playwright test",
    "prepare": "husky install"
  }
}
```

---

## 6. Extensibility & Recommendations

- **State management**: Use React Query and context first. Only add global state libs (Zustand, Redux Toolkit) if complexity demands.
- **Analytics/logging:** Integrate Sentry, LogRocket, or Datadog for error monitoring and real user metrics.
- **Performance monitoring:** Set up bundle size checks and Lighthouse audits in CI.
- **API types:** Prefer automatic TS type generation from your API schema (OpenAPI, tRPC, etc.) for robust FE/BE contract.
- **Storybook/Histoire:** For large teams or design systems, use for interactive component documentation.
- **Mobile responsiveness and dark mode:** All components and layouts must be responsive and support dark mode (Tailwind makes this simple).
- **.env.example:** Always up-to-date to avoid onboarding issues.

---

## 7. References

- [shadcn/ui Docs](https://ui.shadcn.com/docs)
- [React Query Docs](https://tanstack.com/query/latest)
- [React Router Docs](https://reactrouter.com/en/main)
- [Vitest Docs](https://vitest.dev/)
- [Testing Library Docs](https://testing-library.com/docs/react-testing-library/intro/)
- [Playwright Docs](https://playwright.dev/)
- [react-i18next Docs](https://react.i18next.com/)
- [OWASP SPA Security](https://cheatsheetseries.owasp.org/cheatsheets/SPA_Security_Cheat_Sheet.html)

---

This architecture provides a robust, extensible, and maintainable foundation for modern React enterprise applications. Review and adapt as your team, domain, or requirements grow.
