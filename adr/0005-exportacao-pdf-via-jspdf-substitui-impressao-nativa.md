# Exportação de PDF passa a usar jsPDF, substitui a impressão nativa

[0004](./0004-exportacao-pdf-via-impressao-nativa.md) havia optado por `window.print()` para evitar uma dependência nova. Na prática, isso abre o diálogo de impressão do sistema e exige que a pessoa escolha "Salvar como PDF" manualmente — fricção maior do que o esperado. Trocamos para a biblioteca **jsPDF** (carregada via CDN, sem passo de build): o botão "Baixar PDF" agora monta o PDF programaticamente com os blocos da escala da pessoa e dispara o download direto, sem diálogo nenhum.

## Consequences

- O CSS de impressão (`@media print`) foi removido — não é mais usado.
- Isso reintroduz uma dependência de rede na primeira vez que alguém clica em "Baixar PDF" (para baixar o script do CDN), o que pesa contra o objetivo de resiliência a wifi ruim no evento (ver [0002](./0002-vercel-supabase-substituem-github-pages-estatico.md)). Depois do primeiro carregamento, o navegador cacheia o script normalmente.
