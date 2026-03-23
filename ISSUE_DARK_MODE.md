# Issue: Chatbot Text Unreadable in Dark Mode

## Description
When a user's browser or operating system is set to dark mode (`prefers-color-scheme: dark`), the chatbot's text becomes unreadable (white text on a white/light background).

## Root Cause
1. **Tailwind CSS Configuration:** Tailwind CSS v3 defaults to the `media` strategy for dark mode. This means that any `dark:` variants (e.g., `dark:text-slate-100`) are automatically applied if the system theme is dark.
2. **CSS Variables:** The application's theme colors are defined in `globals.css` using CSS variables within a `.dark` class. However, the application never applies the `.dark` class to the `html` or `body` element.
3. **Conflict:** In dark mode, Tailwind applies dark-themed text colors (white/light), but the background remains light because the `.dark` CSS variables are not active. This results in low-contrast, unreadable text.

## Proposed Fix
1. **Update `tailwind.config.js`:** Explicitly set `darkMode: 'class'` to allow manual control and consistency with CSS variable implementation.
2. **Update `globals.css`:** Ensure the theme variables are also applied via `@media (prefers-color-scheme: dark)` to support automatic dark mode without the `.dark` class, or implement a theme provider/toggle.
3. **Implement Theme Provider:** Add a simple hook/provider to manage the `dark` class on the `html` element based on user preference or system setting.

## Tasks
- [ ] Add `darkMode: 'class'` to `frontend/tailwind.config.js`.
- [ ] Update `frontend/src/app/layout.tsx` to include a client component that manages the `dark` class.
- [ ] Add a theme toggle button to the `Sidebar` or `Header`.
- [ ] Verify color contrast in both light and dark modes.
