# Processos e Serviços — Sprint 2

## 1. Inventário de processos e serviços

| Componente | Executa como | Iniciado por | Perfil | Recurso crítico | Se parar | Controle |
|---|---|---|---|---|---|---|
| Proxy / Servidor Web | Processo/serviço | Sistema operacional/serviço de inicialização | I/O e rede | Rede e memória | Usuários deixam de acessar a aplicação | Health check, logs, monitoramento e reinício |
| Aplicação Web / API | Processo | Sistema operacional/serviço de inicialização | Misto: CPU, memória, I/O e rede | CPU e memória | Operações de catálogo, estoque, pedidos e integrações ficam indisponíveis | Health check, logs, monitoramento e reinício |
| Banco de Dados | Processo/serviço | Sistema operacional/serviço de inicialização | I/O e memória | Memória, armazenamento e I/O | Consultas, criação de pedidos e atualização de estoque podem falhar | Monitoramento, logs, backup e recuperação |
| Logs e Monitoramento | Serviço/mecanismo operacional | Serviço de monitoramento | I/O | Armazenamento | Falhas podem deixar de ser registradas ou detectadas | Monitoramento, controle de espaço e retenção de logs |

## 2. Ciclo de vida

### Proxy / Servidor Web

- **Como inicia:** iniciado pelo ambiente operacional como serviço.
- **Como saber que está saudável:** responde às verificações de disponibilidade.
- **Como encerra normalmente:** parada controlada do serviço.
- **Como detectar falha:** health check sem resposta ou registros de erro.
- **Como recuperar:** reinício do serviço e análise dos logs.

### Aplicação Web / API

- **Como inicia:** iniciado pelo ambiente operacional como processo/serviço.
- **Como saber que está saudável:** health check responde e o processo permanece disponível.
- **Como encerra normalmente:** parada controlada da aplicação.
- **Como detectar falha:** health check sem resposta, processo encerrado ou erros nos logs.
- **Como recuperar:** reinício do processo/serviço e análise dos logs.

### Banco de Dados

- **Como inicia:** iniciado pelo ambiente operacional como serviço.
- **Como saber que está saudável:** serviço disponível e respondendo às operações necessárias.
- **Como encerra normalmente:** parada controlada do serviço.
- **Como detectar falha:** indisponibilidade, falhas de conexão ou erros de I/O.
- **Como recuperar:** reinício do serviço e, quando necessário, recuperação a partir de backup.

### Logs e Monitoramento

- **Como inicia:** disponibilizado pelo mecanismo/serviço de monitoramento.
- **Como saber que está saudável:** eventos continuam sendo registrados e há espaço disponível.
- **Como encerra normalmente:** parada controlada do mecanismo.
- **Como detectar falha:** ausência de registros, falha no monitoramento ou falta de espaço.
- **Como recuperar:** restabelecimento do mecanismo e controle do espaço utilizado.

## 3. Hipótese de falha

### Falha da Aplicação Web / API

**Sintoma:** usuários não conseguem acessar ou concluir operações de catálogo, estoque ou pedidos.

**Evidências esperadas:**

- health check sem resposta;
- processo da aplicação encerrado ou indisponível;
- mensagens de erro nos logs;
- consumo anormal de CPU ou memória.

**Recuperação:**

1. Confirmar a indisponibilidade pelo health check.
2. Verificar o estado do processo.
3. Consultar os logs.
4. Reiniciar o processo/serviço.
5. Verificar novamente a disponibilidade.
6. Registrar a causa e o impacto da falha.

**Risco:** indisponibilidade das operações principais da LudCommerce.

## 4. Dependências e comunicação

O fluxo principal considerado é:

1. Cliente acessa o Proxy/Servidor Web.
2. O Proxy encaminha a requisição para a Aplicação Web/API.
3. A aplicação consulta e atualiza o Banco de Dados.
4. A aplicação utiliza o armazenamento de arquivos quando necessário.
5. A aplicação se comunica com serviços externos de pagamento, fornecedor e entrega.
6. Eventos e falhas são registrados nos mecanismos de logs e monitoramento.

Os módulos de catálogo, estoque, pedidos, pagamento, fornecedor e entrega são tratados como responsabilidades lógicas da Aplicação Web/API. Nesta etapa, não são considerados processos ou servidores independentes.

## 5. Concorrência e recursos

As operações de compra podem ocorrer simultaneamente. O controle do estado do estoque deve evitar inconsistências quando mais de uma operação tentar utilizar o mesmo recurso.

Os principais recursos do Sistema Operacional considerados são:

- CPU;
- memória;
- armazenamento;
- I/O;
- rede;
- processos e serviços;
- permissões de acesso.

## 6. Decisões da Sprint 2

- Manter a Aplicação Web/API como componente central do processamento.
- Tratar catálogo, estoque, pedidos e integrações como responsabilidades lógicas da aplicação.
- Considerar Proxy, Aplicação Web/API e Banco de Dados como os principais processos/serviços operacionais.
- Utilizar health checks, logs e monitoramento de recursos como mecanismos de detecção.
- Considerar reinício de processos/serviços como estratégia inicial de recuperação.
- Considerar backup e recuperação para o Banco de Dados.

## 7. Débitos técnicos

A arquitetura atual é conceitual e ainda não define:

- tecnologia específica do Proxy/Servidor Web;
- tecnologia específica do Banco de Dados;
- ferramenta específica de monitoramento;
- política automatizada de restart;
- parâmetros reais de health check;
- infraestrutura definitiva de produção.

Esses pontos permanecem como decisões para etapas posteriores do projeto.