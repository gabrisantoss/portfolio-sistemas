# 05 · Transporte de Olhadura — das notas de campo às consultas

[Voltar ao portfólio](../README.md) · [Código e regras do módulo](https://github.com/gabrisantoss/operacoes-agricolas/tree/main/app_notas)

## Necessidade que originou o projeto

Recebo notas físicas preenchidas no campo e digito suas informações para organizar o transporte de mudas de cana destinadas ao plantio. Antes, o controle dependia principalmente de Excel. O desafio é conseguir consultar quais fazendas forneceram ou receberam mudas, as variedades, os talhões de origem e quando as operações ocorreram.

A nota continua sendo preenchida no campo e sua entrada no sistema é manual. O software organiza os registros e produz consultas e relatórios depois do lançamento; não é apresentado como captura automática das notas.

## Minha participação

Concebi o fluxo a partir da minha rotina, defini os campos e confirmei as regras que dão significado aos dados. Entre elas: uma nota representa uma viagem; motorista ou operador podem repetir viagens no mesmo dia; o talhão existente representa exclusivamente a origem. Também participei da definição dos cenários para conferir a solução.

Usei ferramentas de IA como apoio à implementação de código, testes e documentação. As tecnologias presentes no projeto não são apresentadas como competências dominadas de forma independente. A validação técnica descrita abaixo usa a demonstração sintética e ferramentas automatizadas.

## Decisões que afetam a análise

| Decisão | Consequência prática |
| --- | --- |
| Separar data de colheita e de plantio na consulta. | Uma viagem colhida em 30/04 e plantada em 02/05 aparece em abril ou maio conforme a referência escolhida. Colheita permanece padrão. |
| Tratar `talhao` como origem. | Relatórios distinguem fazenda de origem, seu talhão e fazenda de destino; não inferem um talhão de plantio que não foi coletado. |
| Combinar filtros independentes. | É possível investigar origem, destino e variedade junto da busca e do período. |
| Paginar no banco. | A consulta conta o total e devolve até 50 notas por página, em vez de carregar tudo e mostrar apenas as primeiras 1.000. |
| Explicitar o ano do fechamento. | O PDF anual usa 01/01–31/12 do ano selecionado, mesmo quando os demais relatórios usam um intervalo menor. |

A coleta de talhão de destino poderá ser avaliada futuramente como campo independente e opcional. Nenhum valor foi deduzido para registros antigos.

## Demonstração atual

![Histórico de transporte inteiramente fictício](https://raw.githubusercontent.com/gabrisantoss/operacoes-agricolas/main/docs/screenshots/notas.png)

Os filtros permanecem durante a sessão; mudá-los volta à primeira página. Datas padrão usam o dia civil local, e armazenamento indisponível não impede o uso. O autocomplete descarta respostas antigas para evitar substituir referências mais recentes.

![Relatórios e fechamento anual](https://raw.githubusercontent.com/gabrisantoss/operacoes-agricolas/main/docs/screenshots/notas-relatorios.png)

O navegador oferece PDFs diário, geral, simples, plantio detalhado, histórico de fazendas de mudas e fechamento anual, além de Excel bruto e de fluxo. As exportações usam o período e a referência do painel de relatórios e não ficam limitadas à página do histórico. A documentação do módulo explica os recortes específicos.

## Evidências e estudo do código

- [Recebimento dos filtros e rotas de relatórios](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/app_notas/web_app/server.py).
- [Consulta paginada, total e seleção por data](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/app_notas/database.py).
- [Validação das datas de referência](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/app_notas/date_reference.py).
- [Interface, filtros de sessão e proteção do autocomplete](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/app_notas/web_app/static/app.js).
- [Coleta dos relatórios](https://github.com/gabrisantoss/operacoes-agricolas/tree/main/app_notas/reporting).
- [Testes de paginação](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/app_notas/tests/test_history_pagination.py), [usabilidade](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/app_notas/tests/web_usability.test.cjs) e [execução em PostgreSQL real](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/scripts/test_notas_postgres.py).

A revisão final conferiu autenticação pelo portal, cadastro, lançamento, filtros de colheita/plantio em meses distintos, páginas com 1.124 notas fictícias em teste, PDF/Excel e os dois relatórios expostos no navegador. O registro atualizado apresenta as contagens executadas, ambiente e limites na [validação pública](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/docs/VALIDACAO.md). Esses testes não representam cobertura total nem resultados empresariais.

## Limites

O projeto público usa exclusivamente dados sintéticos e identidade neutra; não contém notas, cadastros, mapas ou documentos operacionais. A demonstração é local, não um serviço hospedado. Não há pesagem das mudas nem conversão de viagens em tonelagem medida. Também não há medição publicada de tempo economizado ou produtividade.

Os estudos [01](01-plataforma-integrada.md) e [03](03-rotinas-administrativas.md) explicam o portal e as demais rotinas; este estudo concentra as decisões e verificações do transporte.
