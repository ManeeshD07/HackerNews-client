# HackerNews Client

A Vite + React single-page app that surfaces the top stories from Hacker News, lets you drill into the discussion, and manage personal bookmarks once authenticated.

## Features
- Browse the current top Hacker News stories with score-based highlighting for popular posts.
- Open the original article, or jump into a dedicated comments view that fetches the full discussion tree.
- Sign in or register via the bundled auth forms to unlock bookmark creation and deletion.
- Persist bookmarks against the companion API so saved posts are available across sessions.
- Responsive Tailwind UI with desktop and mobile navigation, loaders, and icons from Headless UI and React Icons.

## Tech Stack
- React 18 with React Router for routing and nested layouts.
- Vite 4 for local development, fast refresh, and production builds.
- Tailwind CSS with Headless UI components for styling.
- Axios for requests to the Hacker News API and the bookmark/auth services.
- React Context for lightweight user session management.

## Getting Started
### Prerequisites
- Node.js 18 LTS (or any version supported by Vite, >= 16.9) and npm.

### Installation
```bash
npm install
```

### Local Development
```bash
npm run dev
```
The dev server defaults to `http://localhost:5173`. Use `npm run host` to bind on all interfaces if you need to access it from another device.

### Production Build
```bash
npm run build
npm run preview
```
The `preview` command serves the production build locally so you can confirm everything before deploying.

## Project Structure
```
src/
  components/       # Story and bookmark list UIs
  context/          # React context for user session state
  lib/              # Auth and bookmark API helpers
  pages/            # Route modules (home, bookmarks, auth, comments)
  App.jsx           # Route layout wiring
  main.jsx          # App bootstrap with BrowserRouter
```

## External Services
Authentication and bookmark persistence rely on companion services defined in:
- `src/lib/auth.js` → `http://54.249.173.192:9898`
- `src/lib/bookmark.js` → `http://54.249.173.192:9899`

If you host your own backend, update these URLs accordingly. Both modules expose simple helpers (`login`, `register`, `createBookmark`, `deleteBookmark`, `fetchBookmarks`) that the UI calls directly.

## Notes
- Bookmarks are available only after signing in; they are fetched per-username from the bookmark service.
- Comment threads are fetched recursively from the official Hacker News REST API and rendered flat in the comments page.
- Tailwind configuration lives in `tailwind.config.cjs` and global styles in `src/index.css` / `src/App.css`.
- There are currently no automated tests; run the app locally to verify changes.

## Next Steps
Potential enhancements include swapping the hard-coded API URLs for environment variables, caching story data to avoid repeated Hacker News requests, and rendering comment nesting hierarchically.
