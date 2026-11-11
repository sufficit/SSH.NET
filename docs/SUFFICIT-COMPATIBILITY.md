# Sufficit compatibility package

This release branch packages the validated compatibility patch from 7849a10c939cc1543ab5535a8af0ec0baf503a08 as stable fork version 2026.0.100. It is distinct from upstream SSH.NET releases and the upstream PR remains unmerged at preparation time. Source behavior, signing key and existing target frameworks are preserved. Additional changes on this release branch are package version configuration, release-note provenance and preserving assembly identity 2026.0.0.1 for existing Framework bindings.

Build from this branch with `dotnet pack src/Renci.SshNet/Renci.SshNet.csproj -c Release -m:1`. The package contains the upstream MIT license. Consumer restoration requires the Sufficit compatibility feed or vendored package; no public nuget.org publication is claimed.

Validation of the compatibility patch: 2388 native net10 unit tests and 2388 tests against netstandard2.0 passed (45 existing skips in each suite). A native .NET 7 consumer passed PKCS8 parsing/signing and async-enumeration API checks. Stable release packaging and consumer integration are recorded in sufficit-standard/docs/PLAN-SSHNET-FORK-CONSUMPTION.md. No SSH.NET downgrade or SCP fix reversal is involved.

Prepared by OpenAI Codex at the maintainer's request.
