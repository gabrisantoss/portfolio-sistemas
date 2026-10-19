# 04 · Balança Audit: análise gerencial complementar ao sistema corporativo

[Voltar ao portfólio](../README.md) · [Código da demonstração](https://github.com/gabrisantoss/operacoes-agricolas)

## Contexto

O registro oficial de ordens de serviço, pesagens e entregas fica em um sistema corporativo, que é a fonte de verdade. O que faltava era uma etapa de organização e conferência entre a exportação desses dados e a análise gerencial. Essa etapa era feita em planilhas e documentos avulsos.

O Balança Audit cobre essa etapa. Ele não substitui o sistema corporativo e não envia nada de volta a ele.

```text
Sistema corporativo oficial
→ Planilha operacional exportada (ordens de serviço) e relatório padronizado de pesagem em PDF
→ Importação com prévia, conferências e alertas
→ Organização, indicadores e relatórios gerenciais
```

Tudo o que aparece aqui vem da demonstração pública, com fazendas, talhões, ordens e pesagens fictícios.

## O que a demonstração faz

### Importação gerencial de OS via Excel

A planilha operacional exportada passa por uma prévia antes de qualquer gravação, que mostra:

- as OS novas e as alterações propostas;
- as OS encerradas, que permanecem preservadas;
- as divergências, que não são aplicadas automaticamente: setor já vinculado a outra OS ativa, setor repetido em duas OS da mesma planilha, setor novo em OS encerrada e setor ausente da planilha.

A mesma planilha não pode ser importada duas vezes, porque o controle é feito pelo conteúdo do arquivo. Uma nova exportação com mudanças legítimas é aceita. Cada importação fica no histórico e gera um relatório CSV.

### Importação manual do relatório padronizado de pesagem

O relatório padronizado de pesagem chega em PDF e é inserido manualmente. Antes de gravar, a prévia compara o arquivo com os PDFs já importados:

| Situação | Comportamento |
| --- | --- |
| Arquivo idêntico | Bloqueado |
| Mesmo período ou período sobreposto com talhões em comum | Gravação só após revisão explícita |
| Conteúdo repetido | Gravação só após revisão explícita |
| Mesmo período, outras fazendas | Apenas informado e gravado |

Nenhum registro válido é descartado automaticamente. Os casos ambíguos ficam para a decisão de uma pessoa.

### Conferências e indicadores

- **Pesagens via CSV:** o separador `;` ou `,` é detectado automaticamente, o mapeamento das colunas aparece na prévia e um arquivo já importado é recusado.
- **Divergências e rateio:** pesagens sem OS e vínculos inconsistentes ficam visíveis, em vez de entrarem silenciosamente nos totais.
- **TCH com área comprovada:** a área cadastrada é diferente da área dos talhões encerrados. O TCH só usa os talhões com OS encerrada e todas as entregas dentro do período. Em recortes parciais, aparece como "parcial" ou N/D, com a explicação.

### Central de relatórios

Há um relatório geral e outro detalhado por fazenda, talhão e período. A prévia na tela e o PDF usam o mesmo cálculo. Na validação, os totais da prévia, do PDF e de uma consulta direta ao banco demonstrativo foram iguais. Também foram iguais aos do painel de safra e do rateio para a OS encerrada usada na conferência.

![Central de relatórios com dados fictícios](https://raw.githubusercontent.com/gabrisantoss/operacoes-agricolas/main/docs/screenshots/relatorios.png)

## Competências envolvidas

- **Processos:** mapear onde termina o sistema oficial e onde começa a análise complementar, sem duplicar responsabilidades.
- **Dados:** separar cadastro de comprovação, tratar a reimportação e a sobreposição de arquivos, e explicitar quando um indicador não pode ser calculado.
- **Automação:** prévias, validações e relatórios substituem conferências manuais repetitivas, mas mantêm a decisão humana nos casos ambíguos.
- **Inteligência operacional:** indicadores que avisam sobre os próprios limites, em vez de mostrar números aparentemente precisos.

## Minha participação e o uso de IA

- **Autoria:** o Balança Audit é um software de minha autoria.
- **Concepção e necessidades:** identifiquei o problema, defini o fluxo a partir do sistema corporativo e estabeleci as regras de negócio, entre elas o que conta como área comprovada, quais divergências bloqueiam ou pedem revisão e o que nunca deve ser descartado.
- **Implementação auxiliada por IA:** grande parte do código, dos testes e da documentação foi escrita com assistentes de IA, a partir das especificações e correções que eu fornecia em etapas.
- **Validação:** conferi cada etapa na demonstração, revisei os PDFs página a página, comparei os totais entre as telas e apontei inconsistências que viraram correções. Um exemplo: no cenário fictício, uma OS encerrada antes das últimas pesagens, o que exigiu corrigir o seed.

## Evidências verificáveis

Validação local de 19/10/2026, em instalação limpa: **143 testes Python e 174 testes TypeScript aprovados**, incluindo testes com PostgreSQL real e com PDFs sintéticos lidos pelo Poppler. A auditoria de dependências do npm (`--audit-level=high`) não apontou vulnerabilidades.

Esses números indicam que as suítes passaram. Não significam cobertura total nem ganhos de produtividade, que não foram medidos.

> Os itens desta seção e das telas de relatórios, importação de OS e sobreposição de PDFs dependem da publicação da branch de revisão do repositório de código. Até lá, os links apontam para a versão pública anterior.

## Limites

- Não há integração direta com o sistema corporativo. A troca de dados é feita por arquivos exportados e importados manualmente.
- O formato real das planilhas e relatórios corporativos não é reproduzido. Os arquivos da demonstração são sintéticos.
- Os controles reduzem o risco de duplicidade e de indicadores enganosos, mas não dispensam a conferência humana.
- A leitura de PDF depende do Poppler instalado localmente.
