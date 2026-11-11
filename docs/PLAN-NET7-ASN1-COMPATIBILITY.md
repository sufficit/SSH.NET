# SSH.NET 2026: compatibilidade ASN.1/net7

Objetivo: preservar as correções SSH.NET 2026 e tornar o asset netstandard2.0 utilizável em net7 sem aviso de suporte transitivo, com PR revisável no fork Sufficit.

1. [concluído] Reproduzir o aviso com consumo real net7 e identificar o menor ajuste de dependência compatível.
2. [concluído] Implementar o ajuste e validação de consumo, executar testes criptográficos/SCP e builds pertinentes; verificar audit.
3. [em andamento] Registrar evidências e limites, enviar branch ao fork Sufficit e abrir PR no fork Sufficit com divulgação de uso de IA e material para submissão humana ao upstream.

Usar uma alteração pequena sobre develop (linha 2026.0.1), conferir também a release 2026.0.0. Não fazer downgrade de SSH.NET, remover correções SCP ou suprimir avisos. Não substituir o pacote do Standard antes de existir uma revisão validada e identificável.

Consumidor real net7 referenciando SSH.NET 2026.0.0 reproduz o aviso ASN.1 como erro com -warnaserror. Runtime 7.0.20 instalado isoladamente em /tmp apenas para validação; não é declaração de suporte oficial ao runtime EOL. Ajuste limita ASN.1 8.0.2 ao asset netstandard2.0 e preserva 10.x para os demais.

CONTRIBUTING do upstream remete à política Polars: interação por agentes é proibida e revisão humana é exigida. O PR será no fork Sufficit autorizado pelo mantenedor; nenhuma interação de escrita será feita em sshnet/SSH.NET. Leitura da política: https://raw.githubusercontent.com/pola-rs/polars/8956615c8e6f8f6379590a7b3fde8317d4a517ca/AI_POLICY.md

Problema adicional reproduzido: ListDirectoryAsync do asset netstandard2.0 expõe IAsyncEnumerable de Microsoft.Bcl.AsyncInterfaces, mas Logging 8 seleciona seu asset moderno no consumidor e elimina a dependência transitiva. Consumidor net7 falha CS0012. Declarada referência pública direta no grupo netstandard2.0. Testes da biblioteca .NET Standard em host net10 exigem também desambiguar Lock no helper de sockets; não altera o runtime da biblioteca.

Validação final: pack Release dos cinco assets; 2388 unitários nativos +2388 contra netstandard2.0 aprovados (45 skips previstos por suíte). Consumidor empacotado net7: build -warnaserror sem avisos, seis cargas PKCS8 com assinatura/verificação/tamper e enumeração async desconectada aprovadas; audit transitivo sem vulneráveis. Release 2026.0.0 com o mesmo ajuste também compilou netstandard2.0 e passou os seis casos PKCS8 em runtime7 isolado. Não foram executados testes Docker/servidor SSH externo.
