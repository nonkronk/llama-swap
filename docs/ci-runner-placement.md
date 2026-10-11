# GitHub Actions runner placement

OCI ARM64 is the default for portable CI. Explicit labels prevent fallback to Unraid.

## OCI jobs

`closeinactive.yml`, `config-schema.yml`, `go-ci.yml`, `ui-tests.yml` require `[self-hosted, Linux, ARM64, oci-light]`. Register a repository-specific OCI runner and confirm it is online before merge. Bound CPU and memory, and do not expose the OCI Docker socket.

## Unraid exceptions

`containers.yml`, `release.yml`, `unified-docker-backend.yml`, `unified-docker.yml` use `[self-hosted, Linux, X64, llama-swap]` for x86-compatible Docker/build workloads. `go-ci-windows.yml` remains on a genuine Windows runner.

## Migration gates

Before merging, register and verify the OCI runner with a representative test. Do not disable the Unraid runner polling until exceptional workflows have an event-driven or manual activation path. Roll back by reverting this change. The OCI runner deployment belongs to `nonkronk/oci`.
