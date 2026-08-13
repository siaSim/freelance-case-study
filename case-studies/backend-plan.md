# Backend Plan and Boundary

Status: Planned foundation — implementation not claimed

## Goal

Create a backend that can replace the frontend's local content store with shared recipe and category persistence while preserving the existing async read boundary.

## Proposed first contract

These are proposed endpoints for the next implementation phase, not endpoints that currently exist.

### Public reads

- `GET /api/v1/recipes`
- `GET /api/v1/recipes/{slug}`
- `GET /api/v1/categories`

### Authoring writes

- `POST /api/v1/admin/recipes`
- `PATCH /api/v1/admin/recipes/{recipeId}`
- `DELETE /api/v1/admin/recipes/{recipeId}`
- `POST /api/v1/admin/categories`
- `PATCH /api/v1/admin/categories/{categoryId}`
- `DELETE /api/v1/admin/categories/{categoryId}`

The admin write routes require an explicit authentication and authorization design before they are used by the frontend.

## Compatibility target

The frontend's current read API already exposes:

- recipe listing by category, sort, query, and limit;
- recipe lookup by slug;
- related recipes;
- category listing;
- category counts;
- desktop and mobile hero selection;
- lookup by recipe slugs.

The backend adapter should preserve these behaviors at the page-facing boundary and translate them into HTTP requests.

## Persistence boundary

The backend should own:

- recipe and category persistence;
- validation of recipe references and category relationships;
- authorization for authoring writes;
- auditability of edits;
- versioned API responses.

The frontend should own:

- rendering;
- local UI state;
- optimistic or pending states;
- presentation-level filtering when explicitly chosen;
- graceful loading and error states.

## Not yet claimed

No backend framework, database, deployment, authentication provider, production scale, or operational SLA is claimed in this document. Those decisions belong in reviewed issues and commits in the organization backend repository.
