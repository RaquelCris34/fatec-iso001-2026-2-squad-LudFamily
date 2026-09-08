# 04 - Decisões Técnicas

## 1. Objetivo

Este documento registra as principais decisões técnicas adotadas para a arquitetura da LudCommerce e os motivos que levaram a essas escolhas.

As decisões consideram as necessidades do negócio e sua relação com conceitos de Sistemas Operacionais, como processos, armazenamento, permissões, logs, desempenho, disponibilidade e recuperação.

---

## 2. ADR-001 - Arquitetura centralizada da aplicação

### Contexto

A LudCommerce precisa disponibilizar uma plataforma de e-commerce para clientes, administradores e equipe operacional.

A solução precisa concentrar o processamento das operações de catálogo, pedidos, estoque, pagamentos e entregas, mantendo uma arquitetura que possa ser administrada por uma empresa de médio porte.

### Decisão

Adotar uma aplicação Web/API central como principal ponto de processamento das operações da LudCommerce.

A aplicação ficará hospedada em um servidor Linux e será acessada por meio de um proxy/servidor web.

### Alternativas consideradas

- Separar cada funcionalidade em serviços independentes.
- Utilizar uma arquitetura totalmente distribuída.
- Concentrar todas as funcionalidades diretamente no servidor web.

### Justificativa

A aplicação central reduz a complexidade inicial da solução e facilita a administração da infraestrutura.

A arquitetura também permite separar posteriormente funcionalidades específicas caso o crescimento da operação justifique essa mudança.

### Trade-offs

**Vantagens:**

- Menor complexidade operacional.
- Facilidade de manutenção.
- Menor quantidade de componentes para administrar.
- Facilita o controle dos recursos do servidor.

**Desvantagens:**

- Uma falha na aplicação pode afetar várias operações.
- O crescimento da aplicação pode aumentar a necessidade de recursos computacionais.

### Relação com Sistemas Operacionais

A aplicação depende de processos executados no servidor Linux e dos recursos de CPU, memória e armazenamento disponibilizados pelo sistema operacional.

---

## 3. ADR-002 - Separação entre banco de dados e armazenamento de arquivos

### Contexto

A LudCommerce precisa armazenar informações estruturadas dos pedidos, estoque e pagamentos, além de arquivos utilizados pela plataforma.

Esses tipos de dados possuem características diferentes de armazenamento.

### Decisão

Separar o banco de dados do armazenamento de arquivos.

O banco será utilizado para informações estruturadas da aplicação, enquanto o armazenamento de arquivos será utilizado para arquivos da plataforma.

### Alternativas consideradas

- Armazenar todos os dados em um único local.
- Armazenar arquivos diretamente no banco de dados.
- Utilizar somente o sistema de arquivos para todas as informações.

### Justificativa

A separação facilita a organização dos dados, o controle de permissões e as estratégias de backup e recuperação.

Também permite administrar de forma independente o espaço utilizado pelos arquivos e pelos dados estruturados.

### Trade-offs

**Vantagens:**

- Melhor organização.
- Facilita backups específicos.
- Facilita o controle de permissões.
- Reduz o impacto de problemas em um tipo de armazenamento sobre o outro.

**Desvantagens:**

- Exige administração de mais de um recurso de armazenamento.
- A recuperação precisa considerar os diferentes tipos de dados.

### Relação com Sistemas Operacionais

A decisão está relacionada ao sistema de arquivos, permissões de acesso, espaço em disco, operações de entrada e saída e backup.

---

## 4. ADR-003 - Utilização de servidor Linux

### Contexto

A plataforma precisa de um ambiente de execução capaz de hospedar a aplicação e seus recursos de armazenamento.

### Decisão

Utilizar um servidor baseado em Linux como ambiente de execução da LudCommerce.

### Alternativas consideradas

- Utilizar um servidor baseado em Windows.
- Utilizar exclusivamente serviços gerenciados de terceiros.

### Justificativa

O Linux oferece um ambiente adequado para execução de aplicações web e permite trabalhar diretamente com conceitos de Sistemas Operacionais abordados no projeto, como processos, permissões, armazenamento, logs, serviços e monitoramento.

### Trade-offs

**Vantagens:**

- Controle sobre processos e serviços.
- Controle de permissões.
- Facilidade de observação dos recursos do sistema.
- Possibilidade de utilização de ferramentas de administração por terminal.

**Desvantagens:**

- Exige conhecimento para administração do ambiente.
- A equipe precisa definir procedimentos de operação e recuperação.

### Relação com Sistemas Operacionais

Essa decisão estabelece o sistema operacional como parte fundamental da infraestrutura da LudCommerce.

---

## 5. ADR-004 - Integrações externas desacopladas da aplicação

### Contexto

A LudCommerce depende de serviços externos para pagamentos, fornecimento de produtos e entrega.

A indisponibilidade desses serviços pode afetar o processamento dos pedidos.

### Decisão

Manter as integrações externas como serviços independentes da infraestrutura da LudCommerce.

A aplicação realizará as solicitações necessárias e registrará os resultados recebidos.

### Alternativas consideradas

- Integrar diretamente cada fornecedor à estrutura interna da aplicação.
- Não utilizar integrações externas e realizar todas as operações manualmente.

### Justificativa

A separação permite identificar claramente os limites da responsabilidade da LudCommerce e os pontos de dependência externa.

Também facilita o tratamento de falhas e a observabilidade das operações.

### Trade-offs

**Vantagens:**

- Separação de responsabilidades.
- Identificação clara das dependências externas.
- Facilita o tratamento de indisponibilidade.
- Permite substituir um serviço externo futuramente.

**Desvantagens:**

- A operação depende da disponibilidade dos serviços externos.
- Falhas de comunicação podem interromper ou atrasar operações.

### Relação com Sistemas Operacionais

As integrações dependem de processos de comunicação e operações de entrada e saída de rede, além de registros em logs para diagnóstico de falhas.

---

## 6. ADR-005 - Registro de logs operacionais

### Contexto

A LudCommerce precisa identificar falhas, acompanhar operações e investigar problemas relacionados a pedidos, estoque, pagamentos e integrações.

### Decisão

Registrar eventos relevantes da aplicação e das operações em logs operacionais.

Os logs devem permitir identificar acontecimentos importantes e auxiliar na investigação de falhas.

### Alternativas consideradas

- Não manter registros operacionais.
- Registrar somente erros críticos.
- Registrar todos os eventos sem qualquer controle de volume.

### Justificativa

Os logs são necessários para observabilidade e diagnóstico.

O registro deve ser suficiente para investigar problemas sem gerar volume desnecessário de informações.

### Trade-offs

**Vantagens:**

- Facilita diagnóstico.
- Permite rastrear eventos.
- Auxilia na recuperação de incidentes.
- Apoia o monitoramento da operação.

**Desvantagens:**

- Ocupa espaço de armazenamento.
- Exige política de retenção e gerenciamento.

### Relação com Sistemas Operacionais

Os logs utilizam armazenamento e operações de entrada e saída. O crescimento excessivo dos arquivos pode consumir espaço em disco e afetar a operação.

---

## 7. ADR-006 - Estratégia de backup e recuperação

### Contexto

A indisponibilidade ou perda de dados pode interromper vendas, afetar informações de estoque e comprometer a operação da LudCommerce.

### Decisão

Adotar uma estratégia de backup dos dados importantes e definir procedimentos de recuperação.

O processo deverá considerar principalmente o banco de dados e os arquivos necessários para o funcionamento da plataforma.

### Alternativas consideradas

- Não realizar backups.
- Realizar backups manuais sem periodicidade definida.
- Realizar backups automatizados e controlados.

### Justificativa

A recuperação precisa ser planejada antes da ocorrência de uma falha.

O backup reduz o impacto de problemas relacionados ao armazenamento e à perda de dados.

### Trade-offs

**Vantagens:**

- Redução do risco de perda de dados.
- Facilita a recuperação após falhas.
- Aumenta a continuidade operacional.

**Desvantagens:**

- Consome armazenamento.
- Exige controle e validação dos backups.
- A recuperação pode exigir indisponibilidade temporária.

### Relação com Sistemas Operacionais

A estratégia envolve armazenamento, sistema de arquivos, permissões, operações de entrada e saída e recuperação de dados.

---

## 8. Resumo das decisões

| Decisão | Escolha | Principal motivo |
|---|---|---|
| Arquitetura | Aplicação Web/API central | Reduzir complexidade inicial |
| Dados | Banco separado de arquivos | Organização e recuperação |
| Sistema operacional | Linux | Controle dos recursos e relação com SO |
| Integrações | Serviços externos independentes | Separação de responsabilidades |
| Logs | Registro de eventos operacionais | Observabilidade e diagnóstico |
| Backup | Estratégia de backup e recuperação | Reduzir impacto de falhas |

---

## 9. Relação geral com Sistemas Operacionais

As decisões técnicas da LudCommerce estão diretamente relacionadas aos recursos e responsabilidades do sistema operacional.

Os principais pontos são:

- **Processos:** execução da aplicação e dos serviços.
- **CPU e memória:** recursos utilizados pelos processos durante o processamento das operações.
- **Sistema de arquivos:** armazenamento dos arquivos da plataforma e dos logs.
- **Permissões:** controle de acesso aos recursos e arquivos.
- **Entrada e saída:** operações de armazenamento e comunicação de rede.
- **Logs:** registro de eventos para observabilidade e diagnóstico.
- **Backup e recuperação:** proteção dos dados e continuidade da operação.
- **Disponibilidade:** capacidade de manter os serviços funcionando e recuperar a operação após falhas.