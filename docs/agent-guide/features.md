# GridCraft — funcionalidades e módulos

Última atualização: 2026-10-28.

## Fluxo principal

| Etapa | Entradas | Responsabilidade e dependências | Saídas |
|---|---|---|---|
| Abrir e editar | Células, fórmulas, CSV e arquivos de planilha | [core](../../crates/core/), [formula](../../crates/formula/), [functions](../../crates/functions/), [model](../../crates/model/), [calc](../../crates/calc/), [engine](../../crates/engine/) | Workbook, dependências e valores recalculados |
| Avaliar e produzir saída | Estado editado e parâmetros de saída | [xlsx](../../crates/xlsx/), [chart](../../crates/chart/), [pdf](../../crates/pdf/) | Arquivos de planilha, gráficos e saída de impressão |
| Acesso pelo usuário ou agente | Gestos, argumentos CLI ou chamadas estruturadas | [apps](../../apps/), [engine](../../crates/engine/) e interfaces descritas abaixo | Estado atualizado, resposta ou erro; comportamento detalhado nos contratos |

A tabela mostra o caminho conceitual, não uma garantia de suporte a todos os formatos. APIs, estruturas, unidades, efeitos colaterais e limites ficam na [arquitetura](../architecture.md), nos documentos de assunto e nos módulos indicados.

## Contratos e exemplos de uso

- [function-parity.md](../function-parity.md)
- [formula-input.md](../formula-input.md)
- [chart-parity.md](../chart-parity.md)
- [cli.md](../cli.md)
- [ods-import.md](../ods-import.md)
- [xlsb-import.md](../xlsb-import.md)
- [control-protocol.md](../control-protocol.md)
- [mcp.md](../mcp.md)

## Inventário de bibliotecas

Responsabilidades resumidas a partir dos manifestos e comentários de módulo do checkout. As dependências listadas são as internas diretas declaradas em `dependencies` (incluindo condicionais); não incluem dependências de teste/build nem expansão de features. O manifesto de cada linha é a fonte exata.

| Módulo / manifesto | Responsabilidade declarada | Dependências internas diretas |
|---|---|---|
| [calc](../../crates/calc/Cargo.toml) | GridCraft calculation engine: dependency graph, recalculation, evaluator, dynamic arrays | `gridcraft-core`, `gridcraft-formula`, `gridcraft-functions`, `gridcraft-model`, `gridcraft-numfmt` |
| [chart](../../crates/chart/Cargo.toml) | GridCraft charts: data resolution, layout into toolkit-free primitives, sparklines and a small rasteriser | `gridcraft-calc`, `gridcraft-core`, `gridcraft-model`, `gridcraft-numfmt` |
| [core](../../crates/core/Cargo.toml) | GridCraft core types: cell addresses, values, errors, date serials | Nenhuma declarada nesta categoria |
| [engine](../../crates/engine/Cargo.toml) | GridCraft engine: sessions, commands, history, clipboard, fill, sort, filter | `gridcraft-calc`, `gridcraft-chart`, `gridcraft-core`, `gridcraft-formula`, `gridcraft-functions`, `gridcraft-model`, `gridcraft-numfmt`, `gridcraft-pdf`, `gridcraft-xlsx` |
| [formula](../../crates/formula/Cargo.toml) | GridCraft formula language: lexer, parser, printer and reference adjustment | `gridcraft-core` |
| [functions](../../crates/functions/Cargo.toml) | GridCraft worksheet function library: math, statistics, text, dates, lookup, financial, engineering | `gridcraft-core` |
| [mcp](../../crates/mcp/Cargo.toml) | GridCraft MCP server: JSON-RPC 2.0 over stdio, driving a running app or a headless session | `gridcraft-engine` |
| [model](../../crates/model/Cargo.toml) | GridCraft document model: workbooks, sheets, cells, styles, tables, charts | `gridcraft-core`, `gridcraft-formula` |
| [numfmt](../../crates/numfmt/Cargo.toml) | GridCraft number formats: Excel format codes, General display, TEXT() | `gridcraft-core` |
| [pdf](../../crates/pdf/Cargo.toml) | GridCraft's tiny self-contained PDF 1.7 writer (standard 14 fonts, vector drawing, RGBA images) | Nenhuma declarada nesta categoria |
| [ui-egui](../../crates/ui-egui/Cargo.toml) | GridCraft egui frontend (Excel-style UI); swappable — nothing below depends on it | `gridcraft-chart`, `gridcraft-engine` |
| [xlsx](../../crates/xlsx/Cargo.toml) | GridCraft file formats: XLSX (SpreadsheetML) and CSV import/export | `gridcraft-core`, `gridcraft-formula`, `gridcraft-model` |

Ao mudar uma entrada, saída ou dependência, atualize primeiro o contrato do módulo e depois esta navegação. [Voltar ao índice](../INDEX.md).
