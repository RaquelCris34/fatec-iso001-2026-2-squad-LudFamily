# Evidências — Sprint 2

## LudCommerce

**Período:** 29/08/2026 a 12/09/2026

---

## 1. Objetivo da Sprint

A Sprint 2 tem como objetivo definir a arquitetura técnica inicial da LudCommerce, identificar seus principais componentes, processos e serviços e mapear os riscos operacionais relacionados ao funcionamento da plataforma.

A arquitetura foi definida considerando o cenário de uma empresa de médio porte que atua no comércio eletrônico de produtos de informática, atendendo consumidores e empresas.

---

## 2. Entregas realizadas

Durante a Sprint 2 foram produzidos e revisados os seguintes artefatos:

- validação dos requisitos funcionais e não funcionais para utilização na arquitetura;
- identificação dos principais componentes da solução;
- definição da arquitetura técnica inicial;
- identificação dos processos e serviços envolvidos;
- mapeamento dos principais riscos operacionais;
- criação do diagrama de contexto;
- criação do diagrama de containers;
- criação do diagrama de deployment;
- registro das principais decisões técnicas da arquitetura.

---

## 3. Artefatos relacionados

### Cenário de negócio

Arquivo:

`docs/01-cenario-negocio.md`

Contém a descrição da LudCommerce, seu modelo de negócio, atores envolvidos, operações, riscos e relação do cenário com conceitos de Sistemas Operacionais.

### Requisitos

Arquivo:

`docs/02-requisitos.md`

Contém os requisitos funcionais, não funcionais e operacionais utilizados como base para a definição da arquitetura.

### Arquitetura

Arquivo:

`docs/03-arquitetura.md`

Contém a descrição da arquitetura técnica inicial, componentes, processos, serviços, fluxo de pedidos, dependências, relação com o Sistema Operacional, segurança, observabilidade, disponibilidade, recuperação e riscos operacionais.

### Decisões técnicas

Arquivo:

`docs/04-decisoes-tecnicas.md`

Contém as principais decisões arquiteturais e seus respectivos motivos, impactos e relações com os conceitos de Sistemas Operacionais.

---

## 4. Diagramas

Os diagramas foram produzidos em Mermaid, mantendo o arquivo-fonte versionado no repositório.

### Diagrama de contexto

Arquivo-fonte:

`diagrams/contexto.mmd`

Exportação:

`diagrams/contexto.png`

O diagrama apresenta os principais atores externos e as interações com a plataforma LudCommerce.

### Diagrama de containers

Arquivo-fonte:

`diagrams/containers.mmd`

Exportação:

`diagrams/containers.png`

O diagrama apresenta os principais componentes técnicos da solução e suas relações.

### Diagrama de deployment

Arquivo-fonte:

`diagrams/deployment.mmd`

Exportação:

`diagrams/deployment.png`

O diagrama apresenta a distribuição conceitual dos componentes em um ambiente baseado em servidor Linux.

---

## 5. Relação com Sistemas Operacionais

A arquitetura da LudCommerce foi definida considerando aspectos diretamente relacionados ao funcionamento de um Sistema Operacional.

Os principais pontos considerados foram:

- processos e serviços;
- gerenciamento de CPU;
- gerenciamento de memória;
- armazenamento;
- sistema de arquivos;
- permissões de acesso;
- operações de entrada e saída;
- comunicação de rede;
- concorrência;
- logs e observabilidade;
- disponibilidade;
- reinicialização e recuperação;
- backup;
- isolamento de componentes;
- gerenciamento de recursos.

Esses aspectos serão aprofundados nas próximas Sprints conforme o cronograma do projeto.

---

## 6. Riscos operacionais identificados

Foram considerados como principais riscos:

1. indisponibilidade de fornecedores parceiros;
2. concorrência entre pedidos envolvendo o último item disponível em estoque;
3. aumento de consumo de CPU, memória e I/O durante períodos de alta demanda;
4. falhas na aplicação, banco de dados ou armazenamento;
5. indisponibilidade de serviços externos;
6. perda ou indisponibilidade de informações operacionais;
7. acesso não autorizado aos recursos da plataforma.

Os riscos foram relacionados aos impactos no negócio e aos recursos do Sistema Operacional envolvidos.

---

## 7. Evidências técnicas

As evidências desta Sprint são compostas principalmente pela documentação e pelos diagramas versionados no GitHub.

A geração dos diagramas foi realizada utilizando Mermaid e Mermaid CLI, permitindo manter tanto os arquivos-fonte quanto suas respectivas exportações.

Os arquivos-fonte dos diagramas são mantidos no repositório para permitir sua revisão e evolução nas próximas Sprints.

---

## 8. Critérios de conclusão da Sprint

A Sprint 2 é considerada concluída quando:

- a arquitetura técnica inicial estiver documentada;
- os principais componentes estiverem identificados;
- os processos e serviços estiverem mapeados;
- os riscos operacionais estiverem documentados;
- os diagramas de contexto, containers e deployment estiverem disponíveis;
- as decisões técnicas estiverem registradas;
- a relação entre a arquitetura e os conceitos de Sistemas Operacionais estiver explícita;
- os artefatos estiverem versionados no GitHub.

---

## 9. Próximas etapas

Os artefatos produzidos nesta Sprint servirão como base para as próximas etapas do projeto.

Nas próximas Sprints serão aprofundados temas relacionados a:

- processos e escalonamento;
- observabilidade;
- memória e limites de recursos;
- desempenho;
- armazenamento e sistema de arquivos;
- permissões;
- logs;
- backup e recuperação;
- entrada e saída;
- rede;
- dispositivos;
- integrações;
- virtualização;
- containers;
- hardening da arquitetura.

---

## 10. Controle de versão

Esta documentação faz parte do repositório oficial do projeto LudCommerce e deve ser atualizada conforme novas evidências e decisões forem produzidas durante o desenvolvimento do projeto.