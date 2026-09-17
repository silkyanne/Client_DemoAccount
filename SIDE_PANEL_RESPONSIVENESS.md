# Side Panel Responsiveness — Consolidated Requests

## Panel persistence

- Clicking a different tab while the side panel is open keeps it open.
- Clicking a different tab while the side panel is closed keeps it closed.
- Clicking the currently active tab toggles the panel open or closed.
- Lumière/logo toggling remains independent from tab selection.
- Active-tab highlighting remains intact across every account.

## Account scope

- Apply the responsive side-panel work to the Executive account.
- Keep Admin, WOP, and Purchasing unchanged.
- Do not alter unrelated account navigation or layouts.

## Desktop and tablet behavior

- Above 1024px, keep the Executive rail as a left-side panel and expand the workspace into multiple columns.
- From 768px through 1024px, use responsive two-column layouts where appropriate.
- Preserve the existing Sidebar Rail shell, desktop logo toggle, active-tab highlighting, and route behavior.
- Prevent horizontal clipping, awkward stretching, or content hidden behind navigation.

## Mobile behavior below 768px

- Move the Executive side panel/navigation rail to the bottom of the viewport.
- Make the mobile rail full-width and fixed using `fixed bottom-0 inset-x-0`.
- Add a subtle top border and bottom safe-area padding.
- Add bottom clearance to the page content so the fixed rail never covers cards, buttons, or forms.
- Use a horizontally scrollable or compact touch-friendly tab row when needed.
- Ensure every navigation button is easy to tap on a phone.
- Remove the orphan floating `L` above the mobile navigation.
- Do not show the desktop logo artifact above the mobile rail.
- Preserve mobile active-tab highlighting and route switching.

## Executive dashboard mobile layout

- Replace vertically stacked metric cards with a compact `grid-cols-2` layout.
- Display Portfolio Health, Total Events, Completed Events, and Ongoing Events in a 2-by-2 arrangement.
- Use compact card padding such as `p-3.5` while preserving the paper-card appearance.
- Keep the dashboard sleek, compact, and luxury-polished without excessive scrolling.
- Keep date/time on the left side of the mobile header in a small muted style.
- Align circular notification and profile controls on the right with appropriate top padding.

## Responsive Executive portal

- Mobile: clean single-column content where a section cannot fit two columns; compact two-column metric grid.
- Tablet: two-column grids for cards and workspace sections.
- Desktop: full multi-column workspace.
- Preserve the Asset Kiosk tab, item detail modals, dual sign-off workflows, analytics, tabs, and navigation actions.
- Keep buttons, filters, tabs, modal actions, and other interactive elements touch-friendly on small screens.

## Login page responsiveness

- Make the login page work across mobile phones, tablets, laptops, and desktop screens.
- Use mobile-first spacing and prevent card/form overflow.
- Scale headings and typography appropriately at narrow widths.
- Keep inputs, password visibility controls, links, and buttons touch-friendly.
- Preserve the current authentication behavior and visual direction.

## Visual design to preserve

- Luxury paper-card background: `#faf8f5`.
- Thin borders.
- Serif headings.
- Uppercase sub-labels.
- Existing spacing, colors, active states, modals, and workflows should remain visually consistent except where mobile compactness requires adjustment.

## Acceptance checklist

- [ ] Active tab toggles the panel only when clicked again.
- [ ] Switching tabs preserves the panel's open/closed state.
- [ ] Lumière/logo toggling remains independent.
- [ ] Executive rail is on the left on desktop/tablet layouts.
- [ ] Executive rail is fixed to the bottom below 768px.
- [ ] Mobile rail includes safe-area padding and does not cover content.
- [ ] No orphan `L` appears above the mobile rail.
- [ ] Executive metrics fit into a compact 2-by-2 mobile grid.
- [ ] Mobile header date/time and action buttons align correctly.
- [ ] Login page is responsive and touch-friendly.
- [ ] Asset Kiosk, item modals, dual sign-off, tabs, and navigation remain functional.
- [ ] Admin, WOP, and Purchasing are untouched.
- [ ] Luxury paper-card styling remains intact.
