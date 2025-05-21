# React Enterprise Starter

A modern, opinionated, and scalable starter for enterprise React applications.

## Features

- **Vite** for lightning-fast dev/build
- **TypeScript** everywhere
- **Tailwind CSS** for styling
- **shadcn/ui** for accessible, customizable UI components
- **React Query** for data fetching/caching
- **Axios** for API requests (with centralized service and interceptors)
- **React Router v7+** with layouts, secure routes, and RBAC
- **Error boundaries** and Suspense for robust error/loading states
- **react-hook-form** for performant, scalable forms
- **Secure authentication** (HTTP-only cookies, RBAC context)
- **Feature-first, collocated folder structure**
- **Testing:** Vitest, Testing Library, Playwright
- **Localization:** [react-i18next](https://react.i18next.com/)
- **Extensible:** Easily add analytics/monitoring when needed

## Getting Started

```bash
git clone https://github.com/your-org/react-enterprise-starter.git
cd react-enterprise-starter
npm install
npm run dev
```

## Project Structure

See [ARCHITECTURE.md](./ARCHITECTURE.md) for a deep dive into layers, design patterns, and extensibility.

## Scripts

- `dev` — Start Vite dev server
- `build` — Build for production
- `preview` — Preview production build
- `lint` — Run ESLint
- `format` — Run Prettier
- `test` — Run Vitest unit/integration tests
- `test:ui` — Run Vitest in UI/watch mode
- `test:e2e` — Run Playwright E2E tests

## Testing

- **Unit/Integration:** [Vitest](https://vitest.dev/), [@testing-library/react](https://testing-library.com/docs/react-testing-library/intro/)
- **E2E:** [Playwright](https://playwright.dev/)

## Localization

- **Library:** [react-i18next](https://react.i18next.com/)
- See `src/i18n/` for config and translation files.

## Documentation

- [Architecture](./ARCHITECTURE.md)

## License

Private. Copyright © 2025 muhammadfaisal0034
