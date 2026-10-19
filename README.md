# Sistemas internos e automação

Portfólio de **Gabriel Barbosa**, estudante de Sistemas de Informação. Meu foco é transformar controles manuais em aplicações que organizam dados, conectam rotinas e tornam as informações consultáveis.

Este repositório explica os problemas, as decisões técnicas e as evidências. O código executável está em [Operações Agrícolas](https://github.com/gabrisantoss/operacoes-agricolas).

## Comece por aqui

- **Para conhecer o produto:** veja a [apresentação](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/docs/APRESENTACAO.md) e as telas abaixo.
- **Para avaliar a engenharia:** leia os estudos de caso, a [arquitetura](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/docs/ARQUITETURA.md) e o [registro de validação](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/docs/VALIDACAO.md).
- **Para experimentar:** siga a [instalação local no Windows](https://github.com/gabrisantoss/operacoes-agricolas#executar-localmente). Não há demonstração hospedada na internet.

## Projeto principal — Operações Agrícolas

Suíte funcional com um portal e quatro aplicações: Colheita e Balança, Notas e Transporte, Colaboradores e Análises Operacionais. Os backends persistem alterações em PostgreSQL e geram relatórios reais a partir de **dados inteiramente fictícios**.

![Portal integrado com dados fictícios](https://raw.githubusercontent.com/gabrisantoss/operacoes-agricolas/main/docs/screenshots/portal.png)

## Estudos de caso

Cinco perspectivas sobre o mesmo ecossistema, com estudos específicos de seus módulos:

| Estudo | Desafio | Evidência pública |
| --- | --- | --- |
| [01 · Plataforma integrada](cases/01-plataforma-integrada.md) | Unificar o acesso sem reescrever todas as aplicações. | Portal, sessão, proxy, contratos e controlador local. |
| [02 · Qualidade dos dados](cases/02-qualidade-dados.md) | Conferir pesagens, vínculos e divergências antes da análise. | Importação, regras, repositórios, testes e fechamento de safra. |
| [03 · Rotinas administrativas](cases/03-rotinas-administrativas.md) | Organizar transporte, pessoas, documentos e relatórios. | Cadastros integrados, histórico, filtros, indicadores e exportações. |
| [04 · Controle de Safra](cases/04-balanca-audit-inteligencia-operacional.md) | Conferir e analisar dados exportados do sistema corporativo, sem substituí-lo. | Importação de OS via Excel, PDFs com alerta de sobreposição, TCH com área comprovada e central de relatórios. |
| [05 · Transporte de Olhadura](cases/05-transporte-olhadura.md) | Consultar viagens de mudas a partir de notas físicas, sem confundir origem, destino e datas. | Histórico paginado, filtros combinados, seis PDFs e validação PostgreSQL. |

## Telas demonstrativas

Estas capturas são da versão executável pública. Nomes, propriedades, registros e indicadores pertencem exclusivamente ao cenário sintético. Não há módulo de mapas.

### Colheita e Balança

![Fechamento de safra do cenário fictício](https://raw.githubusercontent.com/gabrisantoss/operacoes-agricolas/main/docs/screenshots/safra.png)

### Notas e Transporte

[Estudo específico: fluxo, decisões e validação](cases/05-transporte-olhadura.md).

![Notas e transporte da demonstração](https://raw.githubusercontent.com/gabrisantoss/operacoes-agricolas/main/docs/screenshots/notas.png)

### Colaboradores

![Cadastro e acompanhamento de colaboradores fictícios](https://raw.githubusercontent.com/gabrisantoss/operacoes-agricolas/main/docs/screenshots/colaboradores.png)

### Análises Operacionais

![Indicadores operacionais calculados com dados sintéticos](https://raw.githubusercontent.com/gabrisantoss/operacoes-agricolas/main/docs/screenshots/analises.png)

As imagens anteriores permanecem em `assets/screenshots/reais-anonimizados` como material histórico; não são a referência visual da versão atual.

## Evidências e limites

Na validação local de **14/09/2026**, foram aprovados **139 testes Python, 101 testes TypeScript e 29 verificações HTTP integradas**. Na revisão de **19/10/2026** do Controle de Safra, em instalação limpa, passaram **143 testes Python e 174 testes TypeScript** ([estudo 04](cases/04-balanca-audit-inteligencia-operacional.md)). A documentação registra ambiente, procedimentos e limites. O CI do GitHub verifica arquivos versionados, sintaxe Python, build TypeScript e dependências JavaScript; a suíte integrada com PostgreSQL e Qt foi executada localmente.

Na revisão final de **19/10/2026**, após as melhorias do Transporte de Olhadura, foram aprovados **173 testes Python, 174 TypeScript e 6 JavaScript** na suíte integrada, incluindo verificações com PostgreSQL real. Foram conferidos o portal autenticado, filtros, PDFs, planilhas e capturas sintéticas ([estudo 05](cases/05-transporte-olhadura.md), [validação técnica](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/docs/VALIDACAO.md)). Esses totais se referem à demonstração integrada, não somente ao transporte.

Não apresento percentuais de economia ou produtividade sem medição. Os volumes da demonstração são fixtures para explorar regras de negócio, não dados ou resultados atribuídos a clientes.

## Minha atuação e aprendizados

Os projetos nasceram da identificação de dificuldades em rotinas administrativas e operacionais. Minha atuação envolve identificar as necessidades, organizar os fluxos, definir as regras de negócio, estruturar os dados e validar o resultado. Parte da implementação foi feita com assistentes de IA a partir dessas especificações; a conferência na aplicação e as correções de regras ficaram comigo.

Os estudos destacam decisões e compromissos de engenharia: preservar aplicações existentes, separar contratos de integração, manter testes reproduzíveis e oferecer uma experiência demonstrativa sem informações internas.

## Privacidade

As instalações operacionais e suas bases não são publicadas. A demonstração usa identidade neutra, dados sintéticos e bancos locais dedicados. Não deve ser exposta diretamente à internet nem receber dados pessoais reais. Consulte a [política de segurança](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/SECURITY.md).

## Contato

[GitHub](https://github.com/gabrisantoss) · [LinkedIn](https://www.linkedin.com/in/gabriel-santos-49874a356) · [E-mail](mailto:santozgabriiel@gmail.com)
