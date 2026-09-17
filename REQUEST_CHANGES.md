# Lumière UI — Consolidated Change Requests

This document compiles the requested changes and project decisions from the v0 development conversation.

## 1. Panel Persistence and Navigation

- Clicking a different tab while the panel is open keeps the panel open.
- Clicking a different tab while the panel is closed keeps it closed.
- Clicking the currently active tab toggles the panel open or closed.
- Lumière continues to toggle the panel independently.
- Active-tab highlighting remains intact across all accounts.
- Preserve the Sidebar Rail navigation shell, logo toggle, and active-tab behavior.

## 2. Executive Account Responsiveness

Make the Executive account fully responsive across mobile phones, tablets, laptops, and desktop screens.

### Layout breakpoints

- Mobile phones below 768px: cards stack into a clean single-column layout where appropriate.
- Tablets from 768px to 1024px: use a two-column grid.
- Desktop viewports above 1024px: expand into a full multi-column workspace.
- Use responsive grid and flex breakpoints throughout Executive portal components.
- Ensure content does not become horizontally clipped or awkwardly stretched.

### Touch and interaction requirements

- Buttons, tabs, filters, modal actions, and other interactive controls must have touch-friendly sizing on smaller screens.
- Preserve all existing Executive functionality:
  - Asset Kiosk tab.
  - Asset/item detail modals.
  - Dual sign-off workflows.
  - Executive dashboard analytics.
  - Luxury paper-card styling.
  - Existing navigation and active-tab behavior.

### Scope restrictions

- Do not modify Admin, WOP, or Purchasing accounts.
- Do not alter the Sidebar Rail navigation shell, logo toggle, or active-tab highlights unless specifically requested by a later mobile navigation change.

## 3. Executive Mobile Navigation

For screens below 768px:

- Move the Executive side panel/navigation rail to the bottom of the screen.
- Keep the desktop Executive navigation as a left-side rail.
- Make the mobile rail full-width and touch-friendly.
- Preserve tab navigation and active-tab highlighting.
- Remove the orphan floating `L` text above the mobile navigation.
- Keep Lumière/logo behavior intact on desktop.
- Add safe-area handling for devices with bottom insets.

## 4. Responsive Login Page

Make the login page responsive across mobile, tablet, laptop, and desktop screens.

- Use mobile-first spacing and layout.
- Prevent the login card and form from overflowing narrow screens.
- Scale headings and typography appropriately.
- Keep form fields and buttons touch-friendly.
- Keep password visibility controls accessible.
- Preserve the existing visual design and authentication behavior.

## 5. Executive Dashboard Mobile Redesign

For screens below 768px, redesign the Executive Dashboard to feel compact, sleek, and luxury-polished rather than stretched.

### Metric cards

- Replace vertically stacked metric cards with a tight two-column grid.
- Use `grid-cols-2` below 768px.
- Use compact card padding such as `p-3.5`.
- Fit these metrics into a compact 2-by-2 arrangement:
  - Portfolio Health.
  - Total Events.
  - Completed Events.
  - Ongoing Events.

### Mobile header

- Place date/time on the left.
- Use a small muted font for date/time.
- Align circular notification and profile buttons neatly on the right.
- Add appropriate top padding and spacing.

### Mobile bottom navigation

- Remove the orphan `L` text above the navigation.
- Lock the navigation bar to the bottom using:
  - `fixed`.
  - `bottom-0`.
  - `inset-x-0`.
- Add a subtle top border.
- Add safe-area inset padding.
- Add content bottom clearance so dashboard content is not hidden behind the fixed navigation.

### Visual styling to preserve

- Paper-card background: `#faf8f5`.
- Thin borders.
- Serif headings.
- Uppercase sub-labels.
- Existing tabs, modals, navigation buttons, and workflows must remain functional.

## 6. Security and Production Review Findings

The code review identified the following issues that should be addressed before production publishing:

### Critical

- Authentication is client-controlled in `src/lib/auth.tsx`.
- Passwords are compared directly and appear to be stored as plaintext/password-hash fields without a secure server-side authentication boundary.
- The authenticated user is persisted in `localStorage`, which can be edited by any user through browser developer tools.
- Confirmation PINs are stored in `localStorage`.
- Privileged routes are not protected by server-side authorization checks.
- Demo credentials are visibly displayed in the login UI.

### High

- The Ground Crew login flow was reported as no longer reachable after routing changes.
- UI navigation visibility must not be treated as an authorization boundary.
- Executive, Admin, Warehouse, Purchasing, and other privileged routes require role checks.

### Medium

- The production build previously failed due to TypeScript errors in unrelated legacy Warehouse components.
- The build was configured with `noCheck` in `tsconfig.app.json` to allow the production bundle to complete, but this bypasses type checking and should be replaced with proper fixes before production release.
- Asset Kiosk loading and error states should distinguish backend/query failures from an empty inventory result.

### Low

- The mobile Executive rail hides the desktop logo toggle below the `md` breakpoint. Confirm whether a mobile equivalent is required.

## 7. GitHub and Collaboration Setup

- The project was originally connected to `silkyanne/Lumiere-UI`, which is a fork of another repository.
- The project was duplicated into the user-owned repository:
  - `https://github.com/silkyanne/Client_DemoAccount`
- Keep the repository private if the project contains credentials, internal data, or unfinished work.
- Changes in the user-owned fork do not affect the original repository unless an upstream pull request is intentionally opened and merged.
- GitHub may show the fork as behind upstream. Only sync the fork when upstream changes are intentionally desired.
- Review pull requests and failed Vercel checks before merging.

## 8. Deployment and Sharing Requirements

- Do not share a failed Vercel deployment URL with the team.
- Confirm the latest Vercel deployment is marked `Ready` before sharing.
- Share both when appropriate:
  - GitHub repository URL.
  - Successful Vercel preview or production URL.
- Antigravity imports the committed GitHub code, but does not automatically inherit:
  - Vercel environment variables.
  - Supabase integrations and project settings.
  - Vercel deployment configuration.
  - Uncommitted local changes.
  - v0 preview state.
- Reconfigure required environment variables and integrations in Antigravity.

## 9. Current Implementation Caveats

- The latest build fix allowed the production bundle to complete by adding `noCheck` to `tsconfig.app.json`.
- This is a temporary deployment workaround, not a substitute for fixing the underlying TypeScript errors.
- Before production release, restore strict type checking and resolve the existing Warehouse and other legacy type errors.
- Before sharing with a team, complete the authentication and authorization remediation described above.

## 10. Recommended Next Priorities

1. Replace client-side mock authentication with secure server-side authentication.
2. Remove visible demo credentials from the production login page.
3. Add role-based authorization to every protected route and server operation.
4. Fix the underlying TypeScript errors and remove the `noCheck` workaround.
5. Confirm the Ground Crew login flow works.
6. Add Asset Kiosk loading and error states.
7. Run a fresh production deployment and share only a `Ready` deployment URL.
8. Configure the same environment variables and integrations in Antigravity.

## 11. Acceptance Checklist

- [ ] Executive mobile layout uses compact two-column metric cards.
- [ ] Executive tablet layout uses two columns.
- [ ] Executive desktop layout uses the multi-column workspace.
- [ ] Executive mobile navigation is fixed to the bottom.
- [ ] No orphan `L` appears above mobile navigation.
- [ ] Login page works at mobile, tablet, and desktop widths.
- [ ] Asset Kiosk, modals, tabs, and sign-off workflows still work.
- [ ] Admin, WOP, and Purchasing remain unchanged.
- [ ] Active-tab highlights remain intact.
- [ ] Authentication is server-side and secure.
- [ ] Role-based authorization protects privileged routes.
- [ ] No secrets or demo credentials are exposed in production UI.
- [ ] Strict type checking passes.
- [ ] Vercel deployment status is `Ready`.
- [ ] GitHub repository and deployment links are ready to share.
- [ ] Antigravity has matching environment variables and integrations configured.
