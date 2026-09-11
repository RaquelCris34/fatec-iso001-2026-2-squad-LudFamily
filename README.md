# LudCommerce

Projeto acadêmico desenvolvido para a disciplina **ISO001 – Sistemas Operacionais**, da FATEC Mauá.

A LudCommerce representa uma **loja de hardware e periféricos com estoque e vendas online**, utilizada como cenário para relacionar problemas reais de operação empresarial com conceitos de Sistemas Operacionais.

---

## 1. Sobre o projeto

A LudCommerce é uma empresa de médio porte que comercializa produtos de hardware e periféricos para clientes consumidores e empresas.

O projeto tem como objetivo analisar como uma arquitetura computacional pode sustentar as operações da loja, considerando aspectos como:

- processos e serviços;
- armazenamento de dados;
- arquivos e sistemas de arquivos;
- permissões e segurança;
- logs e observabilidade;
- backup e recuperação;
- desempenho;
- memória e limites de recursos;
- entrada e saída (I/O);
- rede e integrações;
- virtualização e containers.

O foco do projeto não é desenvolver uma aplicação de e-commerce completa, mas **modelar e documentar uma arquitetura capaz de suportar o cenário de negócio e seus riscos operacionais**.

---

## 2. Problema de negócio

A LudCommerce precisa garantir que suas operações de catálogo, estoque, pedidos, vendas e conciliação sejam realizadas de maneira consistente e que a plataforma permaneça disponível mesmo durante períodos de alta demanda ou diante de falhas de processos e serviços.

Entre os principais riscos identificados estão:

1. indisponibilidade de fornecedores durante compras sob demanda;
2. venda simultânea da última unidade disponível;
3. sobrecarga de CPU, memória ou I/O durante períodos de alta demanda;
4. falhas de aplicação, banco de dados, armazenamento ou serviços;
5. perda ou indisponibilidade de informações necessárias para a operação.

---

## 3. Objetivo

Projetar e documentar uma arquitetura operacional para a LudCommerce, relacionando as necessidades do negócio aos recursos e mecanismos oferecidos pelos Sistemas Operacionais.

O projeto deverá demonstrar como a arquitetura pode:

- manter a consistência das operações;
- proteger dados e recursos;
- monitorar processos e serviços;
- controlar o uso de recursos;
- registrar eventos e falhas;
- realizar backup e recuperação;
- lidar com indisponibilidade e reinicialização;
- sustentar períodos de maior demanda.

---

## 4. Cenário de negócio

A LudCommerce trabalha com dois cenários de disponibilidade de produtos:

- produtos disponíveis em estoque;
- produtos adquiridos de fornecedores parceiros conforme a necessidade do pedido.

Os pedidos podem ser pagos por:

- Pix;
- cartão;
- boleto.

As entregas são realizadas por serviços de transporte, incluindo Correios e transportadoras parceiras.

### Principais atores

- **Cliente:** consulta produtos, realiza pedidos e acompanha suas compras.
- **Administrador:** gerencia catálogo, estoque e informações da operação.
- **Equipe operacional:** acompanha pedidos, estoque, pagamentos e ocorrências.
- **Fornecedor:** fornece produtos quando necessário para atendimento dos pedidos.
- **Serviço de pagamento:** processa e confirma pagamentos.
- **Transportadora/Correios:** realiza a entrega dos pedidos.

O detalhamento do cenário está em:

[docs/01-cenario-negocio.md](docs/01-cenario-negocio.md)

---

## 5. Relação com Sistemas Operacionais

O projeto utiliza o cenário da LudCommerce para estudar a relação entre operações de negócio e recursos do Sistema Operacional.

| Necessidade do negócio | Conceito de SO relacionado |
|---|---|
| Processamento de pedidos | Processos e serviços |
| Controle de concorrência | Processos, sincronização e recursos |
| Catálogo e dados | Arquivos e armazenamento |
| Proteção das informações | Permissões e controle de acesso |
| Registro de eventos | Logs |
| Recuperação após falhas | Backup e recuperação |
| Alta demanda | CPU, memória e I/O |
| Armazenamento de arquivos | Sistema de arquivos |
| Comunicação com serviços externos | Rede e I/O |
| Isolamento de serviços | Containers/virtualização |
| Acompanhamento da operação | Observabilidade |

Essas relações serão detalhadas ao longo das próximas etapas do projeto.

---

## 6. Backlog

O backlog organiza as atividades de desenvolvimento da arquitetura e da documentação.

### Sprint 2

Principais atividades:

Principais atividades:

- definição dos requisitos iniciais;
- identificação dos componentes;
- definição da arquitetura inicial;
- mapeamento de processos e serviços;
- identificação dos processos críticos;
- definição de health checks;
- definição de política de restart e recuperação;
- classificação de workloads CPU/I/O;
- definição dos logs mínimos;
- identificação dos riscos operacionais;
- criação do diagrama de contexto;
- criação dos diagramas de containers e deployment;
- criação do diagrama de processos em runtime;
- organização das evidências.

[Backlog da Sprint 2](backlog/sprint-02.md)

---

## 7. Documentação

| Documento | Descrição |
|---|---|
| [Cenário de negócio](docs/01-cenario-negocio.md) | Contexto, problema, atores e operações da LudCommerce |
| [Requisitos](docs/02-requisitos.md) | Requisitos funcionais e não funcionais |
| [Arquitetura](docs/03-arquitetura.md) | Arquitetura proposta e relação com Sistemas Operacionais |
| [Decisões técnicas](docs/04-decisoes-tecnicas.md) | Decisões, justificativas e trade-offs |
| [Processos e serviços](docs/04-processos.md) | Processos, ciclo de vida, falhas, health checks, recuperação e logs |

> Os documentos serão preenchidos e versionados conforme o avanço das Sprints.

---

## 8. Diagramas

Os diagramas serão mantidos em formato editável e poderão possuir versões exportadas para apresentação.

- [Diagrama de contexto](diagrams/contexto.mmd)
- [Diagrama de containers](diagrams/containers.mmd)
- [Diagrama de deployment](diagrams/deployment.mmd)
- [Diagrama de processos em runtime](diagrams/runtime-processes.mmd)
---

## 9. Evidências

A pasta `evidencias/` será utilizada para armazenar registros das atividades práticas relacionadas ao projeto.

Podem fazer parte das evidências:

- comandos executados;
- informações do ambiente;
- processos observados;
- permissões;
- armazenamento;
- testes;
- logs;
- experimentos;
- resultados de simulações.

---

## 10. Estrutura do repositório

```text
.
├── README.md
├── docs/
│   ├── 01-cenario-negocio.md
│   ├── 02-requisitos.md
│   ├── 03-arquitetura.md
│   ├── 04-decisoes-tecnicas.md
│   └── 05-operacao-observabilidade.md
├── diagrams/
│   ├── contexto.mmd
│   ├── containers.mmd
│   └── deployment.mmd
├── backlog/
│   └── sprint-02.md
├── evidencias/
└── laboratorio/

