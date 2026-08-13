# Frontend Prototype

Status: Implemented prototype

## Problem

The project needs a recipe browsing experience that can be reviewed before the backend is connected. The frontend repository provides a visual and interactive prototype while keeping the future backend boundary explicit.

## Implemented scope

The current README and source structure document the following routes and flows:

- Home with desktop and mobile hero variations.
- Recipe browsing with category and sorting flows.
- Recipe detail pages.
- Cook mode.
- Saved recipes.
- Search.
- Authoring screens under `/admin`, including recipe and category management and JSON backup/restore.

The repository is built with React, TypeScript, and Vite.

## Content model

The public read API is already isolated behind `src/api/client.ts`. The client currently reads from `src/data/store.ts`, which keeps seed content plus a localStorage overlay. The client functions are asynchronous so a later backend adapter can replace the local implementation without changing the page-level API.

The current local authoring model is intentionally not treated as access control. The README states that the backend write endpoints must provide the real authorization boundary.

## Important boundary

At the current snapshot, the frontend is not connected to a backend. Recipe changes are local to the browser and are not a shared persistence mechanism.

The case study therefore does not claim:

- production deployment;
- shared multi-user persistence;
- authentication or authorization;
- production traffic or user counts;
- backend implementation.

## Review points

- Keep `src/api/client.ts` as the read contract when introducing the backend adapter.
- Keep localStorage behavior isolated to the prototype/store layer.
- Move admin writes behind authenticated backend endpoints before treating the authoring UI as a shared operational tool.
- Preserve the distinction between a visual prototype and a production service.
