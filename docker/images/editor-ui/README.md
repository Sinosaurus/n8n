# editor-ui Docker images

This folder contains example Dockerfiles to build the n8n frontend (`editor-ui`) as an independent Docker image.

Files
- `Dockerfile` - Production multi-stage image: builds static assets using pnpm and serves them with nginx.
- `nginx.conf` - nginx configuration used by the production image (SPA fallback + caching).
- `Dockerfile.dev` - Development image that runs the Vite dev server inside a container (useful with volume mounts).

Build & run (production)

From the repository root (so pnpm workspace files are available in build context):

```bash
# Build the production image (set backend API URL at build time if needed)
DOCKER_BUILDKIT=1 docker build \
  --build-arg NODE_VERSION=22.21.0 \
  --build-arg VUE_APP_URL_BASE_API="http://localhost:5678/" \
  -f docker/images/editor-ui/Dockerfile \
  -t local-n8n-editor-ui:prod \
  # editor-ui Docker image

  This folder contains a simple runtime Dockerfile that serves a prebuilt
  frontend (`packages/frontend/editor-ui/dist`) using nginx. The Dockerfile
  no longer builds the frontend. Build the `dist` locally or in CI and then
  build this image which will copy the `dist` into the image.

  Files
  - `Dockerfile` - runtime-only nginx image that expects `dist` to exist in the build context.
  - `nginx.conf` - nginx configuration used by the image (SPA fallback + caching).

  Build & run (production)

  ```bash
  # 1) Build the frontend locally (from repo root)
  pnpm --filter @n8n/editor-ui build

  # 2) Build the image (it will copy the prebuilt dist)
  DOCKER_BUILDKIT=1 docker build -f docker/images/editor-ui/Dockerfile -t local-n8n-editor-ui:prod .

  # 3) Run the image
  docker run --rm -p 8080:80 local-n8n-editor-ui:prod
  # Open http://localhost:8080
  ```

  Dev workflow

  - For development, prefer running the dev server on the host (`pnpm dev`) for fastest iteration.
  - Alternatively you can run the dev server in a container locally without building the image (not covered here).

  Notes

  - Make sure `packages/frontend/editor-ui/dist` exists before building the image. If you build the image from a CI job, ensure the build step runs in the same workspace or artifacts are copied into the Docker build context.
  - This approach keeps the image small and shifts build complexity to the CI or developer machine.

  CI integration

  - Typical CI flow: build the frontend artifact, upload as pipeline artifact or keep in workspace, then build and push the nginx image that copies the artifact.
