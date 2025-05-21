# React Enterprise Starter

A modern, opinionated, and scalable starter for enterprise React applications.

---

## Features

- **Vite** for fast development and builds
- **TypeScript** for type safety
- **Tailwind CSS** for styling
- **shadcn/ui** for accessible, customizable UI primitives (includes Toaster)
- **React Query** for data fetching/caching
- **Axios** with centralized service for API requests and error handling
- **React Router v7+** with layouts, secure routes, and RBAC
- **Error Boundaries** and Suspense for robust error/loading states
- **react-hook-form** for forms
- **Secure authentication** (HTTP-only cookies, RBAC context)
- **Feature-first, collocated folder structure**
- **Testing:** Vitest, Testing Library, Playwright
- **Localization:** [react-i18next](https://react.i18next.com/)
- **Consistent code quality:** ESLint, Prettier, EditorConfig, Husky
- **.env management** with `.env.example`
- **Automated dependency updates** (Dependabot/Renovate ready)
- **Extensible:** Analytics/monitoring ready

---

## Getting Started

```bash
git clone https://github.com/your-org/react-enterprise-starter.git
cd react-enterprise-starter
npm install
npm run dev
```

---

## Project Structure

See [ARCHITECTURE.md](./ARCHITECTURE.md) for a deep dive into layers, design patterns, and extensibility.

---

## Scripts

| Script         | Description                               |
| -------------- | ----------------------------------------- |
| `dev`          | Start Vite development server             |
| `build`        | Build for production                      |
| `preview`      | Preview production build                  |
| `lint`         | Run ESLint                                |
| `format`       | Run Prettier                              |
| `test`         | Run Vitest unit/integration tests         |
| `test:ui`      | Run Vitest in UI/watch mode               |
| `test:e2e`     | Run Playwright E2E tests                  |
| `prepare`      | Install Husky git hooks                   |

---

## Testing

- **Unit/Integration:** [Vitest](https://vitest.dev/), [@testing-library/react](https://testing-library.com/docs/react-testing-library/intro/)
- **E2E:** [Playwright](https://playwright.dev/)

---

## Localization

- **Library:** [react-i18next](https://react.i18next.com/)
- See `src/i18n/` for configuration and translation files.

---

## Environment

- **Environment variables:**  
  - See `.env.example` for required variables.  
  - Never commit `.env` files with secrets.

---

## Code Quality

- **Linting:** ESLint (JS/TS rules)
- **Formatting:** Prettier
- **EditorConfig:** Consistent editor settings
- **Pre-commit hooks:** Husky + lint-staged

---

## Dependency Management

- Automated updates: [Dependabot](https://docs.github.com/en/code-security/supply-chain-security/keeping-your-dependencies-updated-automatically) / Renovate ready
- Security: `npm audit` and GitHub security alerts enabled

---

## Documentation

- [Architecture](./ARCHITECTURE.md)

---

## License

Private. Copyright © 2025 muhammadfaisal0034
