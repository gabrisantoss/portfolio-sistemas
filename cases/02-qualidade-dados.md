# 02 · Da importação à conferência dos dados

[Voltar ao portfólio](../README.md) · [Código da demonstração](https://github.com/gabrisantoss/operacoes-agricolas)

## Problema

Um indicador de safra depende da qualidade dos registros que o alimentam. Pesagens sem vínculo correto, campos faltantes e talhões fora do contexto de colheita precisam ser identificados antes de consolidar os resultados.

## Solução demonstrada

O módulo Colheita e Balança reúne cadastros de fazendas e talhões, ordens de serviço, importação de pesagens, conferência de divergências, rateio e fechamento de safra.

```text
Arquivo de entrada
→ Prévia e mapeamento de colunas
→ Validação dos registros e vínculos
→ Confirmação e persistência
→ Consulta de divergências e indicadores
```

A demonstração inclui um CSV sintético e uma base com 8 fazendas, 32 talhões, 8 ordens de serviço e 672 pesagens. Há divergências deliberadas para permitir investigação; não são erros extraídos de uma operação real.

## Decisões técnicas

- **Contratos compartilhados:** tipos e validações ficam no workspace compartilhado entre API e interface.
- **Separação de responsabilidades:** a API organiza persistência, serviços e regras; o React apresenta a conferência e os filtros.
- **Verificação com PostgreSQL real:** os testes de repositório usam um banco de testes próprio e schemas temporários.
- **Métricas derivadas dos dados:** o cenário é gerado de forma controlada, e os indicadores são calculados pela aplicação.

A separação ajuda a localizar problemas, mas não elimina a necessidade de revisar regras e casos de borda. Um build aprovado, por si só, não comprova a exatidão de todos os indicadores.

## Onde avaliar o código

- [API, regras e testes](https://github.com/gabrisantoss/operacoes-agricolas/tree/main/balanca-audit/apps/api).
- [Interface React](https://github.com/gabrisantoss/operacoes-agricolas/tree/main/balanca-audit/apps/web).
- [Contratos e validação](https://github.com/gabrisantoss/operacoes-agricolas/tree/main/balanca-audit/packages/shared).
- [Arquivo sintético de importação](https://github.com/gabrisantoss/operacoes-agricolas/tree/main/demo-data).
- [Procedimentos e resultados dos testes](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/docs/VALIDACAO.md).

## Resultado verificável

Na validação local de 14/09/2026, **101 testes TypeScript passaram sem falhas ou testes ignorados**, incluindo verificações com PostgreSQL real. Esse número pertence à suíte da API, não significa cobertura de 100% do sistema.

![Fechamento de safra com propriedades e volumes fictícios](https://raw.githubusercontent.com/gabrisantoss/operacoes-agricolas/main/docs/screenshots/safra.png)

## Limites e aprendizado

A qualidade do relatório começa antes do gráfico: no vínculo entre registros, na interpretação do arquivo e nas regras de persistência. Ter fixtures reproduzíveis permite investigar divergências sem usar informações empresariais.

A distribuição não inclui mapas, coordenadas nem documentos geográficos. OCR, scanners físicos e provedores de IA opcionais não foram configurados ou validados; não fazem parte do caminho demonstrativo apresentado aqui.
