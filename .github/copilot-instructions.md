# GitLab MR Tracker - Copilot Instructions

## Project Overview
This is a single-page web application for tracking GitLab merge requests in real-time. Built as a client-side only SPA with no backend, using React, TypeScript, and Tailwind CSS. All data is stored locally in the browser.

## Tech Stack
- **Frontend**: React 18 with TypeScript
- **Styling**: Tailwind CSS
- **Build Tool**: Vite
- **Linting**: ESLint with TypeScript and React plugins
- **APIs**: Direct calls to GitLab REST API
- **Storage**: Browser localStorage

## Development Setup
- **Install**: `npm install`
- **Dev Server**: `npm run dev` (starts at http://localhost:5173)
- **Build**: `npm run build` (outputs to dist/)
- **Lint**: `npm run lint`
- No automated tests configured; coverage reports in coverage/ directory

## Architecture
- **Components**: Functional React components in separate folders (e.g., `components/MRCard/`)
- **State Management**: Custom hooks (`useMRData`, `useConfig`, `useAutoRefresh`) for data fetching and caching
- **API**: Centralized in `services/gitlabApi.ts` with parallel fetches for MR details, approvals, and notes
- **Data Flow**: Hooks manage MR categorization (my/team/other), auto-refresh (60s default), and localStorage persistence
- **Status Logic**: Derived from GitLab state + approvals/comments; handles edge cases like reopened MRs

## Code Conventions
- **Naming**: PascalCase for components, camelCase for hooks/utilities, PascalCase for enums
- **TypeScript**: Strict mode; explicit interfaces for all props/data models, no `any` types
- **Imports**: Relative paths, no barrel exports
- **Styling**: Tailwind utility classes only; responsive mobile-first design
- **Error Handling**: Custom `GitLabAPIError` class; try-catch with console warnings for non-critical operations
- **Time Formatting**: Uses `date-fns` with custom `timeFormatter.ts` for "time ago" display
- **URL Parsing**: Utilities assume standard GitLab MR URL format (`/{project}/-/merge_requests/{iid}`)
- **Config Migration**: Backward compatibility in hooks for adding new fields with defaults

## Potential Pitfalls
- **API Access**: Requires GitLab personal access token (api/read_api scope); stored insecurely in localStorage. Check for 401/403 errors.
- **CORS**: May fail with self-hosted GitLab instances blocking cross-origin requests.
- **Storage Limits**: localStorage ~5-10MB limit; no cleanup for old data.
- **Auto-refresh**: Intensive if many MRs; errors don't stop the interval.
- **Username Matching**: Case-insensitive, strips `@`; assumes unique usernames.
- **No Tests**: Manual verification required; no local test runner.

## Key Files
- `src/types/index.ts`: Core data models and interfaces
- `src/services/gitlabApi.ts`: API client and status derivation logic
- `src/hooks/useMRData.ts`: Main state management hook
- `src/components/MRCard/MRCard.tsx`: Example component pattern
- `spec/spec.md`: Detailed project specification</content>
<parameter name="filePath">/Users/panachainy/repo/personal/gitlab-mr-tracker/.github/copilot-instructions.md