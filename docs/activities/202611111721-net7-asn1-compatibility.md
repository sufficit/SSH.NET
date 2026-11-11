# SSH.NET netstandard2.0 compatibility

Technical branch commit: 7849a10c939cc1543ab5535a8af0ec0baf503a08. Four-file patch: conditional ASN.1 8.0.2 for netstandard2.0, direct public AsyncInterfaces 8 dependency, opt-in test framework selection and CI coverage, plus host Lock disambiguation in the socket test helper. SSH.NET 2026 security code is unchanged by the patch.

Reproduced ASN.1 TFM warning as an error on native net7. Reproduced CS0012 from async SFTP enumeration before declaring its interface dependency. Patched package built all five assets; 2388 tests passed for the native net10 asset and 2388 for netstandard2.0, each with 45 pre-existing skips. Native .NET 7.0.20 consumer built with -warnaserror and passed six PKCS8 encrypted/unencrypted RSA/ECDSA/Ed25519 cases, signing, verification, rejection of altered payloads and disconnected async SFTP enumeration. Audit found no vulnerable packages. Original tag 2026.0.0 plus compatibility dependency changes compiled and passed PKCS8 smoke tests on native net7. No Docker/external SSH integration run is claimed.

Local final artifact: SSH.NET.2026.0.1-prerelease.21.g7849a10c93.nupkg; SHA-256 0fcd0cafd62851747d89fb69ae2995a80ff96b5b580335bebafd48fb35436678. This artifact is a local validation package, not a NuGet publication or an installed Standard dependency. Standard is unchanged by this task.

The initial filtered Git clone lacked historical blobs required by Nerdbank.GitVersioning; a full refetch fixed the build prerequisite. Early attempts to force only project-reference framework selection exposed the real missing public AsyncInterfaces dependency; final opt-in project framework selection is restored/tested normally by default.

Upstream CONTRIBUTING references the Polars AI policy, including human submission/review. The authorized PR is opened within Sufficit's fork, with AI disclosure and without claiming human review. Implementation and records prepared by OpenAI Codex at the maintainer's request.

[Compatibility notes](../NET7-COMPATIBILITY.md), [plan](../PLAN-NET7-ASN1-COMPATIBILITY.md).

Delivery: https://github.com/sufficit/SSH.NET/pull/1 (open), branch fix/netstandard-asn1-net7, commit 7849a10c93. This is a reviewable PR in the Sufficit fork, not an upstream submission, merge, public NuGet release or Standard rollout.

## Upstream submission explicitly requested

The maintainer clarified that he wanted submission through his own GitHub account. Opened https://github.com/sshnet/SSH.NET/pull/1866 as hugodeco. Verified OPEN state, develop base, source 7849a10c939cc1543ab5535a8af0ec0baf503a08 and exactly four technical files. AI disclosure remains explicit and human review is not asserted. No listed upstream checks at initial verification; fork runs 43095593980/43095593961 were still queued. This subsequent authorized submission supersedes the earlier fork-only delivery decision.
