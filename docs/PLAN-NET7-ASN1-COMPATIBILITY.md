# SSH.NET 2026: compatibilidade ASN.1/net7

Objetivo: preservar as correções SSH.NET 2026 e tornar o asset netstandard2.0 utilizável em net7 sem aviso de suporte transitivo, com PR revisável no fork Sufficit.

1. [concluído] Reproduzir o aviso com consumo real net7 e identificar o menor ajuste de dependência compatível.
2. [concluído] Implementar o ajuste e validação de consumo, executar testes criptográficos/SCP e builds pertinentes; verificar audit.
3. [concluído] Registrar evidências e limites, enviar branch ao fork Sufficit e abrir PR no fork Sufficit com divulgação de uso de IA e material para submissão humana ao upstream.

Usar uma alteração pequena sobre develop (linha 2026.0.1), conferir também a release 2026.0.0. Não fazer downgrade de SSH.NET, remover correções SCP ou suprimir avisos. Não substituir o pacote do Standard antes de existir uma revisão validada e identificável.

Consumidor real net7 referenciando SSH.NET 2026.0.0 reproduz o aviso ASN.1 como erro com -warnaserror. Runtime 7.0.20 instalado isoladamente em /tmp apenas para validação; não é declaração de suporte oficial ao runtime EOL. Ajuste limita ASN.1 8.0.2 ao asset netstandard2.0 e preserva 10.x para os demais.

CONTRIBUTING do upstream remete à política Polars: interação por agentes é proibida e revisão humana é exigida. O PR será no fork Sufficit autorizado pelo mantenedor; nenhuma interação de escrita será feita em sshnet/SSH.NET. Leitura da política: https://raw.githubusercontent.com/pola-rs/polars/8956615c8e6f8f6379590a7b3fde8317d4a517ca/AI_POLICY.md

Problema adicional reproduzido: ListDirectoryAsync do asset netstandard2.0 expõe IAsyncEnumerable de Microsoft.Bcl.AsyncInterfaces, mas Logging 8 seleciona seu asset moderno no consumidor e elimina a dependência transitiva. Consumidor net7 falha CS0012. Declarada referência pública direta no grupo netstandard2.0. Testes da biblioteca .NET Standard em host net10 exigem também desambiguar Lock no helper de sockets; não altera o runtime da biblioteca.

Validação final: pack Release dos cinco assets; 2388 unitários nativos +2388 contra netstandard2.0 aprovados (45 skips previstos por suíte). Consumidor empacotado net7: build -warnaserror sem avisos, seis cargas PKCS8 com assinatura/verificação/tamper e enumeração async desconectada aprovadas; audit transitivo sem vulneráveis. Release 2026.0.0 com o mesmo ajuste também compilou netstandard2.0 e passou os seis casos PKCS8 em runtime7 isolado. Não foram executados testes Docker/servidor SSH externo.

Entrega: branch fix/netstandard-asn1-net7 enviada ao fork e PR https://github.com/sufficit/SSH.NET/pull/1 aberto. Fonte 7849a10c; pacote local 2026.0.1-prerelease.21.g7849a10c93. CI remoto consultado separadamente; seus resultados não são inferidos dos testes locais. Nenhuma publicação NuGet, merge ou substituição do pacote no Standard foi realizada.

## Envio ao upstream autorizado pelo mantenedor

O mantenedor esclareceu que deseja o envio pela própria conta GitHub (hugodeco). Esta instrução explícita substitui a decisão anterior de limitar o envio ao fork. Manter a divulgação de Codex e não afirmar revisão humana que não ocorreu.

4. [concluído] Conferir branch, validações e ausência de PR upstream duplicado; preparar descrição honesta para revisão.
5. [concluído] Abrir PR sshnet/SSH.NET:develop com a branch já validada do fork, usando a conta autenticada.
6. [concluído] Verificar criação/arquivos e registrar URL e estado dos checks.

PR upstream criado: https://github.com/sshnet/SSH.NET/pull/1866.

Verificado: PR 1866 OPEN, autor hugodeco, base develop e head 7849a10c939cc1543ab5535a8af0ec0baf503a08; exatamente os quatro arquivos técnicos esperados. Sem checks apresentados na consulta inicial (CI do fork ainda queued). Divulgação de Codex preservada; nenhuma revisão humana afirmada. O envio efetivo ao upstream supera a restrição de entrega anterior, por instrução explícita do mantenedor.
