# SSH.NET 2026: netstandard2.0 consumption on .NET 7

The compatibility patch keeps ASN.1 8.0.2 on the netstandard2.0 asset and explicitly declares Microsoft.Bcl.AsyncInterfaces 8.0.0 for its public async-enumeration API. Other library assets retain their existing dependency choices. SSH.NET itself and its 2026 SCP security fixes are retained. This does not restore official support for the end-of-life .NET 7 runtime.

A net7.0 package consumer failed `dotnet build -c Release -warnaserror` before the ASN.1 adjustment. Calling ListDirectoryAsync then exposed CS0012 before the direct interface dependency was added. Native .NET 7.0.20 validation uses six PKCS#8 fixtures (RSA, ECDSA and Ed25519, each encrypted/unencrypted), signature verification and rejection of altered messages, plus the disconnected SFTP async-enumeration API. No remote server is contacted by those checks.

Run the existing suite against the compatibility asset:

```sh
dotnet test test/Renci.SshNet.Tests/Renci.SshNet.Tests.csproj -f net10.0 -c Release -p:SshNetTargetFramework=netstandard2.0 -m:1
```

The default build and test framework selection are unchanged without that property. Linux CI includes this additional test path. Integration tests requiring Docker or external SSH servers are separate and must not be inferred from unit results.

Changes are submitted to the Sufficit fork for review. Upstream CONTRIBUTING references the Polars AI policy, requiring human interaction and review; any upstream submission must follow that policy. The patch and validation were prepared by OpenAI Codex at the maintainer's request.

[Execution plan](PLAN-NET7-ASN1-COMPATIBILITY.md).
