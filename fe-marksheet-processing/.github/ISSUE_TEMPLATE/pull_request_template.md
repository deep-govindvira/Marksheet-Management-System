## Summary
Describe what this PR changes on the UI/UX or frontend logic.  
Include context for reviewers (what & why).

## Related Issues
Required: Link the User Story or Bug this PR resolves.  
Example:  
- Fixes #123  
- Related to #456  

## Screenshots / Recordings (Required for UI Changes)
Include:
- Before / After screenshots  
- Screen recordings for interactions  
- Mobile vs Desktop if responsive

## Changes Included
- Components added/updated
- State management changes
- Data fetching / API interactions
- Styling (CSS/SCSS/Tailwind) changes
- Routing changes (Next.js app/pages router)
- Error states or empty states handled
- Feature flags added/updated

## Technical Notes
Include relevant technical details:
- API contract used + example payloads  
- Loading states, error handling  
- Performance considerations (bundle size, hydration, layout shift)
- Accessibility decisions (ARIA roles, semantic HTML)
- SSR/CSR implications (Next.js)

## Testing
Describe testing performed:
- Unit tests (Jest / RTL)
- Integration tests (Playwright / Cypress)
- Manual verification steps
- Cross-browser testing
- Responsive (mobile/desktop) testing

## Deployment / Rollback Notes
Required if PR changes core behavior:
- Feature flag availability
- Rollback expectations
- Screenshot diffs if visual changes are large

## Checklist
### Functionality & UX
- [ ] Meets Figma design
- [ ] Works on Chrome, Firefox, Safari, Edge
- [ ] Mobile and desktop layouts verified
- [ ] Accessibility (WCAG, keyboard, ARIA) checked
- [ ] Handles loading/error/empty states

### Code Quality
- [ ] Follows project coding standards
- [ ] No console warnings or errors
- [ ] No unused variables or commented-out code
- [ ] Types updated (TypeScript)
- [ ] Component structure follows conventions

### Testing
- [ ] Unit tests added/updated
- [ ] Integration/e2e tests added/updated
- [ ] All tests pass locally
- [ ] Cross-browser testing done

### Documentation
- [ ] Storybook updated (if applicable)
- [ ] README / developer docs updated

### Review Readiness
- [ ] PR linked to a User Story/Bug
- [ ] PR assigned to a reviewer
- [ ] PR title follows naming standards
