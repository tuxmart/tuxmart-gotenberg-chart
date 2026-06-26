# Gotenberg Helm chart

This repository packages the Gotenberg Helm chart used to run Gotenberg as a
standalone Kubernetes Deployment.

The chart lives under `charts/gotenberg/` to follow the standard Helm chart
repository layout used by chart-releaser and OCI publishing. The repository is
single-purpose today; the root files are convenience entry points for that chart.

## Chart

- [Gotenberg](charts/gotenberg/)

## Helmfile

This repository includes an optional root `helmfile.yaml` that delegates to the
Gotenberg chart Helmfile. It is a convenience wrapper for the single chart, not
a multi-service orchestration layer. Environment overlays live in
`charts/gotenberg/environments/<env>/values.yaml`.

```console
export GOTENBERG_ENV=dev # or staging | prod
helmfile template
```

`GOTENBERG_ENV` takes precedence over `SENTINEL_ENV`. If neither is set, the
chart renders the `dev` overlay. `RELEASE_NAMESPACE` can be used to override the
release namespace.

Common Helmfile environment overrides:

- Release: `GOTENBERG_RELEASE_NAME`, `RELEASE_NAMESPACE`, `GOTENBERG_ENV`, `SENTINEL_ENV`
- Image: `GOTENBERG_IMAGE_REPOSITORY`, `GOTENBERG_IMAGE_TAG`, `GOTENBERG_IMAGE_PULL_POLICY`
- Service: `GOTENBERG_SERVICE_TYPE`, `GOTENBERG_SERVICE_PORT`, `GOTENBERG_SERVICE_LOAD_BALANCER_IP`
- API: `GOTENBERG_API_TIMEOUT`, `GOTENBERG_API_BODY_LIMIT`, `GOTENBERG_API_DISABLE_DOWNLOAD_FROM`
- Chromium: `GOTENBERG_CHROMIUM_AUTO_START`, `GOTENBERG_CHROMIUM_START_TIMEOUT`, `GOTENBERG_CHROMIUM_DISABLE_WEB_SECURITY`, `GOTENBERG_CHROMIUM_MAX_CONCURRENCY`, `GOTENBERG_CHROMIUM_MAX_QUEUE_SIZE`
- LibreOffice: `GOTENBERG_LIBREOFFICE_AUTO_START`, `GOTENBERG_LIBREOFFICE_START_TIMEOUT`, `GOTENBERG_LIBREOFFICE_DISABLE_ROUTES`, `GOTENBERG_LIBREOFFICE_MAX_QUEUE_SIZE`
- Capacity: `GOTENBERG_RESOURCES_CPU`, `GOTENBERG_RESOURCES_MEMORY`, `GOTENBERG_AUTOSCALING_ENABLED`, `GOTENBERG_AUTOSCALING_MIN_REPLICAS`, `GOTENBERG_AUTOSCALING_MAX_REPLICAS`, `GOTENBERG_AUTOSCALING_TARGET_CPU`, `GOTENBERG_AUTOSCALING_TARGET_MEMORY`
- Availability/security: `GOTENBERG_PDB_CREATE`, `GOTENBERG_PDB_MIN_AVAILABLE`, `GOTENBERG_NETWORK_POLICY_ENABLED`, `GOTENBERG_NETWORK_POLICY_ALLOW_INGRESS`, `GOTENBERG_NETWORK_POLICY_ALLOW_EGRESS`, `GOTENBERG_AUTOMOUNT_SERVICE_ACCOUNT_TOKEN`
- Long-running report tuning: `GOTENBERG_GRACEFUL_SHUTDOWN_SECONDS`, `GOTENBERG_PRESTOP_SLEEP_SECONDS`, `GOTENBERG_TMP_SIZE_LIMIT`, `GOTENBERG_PRIORITY_CLASS_NAME`, `GOTENBERG_PRIORITY_CLASS_CREATE`, `GOTENBERG_PRIORITY_CLASS_VALUE`

## OCI Repositories

The recommended way to install this chart is via OCI and the `helm search hub maikumori` command should list the available package.

## Non-OCI Repository

If you don't want to use the OCI repositories you can add the `maikumori` repository as follows.

```console
helm repo add maikumori https://maikumori.github.io/helm-charts/
helm repo update
```
