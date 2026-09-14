# 03 · De controles dispersos a rotinas consultáveis

[Voltar ao portfólio](../README.md) · [Código da demonstração](https://github.com/gabrisantoss/operacoes-agricolas)

## Problema

Notas de transporte, cadastros de pessoas, vencimentos de documentos e apontamentos operacionais atendem a necessidades diferentes. Quando ficam dispersos em arquivos, é difícil manter referências consistentes, consultar o histórico e consolidar relatórios.

## Solução demonstrada

Três aplicações Python organizam essas rotinas, com acesso pelo portal e persistência PostgreSQL na demonstração:

| Aplicação | Fluxo disponível | O que observar |
| --- | --- | --- |
| Notas e Transporte | Lançamento, histórico, filtros, BI e exportações. | Referências integradas de cadastros e proteção do histórico. |
| Colaboradores | Cadastro, escala, CNH e pendências documentais. | Filtros e contadores de situações de acompanhamento. |
| Análises Operacionais | Paradas, motivos, turnos, frentes e colheita. | Consolidação dos apontamentos e relatórios PDF/Excel. |

## Decisões técnicas

- Preservar mecanismos próprios de relatórios, em vez de substituir as telas por mockups.
- Integrar referências entre módulos, mantendo explícita a origem de cada cadastro.
- Manter as interfaces PyQt no código e validar o caminho web para a apresentação pública.
- Gerar pessoas, notas e apontamentos sintéticos, sem copiar cadastros empresariais.
- Executar testes Python em processos separados por arquivo para evitar interferência entre instâncias nativas do Qt.

## Evidências no código

- [Notas, transporte e relatórios](https://github.com/gabrisantoss/operacoes-agricolas/tree/main/app_notas).
- [Cadastro e acompanhamento de colaboradores](https://github.com/gabrisantoss/operacoes-agricolas/tree/main/app_colaboradores).
- [Análises, apontamentos e exportações](https://github.com/gabrisantoss/operacoes-agricolas/tree/main/analises).
- [Preparação de dados e execução de testes](https://github.com/gabrisantoss/operacoes-agricolas/tree/main/scripts).

![Notas e transporte com dados fictícios](https://raw.githubusercontent.com/gabrisantoss/operacoes-agricolas/main/docs/screenshots/notas.png)

![Acompanhamento de colaboradores fictícios](https://raw.githubusercontent.com/gabrisantoss/operacoes-agricolas/main/docs/screenshots/colaboradores.png)

## Resultado verificável

O cenário público inclui 32 colaboradores, 84 notas, 112 apontamentos de parada e 112 registros de colheita fictícios. Os dados permitem explorar filtros, situações de CNH e indicadores sem informações pessoais reais.

Na validação local de 14/09/2026, **139 testes Python foram aprovados**. As 29 verificações HTTP da suíte integrada incluíram consultas, alteração/restauração de cadastro e exportações PDF/Excel, com verificação de resposta, assinatura e conteúdo não vazio dos arquivos. Isso não equivale à revisão visual de todas as páginas de todos os relatórios.

## Aprendizado e limites

Uma rotina administrativa precisa de mais que um formulário: referências consistentes, histórico, regras de alteração e saídas que a equipe consiga utilizar. Preservar relatórios existentes facilita a continuidade, mas amplia a superfície de manutenção.

Não há medição publicada de horas economizadas ou retorno financeiro. Os resultados apresentados são funcionalidades e verificações da demonstração. O ambiente não deve receber documentos, credenciais ou dados de pessoas reais.
