# Contributing Guidelines — Frontend (Next.js / React)

These guidelines define how frontend work should be planned, implemented, tested, and reviewed.  
All contributors must follow these rules to ensure high-quality UI, predictable behavior, and maintainable code.

---

# 1. Workflow

## 1.1 Start with a tracked issue
All frontend work must originate from:

- User Story (`user-story`)
- Bug (`bug`)
- Spike (`spike`)
- Technical Debt (`tech-debt`)

Use the appropriate GitHub Issue Template.

## 1.2 Branching
Create feature branches using these conventions:
- `feature/<issue-number>-short-summary`
- `bugfix/<issue-number>-short-summary`
- `spike/<issue-number>`
- `techdebt/<issue-number>`

Examples:
- `feature/102-update-profile-ui`
- `bugfix/55-navbar-overflow-issue`


## 1.3 Commit Message Standards
Use conventional commits:
- `feat: add new profile settings page`
- `fix: resolve layout shift on dashboard`
- `docs: update Storybook for Button component`
- `test: add RTL tests for LoginForm`
- `chore: upgrade Next.js version`


## 1.4 Pull Requests
- Use the **Frontend PR template**.
- Screenshots or video recordings required for UI changes.
- At least 1 reviewer required.
- Every PR must reference an issue (`Fixes #123`).
- PR must pass CI before merging.

---

# 2. UI/UX Requirements

## 2.1 Figma & Design Accuracy
- Follow the Figma design exactly (spacing, colors, typography).
- If a variation is needed, confirm with designer before implementing.
- Maintain consistent UI patterns and component usage.

## 2.2 Responsiveness
All UI must work on:

- Mobile (min 360px width)
- Tablet
- Desktop
- Large screens (1440px+)

Test resizing manually.

## 2.3 Accessibility (A11y)
All UI must follow:

- WCAG 2.1 AA guidelines  
- Proper ARIA attributes  
- Keyboard navigation support  
- Sufficient color contrast  
- No text inside icons without accessible labels  

Accessibility is **mandatory**, not optional.

## 2.4 Error, Loading, and Empty States
Every component with data fetching must support:

- Loading states
- Error states
- Empty states

---

# 3. Technical Guidelines

## 3.1 Architecture & Component Structure
Use:
- `src/`
- `components/`
- `pages/ or app/`
- `hooks/`
- `utils/`
- `styles/`
- `lib/`
- `services/ (API)`


Rules:
- Use **functional components** and **React hooks**.
- Keep components small and composable.
- Avoid deeply nested prop drilling (use context or state libs if needed).
- Use TypeScript everywhere.

## 3.2 Data Fetching (Next.js)
Choose based on page behavior:

- Server Components (`fetch(...)`)
- `getServerSideProps`
- `getStaticProps`
- Client components using SWR/React Query

Follow team guidelines for caching, revalidation, and SSR vs CSR decisions.

## 3.3 API Interaction
- All API calls go through a dedicated `services/` layer.
- Handle errors gracefully (no console errors visible to users).
- Validate API responses before rendering.

---

# 4. Styling Guidelines

Use consistent styling standards:

- CSS Modules, Tailwind, or styled-components (depending on project standard).
- Never mix multiple styling paradigms without purpose.
- Follow consistent spacing, typography, and breakpoints.
- No !important unless justified.

---

# 5. Testing Requirements

## 5.1 Unit Tests
Use **Jest + React Testing Library**:
- Test key logic and UI behavior.
- Test accessibility attributes.
- Mock API calls and external dependencies.

## 5.2 Integration & E2E Tests
Use:

- **Playwright** or **Cypress**

Test:
- Navigation flows  
- Form validation  
- Rendering and state transitions  
- API integration behavior  

## 5.3 Snapshot Testing (optional)
Use snapshots sparingly — only for stable UI.

## 5.4 Required coverage
Minimum:
- **70% unit test coverage**
- Critical components: 80%+

---

# 6. Code Quality Standards

## 6.1 Linting & Formatting
All code must satisfy:

- ESLint rules
- Prettier formatting
- TypeScript strict mode (`strict: true`)
- No unused variables
- No console logs (except temporary debugging)

## 6.2 Performance
Avoid:

- Large bundle sizes  
- Unnecessary re-renders  
- Inline arrow functions inside render  
- Heavy dependencies unless justified  

Use:

- `React.memo`
- `useCallback`, `useMemo` when beneficial

## 6.3 Security
- Sanitize user input.
- Never expose secrets.
- Validate all data shown in UI.
- Avoid dangerouslySetInnerHTML unless unavoidable.

---

# 7. Documentation

## 7.1 Storybook (if used)
Every reusable component must include:

- Storybook story  
- Variants (primary, disabled, loading…)  
- Controls / args  

## 7.2 Developer Docs
Update:
- README  
- Architecture diagrams  
- API usage examples  
- Component guidelines  

---

# 8. CI/CD Requirements
A PR cannot be merged unless:

- All tests pass  
- Lint and formatting pass  
- The app builds successfully  
- No TypeScript errors  
- No bundle-size regression (if monitored)  

---

# 9. After Merge
- Mark the User Story as **Done**.
- Update any linked documentation.
- Check deployment preview (Vercel or dev environment).

---

These guidelines ensure that frontend contributions are consistent, maintainable, performant, and aligned with UX expectations.



