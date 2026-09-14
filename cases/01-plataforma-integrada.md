# 01 · Uma entrada para aplicações diferentes

[Voltar ao portfólio](../README.md) · [Código da demonstração](https://github.com/gabrisantoss/operacoes-agricolas)

## Problema

Aplicações separadas podem resolver tarefas específicas, mas também fragmentam o acesso, os cadastros e a navegação. Integrá-las exige respeitar as regras que cada módulo já implementa e definir quem é responsável por cada informação.

## Solução demonstrada

O portal de Operações Agrícolas autentica o usuário, organiza a navegação e encaminha as requisições para quatro aplicações. Cada módulo mantém seu backend e seu banco dedicado no mesmo cluster PostgreSQL demonstrativo.

```text
Navegador
└── Portal: sessão, permissões, navegação e proxy
    ├── Colheita e Balança → API TypeScript/Express
    ├── Notas e Transporte → aplicação Python
    ├── Colaboradores      → aplicação Python
    └── Análises           → aplicação Python
        Persistência: bancos PostgreSQL dedicados por módulo
```

O desenho representa acesso e persistência, não uma arquitetura de microsserviços pronta para a nuvem. A distribuição pública foi validada para uso local.

## Decisões e compromissos

| Decisão | Benefício | Custo ou limite |
| --- | --- | --- |
| Preservar módulos Python e TypeScript. | Reaproveitar regras, relatórios e interfaces. | Mais de um runtime e mais dependências no preparo. |
| Centralizar a entrada no portal. | Navegação e sessão compartilhadas. | A disponibilidade do portal afeta o acesso integrado. |
| Separar bancos por módulo. | Tornar explícita a responsabilidade pelos dados. | Integrações precisam de contratos e sincronização. |
| Criar controlador demonstrativo próprio. | Inicializar serviços, migrações e fixtures de forma reproduzível. | Pré-requisitos locais ainda precisam ser instalados. |
| Vincular todos os serviços ao loopback. | Limitar a demonstração ao computador local. | Não oferece implantação pública ou acesso remoto. |

A integração Balança → Notas usa uma identidade de serviço fictícia e uma senha aleatória gerada localmente. O diretório de execução e suas credenciais não são versionados.

## Onde avaliar o código

- [Portal e proxy](https://github.com/gabrisantoss/operacoes-agricolas/tree/main/launcher_web).
- [Código transversal e compatibilidade SQL](https://github.com/gabrisantoss/operacoes-agricolas/tree/main/agricola_shared).
- [Controlador de preparo e execução](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/demo.py).
- [Contratos TypeScript compartilhados](https://github.com/gabrisantoss/operacoes-agricolas/tree/main/balanca-audit/packages/shared).
- [Arquitetura e portas demonstrativas](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/docs/ARQUITETURA.md).

## Resultado verificável

O portal e os quatro módulos foram abertos com dados sintéticos. A validação integrada incluiu autenticação, consultas e sincronização entre aplicações. Os números e o procedimento constam no [registro de validação de 14/09/2026](https://github.com/gabrisantoss/operacoes-agricolas/blob/main/docs/VALIDACAO.md).

![Portal da suíte demonstrativa](https://raw.githubusercontent.com/gabrisantoss/operacoes-agricolas/main/docs/screenshots/portal.png)

## Aprendizado e próximos cuidados

Integrar é também definir limites: sessão, responsabilidade pelo cadastro, tratamento de falhas e ciclo de vida dos processos. Preservar aplicações existentes reduz a reescrita, mas exige disciplina nos contratos e nos testes.

Carga concorrente elevada, publicação na internet, instaladores desktop e execução gráfica Electron não foram validados. Esses itens não são apresentados como capacidades prontas.
