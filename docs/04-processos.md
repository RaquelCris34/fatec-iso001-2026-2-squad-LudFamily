# Processos e Serviços — LudCommerce

## 1. Objetivo

Este documento descreve os principais processos e serviços envolvidos na execução da LudCommerce, suas responsabilidades, dependências, recursos do Sistema Operacional e possíveis mecanismos de controle e recuperação.

O objetivo é tornar explícito como os componentes da solução executam, iniciam, se comunicam, falham e podem ser monitorados e recuperados.

---

## 2. Inventário de Processos e Serviços

| Componente | Executa como | Iniciado por | Perfil | Recurso crítico | Se parar | Controle |
|---|---|---|---|---|---|---|
| Proxy / Servidor Web | Processo/serviço | Sistema operacional | I/O e rede | Rede | Requisições não chegam à aplicação | Health check e logs |
| Web / API | Processo/serviço | Sistema operacional | CPU e memória | CPU/memória | Sistema fica indisponível | Health check, logs e restart |
| Banco de Dados | Processo/serviço | Sistema operacional | I/O e memória | Disco/memória | Pedidos e consultas ficam indisponíveis | Monitoramento, logs e backup |
| Processamento de pedidos | Processo da aplicação | Web / API | CPU e I/O | CPU e banco | Pedidos podem não ser concluídos | Logs e recuperação |
| Controle de estoque | Processo da aplicação | Web / API | CPU e banco | Banco de dados | Estoque pode ficar inconsistente | Controle de concorrência e logs |
| Comunicação com pagamento | Processo da aplicação | Web / API | I/O e rede | Rede | Pagamentos podem não ser confirmados | Logs, retry e monitoramento |
| Comunicação com fornecedor | Processo da aplicação | Web / API | I/O e rede | Rede | Atualizações de fornecedor podem atrasar | Logs e retry |
| Comunicação com entrega | Processo da aplicação | Web / API | I/O e rede | Rede | Informações de entrega podem atrasar | Logs e retry |
| Logs e monitoramento | Serviço/processo | Sistema operacional | I/O | Armazenamento | Diagnóstico fica prejudicado | Monitoramento do próprio serviço |

---

## 3. Ciclo de Vida

### Inicialização

Os serviços principais são iniciados no ambiente do servidor e devem estar disponíveis antes do processamento normal das requisições.

A aplicação depende do banco de dados e dos serviços necessários para executar suas operações.

### Estado saudável

Um componente é considerado saudável quando está em execução e consegue realizar sua responsabilidade principal.

Os health checks devem permitir identificar se o componente está disponível ou apresenta falha.

### Execução normal

Durante a operação, os processos utilizam recursos de CPU, memória, armazenamento e rede.

A aplicação Web/API recebe as requisições e coordena as operações de pedidos, estoque, pagamento, fornecedor e entrega.

### Parada normal

A parada deve ocorrer de forma controlada, evitando perda de operações em andamento e permitindo o registro do evento em log.

### Falha

Quando um processo apresenta erro ou deixa de responder, o problema deve ser identificado por monitoramento ou health check.

A recuperação pode envolver reinicialização do processo, nova tentativa de comunicação ou intervenção manual, dependendo do tipo de falha.

---

## 4. Processos Críticos

Os componentes considerados mais críticos são:

### Web / API

É o principal ponto de processamento da aplicação. Sua indisponibilidade impede o funcionamento das principais operações da LudCommerce.

### Banco de Dados

Armazena informações necessárias para pedidos, produtos e estoque. Sua indisponibilidade compromete diretamente as operações.

### Controle de Estoque

É crítico porque alterações concorrentes podem gerar inconsistências, principalmente em situações envolvendo a última unidade disponível.

### Comunicação com Pagamento

Uma falha pode impedir a confirmação de uma venda ou deixar uma transação aguardando processamento.

### Proxy / Servidor Web

É responsável por receber e encaminhar as requisições para a aplicação. Sua indisponibilidade impede o acesso ao sistema.

---

## 5. Health Checks

Os componentes críticos devem possuir mecanismos de verificação de saúde.

O health check deve permitir identificar pelo menos dois estados:

- **Saudável:** processo em execução e respondendo normalmente.
- **Não saudável:** processo parado, indisponível ou sem resposta esperada.

A detecção de um estado não saudável deve gerar evidência nos logs e permitir uma ação de recuperação.

Os health checks são especialmente importantes para:

- Proxy / Servidor Web;
- Web / API;
- Banco de Dados;
- Serviços críticos de comunicação.

---

## 6. Política de Restart e Recuperação

Quando um processo crítico falhar, a primeira ação de recuperação pode ser uma tentativa de reinicialização.

A estratégia deve considerar:

1. Identificação da falha;
2. Registro do erro em log;
3. Tentativa de restart;
4. Verificação do health check;
5. Nova tentativa, quando aplicável;
6. Intervenção manual caso o problema persista.

Deve existir um limite de tentativas para evitar um ciclo contínuo de reinicializações.

Caso o processo continue falhando, o problema deve permanecer registrado para investigação.

---

## 7. Classificação de Workloads

Os processos possuem diferentes perfis de utilização dos recursos do Sistema Operacional.

### CPU

Processos relacionados ao processamento de pedidos e regras da aplicação podem apresentar maior utilização de CPU durante períodos de alta demanda.

### Memória

A Web/API e o banco de dados dependem de memória para manter dados e operações em execução.

### I/O

Banco de dados, armazenamento de arquivos e registros de logs possuem forte relação com operações de entrada e saída.

### Rede

Proxy, Web/API e integrações com pagamento, fornecedores e entrega dependem da comunicação de rede.

O acompanhamento desses recursos permite identificar possíveis gargalos e orientar ações de recuperação.

---

## 8. Logs Mínimos

Os logs devem registrar eventos suficientes para permitir o diagnóstico dos processos.

Eventos mínimos considerados:

- Inicialização de processo;
- Parada de processo;
- Falhas e erros;
- Tentativas de restart;
- Resultado de health checks;
- Falhas de comunicação;
- Eventos relevantes de processamento.

Sempre que possível, o registro deve permitir relacionar o evento ao processo ou componente responsável.

Os logs constituem uma das principais evidências para investigação de falhas e acompanhamento operacional.

---

## 9. Hipóteses de Falha

| Sintoma | Evidência esperada | Recuperação | Risco |
|---|---|---|---|
| Web/API indisponível | Health check falhou e logs apresentam erro | Restart do processo | Sistema indisponível |
| Banco de Dados indisponível | Falha de conexão e logs | Reinicialização ou intervenção manual | Operações interrompidas |
| Pagamento indisponível | Erro de comunicação | Retry e posterior verificação | Venda pendente |
| Serviço de entrega indisponível | Falha de comunicação | Retry | Atualização de entrega atrasada |
| Alto uso de CPU/memória | Métricas do servidor | Identificar processo causador e atuar sobre ele | Degradação de desempenho |
| Armazenamento indisponível | Erros de I/O | Verificação do recurso e recuperação | Perda de capacidade de registrar ou acessar dados |

---

## 10. Relação com o Sistema Operacional

Os processos e serviços da LudCommerce dependem diretamente dos mecanismos fornecidos pelo Sistema Operacional.

Os principais conceitos relacionados são:

- Gerenciamento de processos;
- Concorrência;
- Comunicação entre componentes;
- CPU;
- Memória;
- Entrada e saída;
- Armazenamento;
- Rede;
- Monitoramento;
- Recuperação de falhas.

A arquitetura considera esses recursos para compreender o comportamento da aplicação em execução e os impactos de possíveis falhas.

---

## 11. Decisões e Débitos da Sprint

### Decisões

- A Web/API será considerada o principal processo da aplicação.
- Banco de Dados será tratado como componente crítico.
- Health checks serão utilizados para identificar indisponibilidade.
- Logs serão utilizados como evidência operacional.
- Falhas poderão acionar restart ou retry conforme o componente.
- Deve existir limite de tentativas para evitar loops de recuperação.

### Débitos

- Definir posteriormente métricas e valores concretos de monitoramento.
- Detalhar futuramente comandos ou ferramentas específicas de health check.
- Definir configurações concretas de restart quando a tecnologia da infraestrutura for escolhida.