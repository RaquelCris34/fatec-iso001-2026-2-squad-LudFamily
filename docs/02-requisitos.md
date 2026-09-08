# Requisitos da LudCommerce

## 1. Objetivo

Este documento define os requisitos funcionais e não funcionais da LudCommerce, considerando o cenário de uma loja de hardware e periféricos com estoque e vendas online.

Os requisitos foram definidos a partir do problema de negócio identificado e servirão como base para a definição da arquitetura, dos componentes técnicos, dos processos e dos controles operacionais.

---

## 2. Requisitos funcionais

### RF01 — Consultar catálogo

**Descrição:**  
O sistema deve permitir que clientes consultem o catálogo de produtos disponíveis para venda.

**Atores:** Cliente, Administrador.

**Critério de aceite:**
- Dado que o catálogo esteja disponível;
- Quando o cliente acessar a loja;
- Então os produtos cadastrados devem ser apresentados com suas informações básicas.

**Conexão com Sistemas Operacionais:**
- Arquivos e armazenamento;
- Processos e serviços;
- Desempenho de leitura.

---

### RF02 — Consultar disponibilidade de estoque

**Descrição:**  
O sistema deve permitir consultar a quantidade disponível de cada produto.

**Atores:** Cliente, Administrador, Equipe operacional.

**Critério de aceite:**
- Dado que um produto esteja cadastrado;
- Quando sua disponibilidade for consultada;
- Então o sistema deve apresentar a quantidade disponível ou indicar que o produto precisa ser adquirido de fornecedor.

**Conexão com Sistemas Operacionais:**
- Armazenamento;
- Processos concorrentes;
- Consistência de dados.

---

### RF03 — Criar pedido

**Descrição:**  
O sistema deve permitir que clientes criem pedidos contendo um ou mais produtos.

**Atores:** Cliente.

**Critério de aceite:**
- Dado que os produtos estejam disponíveis para venda;
- Quando o cliente confirmar a compra;
- Então um pedido deve ser registrado com seus respectivos produtos e quantidades.

**Conexão com Sistemas Operacionais:**
- Processos;
- Concorrência;
- Armazenamento;
- Persistência de dados.

---

### RF04 — Controlar concorrência na venda

**Descrição:**  
O sistema deve impedir que dois pedidos confirmados consumam simultaneamente a mesma unidade disponível em estoque.

**Atores:** Sistema.

**Critério de aceite:**
- Dado que exista apenas uma unidade disponível;
- Quando dois pedidos tentarem adquirir essa unidade simultaneamente;
- Então somente uma operação deve confirmar a reserva da unidade.

**Conexão com Sistemas Operacionais:**
- Processos concorrentes;
- Sincronização;
- Controle de recursos;
- Consistência.

---

### RF05 — Registrar pagamento

**Descrição:**  
O sistema deve registrar o pagamento associado ao pedido.

**Meios previstos:**
- Pix;
- Cartão;
- Boleto.

**Critério de aceite:**
- Dado que um pedido tenha sido criado;
- Quando o pagamento for processado;
- Então o pedido deve registrar o resultado da operação de pagamento.

**Conexão com Sistemas Operacionais:**
- Processos e serviços;
- Rede e I/O;
- Logs;
- Tratamento de falhas.

---

### RF06 — Controlar pedidos de produtos sob demanda

**Descrição:**  
Quando um produto não estiver disponível em estoque próprio, o sistema deve permitir o registro da necessidade de aquisição junto a fornecedor parceiro.

**Atores:** Equipe operacional, Fornecedor.

**Critério de aceite:**
- Dado que um produto não esteja disponível no estoque;
- Quando houver um pedido que dependa desse produto;
- Então a necessidade de aquisição deve ser registrada para acompanhamento operacional.

**Conexão com Sistemas Operacionais:**
- Processos;
- Serviços externos;
- Rede;
- Logs;
- Tratamento de indisponibilidade.

---

### RF07 — Atualizar status do pedido

**Descrição:**  
O sistema deve permitir acompanhar a evolução do pedido desde sua criação até a entrega.

**Possíveis estados:**
- Pedido criado;
- Pagamento pendente;
- Pagamento confirmado;
- Em preparação;
- Aguardando fornecedor;
- Em transporte;
- Entregue;
- Cancelado.

**Critério de aceite:**
- Dado que um pedido esteja registrado;
- Quando ocorrer uma mudança de etapa;
- Então o novo status deve ser persistido e disponibilizado para consulta.

**Conexão com Sistemas Operacionais:**
- Processos e serviços;
- Persistência;
- Logs;
- Observabilidade.

---

### RF08 — Registrar informações de entrega

**Descrição:**  
O sistema deve registrar as informações necessárias para o acompanhamento da entrega realizada por Correios ou transportadora parceira.

**Atores:** Equipe operacional, Transportadora/Correios.

**Critério de aceite:**
- Dado que um pedido esteja pronto para envio;
- Quando os dados de transporte forem registrados;
- Então as informações devem ficar associadas ao pedido.

**Conexão com Sistemas Operacionais:**
- Rede;
- I/O;
- Processos;
- Serviços externos;
- Logs.

---

### RF09 — Registrar eventos operacionais

**Descrição:**  
O sistema deve registrar eventos relevantes relacionados às operações de pedidos, pagamentos, estoque e serviços.

**Critério de aceite:**
- Dado que uma operação relevante seja executada;
- Quando a operação ocorrer;
- Então um registro do evento deve ser armazenado para consulta e análise.

**Conexão com Sistemas Operacionais:**
- Logs;
- Filesystem;
- Armazenamento;
- Observabilidade.

---

### RF10 — Monitorar serviços

**Descrição:**  
A solução deve permitir verificar a disponibilidade dos principais serviços utilizados pela operação.

**Critério de aceite:**
- Dado que os serviços estejam em execução;
- Quando forem realizados health checks;
- Então o estado de cada serviço deve poder ser identificado.

**Conexão com Sistemas Operacionais:**
- Processos;
- Serviços;
- Monitoramento;
- Health checks;
- Reinicialização.

---

### RF11 — Realizar backup

**Descrição:**  
A solução deve possuir uma estratégia para realizar cópias de segurança dos dados críticos.

**Critério de aceite:**
- Dado que existam dados operacionais importantes;
- Quando a rotina de backup for executada;
- Então uma cópia dos dados deve ser armazenada em local definido pela arquitetura.

**Conexão com Sistemas Operacionais:**
- Filesystem;
- Armazenamento;
- I/O;
- Backup;
- Recuperação.

---

### RF12 — Recuperar dados após falha

**Descrição:**  
A solução deve permitir a recuperação dos dados críticos a partir dos backups disponíveis.

**Critério de aceite:**
- Dado que ocorra uma falha que comprometa os dados;
- Quando o procedimento de recuperação for executado;
- Então os dados disponíveis no último backup válido devem poder ser restaurados.

**Conexão com Sistemas Operacionais:**
- Filesystem;
- Backup;
- Recuperação;
- Armazenamento.

---

## 3. Requisitos não funcionais

### RNF01 — Disponibilidade

A plataforma deve permanecer disponível durante a operação normal e possuir mecanismos para recuperação de serviços após falhas.

**Critério de aceite:**
- Serviços críticos devem possuir mecanismo de verificação de saúde;
- falhas devem ser identificáveis;
- deve existir estratégia de reinicialização ou recuperação.

**Conexão com Sistemas Operacionais:**
- Processos;
- Serviços;
- Restart;
- Monitoramento;
- Isolamento.

---

### RNF02 — Desempenho

A arquitetura deve ser capaz de suportar períodos de maior demanda sem degradação que impeça a realização das operações críticas.

**Critério de aceite:**
- CPU, memória e I/O devem ser considerados na análise;
- gargalos devem poder ser identificados por métricas ou evidências;
- recursos críticos devem possuir limites ou estratégias de controle quando necessário.

**Conexão com Sistemas Operacionais:**
- CPU;
- Memória;
- I/O;
- Processos;
- Limites de recursos.

---

### RNF03 — Segurança

O acesso aos recursos da aplicação e aos dados armazenados deve ser controlado de acordo com as responsabilidades de cada usuário ou serviço.

**Critério de aceite:**
- recursos devem possuir permissões adequadas;
- credenciais e segredos não devem ser armazenados diretamente no código;
- acessos relevantes devem ser registrados.

**Conexão com Sistemas Operacionais:**
- Usuários;
- Grupos;
- Permissões;
- Filesystem;
- Processos.

---

### RNF04 — Integridade dos dados

As operações de estoque, pedidos e pagamentos devem preservar a consistência dos dados mesmo diante de operações concorrentes ou falhas.

**Critério de aceite:**
- operações críticas devem possuir mecanismos para evitar inconsistências;
- falhas durante operações devem ser identificáveis;
- dados persistidos devem possuir estratégia de recuperação.

**Conexão com Sistemas Operacionais:**
- Processos;
- Concorrência;
- Sincronização;
- Armazenamento;
- Recuperação.

---

### RNF05 — Observabilidade

A solução deve permitir acompanhar o comportamento dos principais serviços e identificar falhas ou degradações.

**Critério de aceite:**
- eventos importantes devem gerar logs;
- serviços críticos devem possuir health checks;
- métricas relevantes devem poder ser acompanhadas;
- falhas importantes devem gerar alertas ou registros identificáveis.

**Conexão com Sistemas Operacionais:**
- Logs;
- Processos;
- Serviços;
- Monitoramento;
- Recursos do sistema.

---

### RNF06 — Recuperabilidade

Os dados e serviços críticos devem possuir mecanismos que permitam a recuperação após falhas.

**Critério de aceite:**
- deve existir uma estratégia de backup;
- os procedimentos de restauração devem ser documentados;
- os serviços devem possuir procedimentos de recuperação.

**Conexão com Sistemas Operacionais:**
- Filesystem;
- Backup;
- Armazenamento;
- Processos;
- Serviços.

---

### RNF07 — Isolamento

Os principais componentes da solução devem possuir isolamento suficiente para reduzir o impacto de uma falha em um componente sobre os demais.

**Critério de aceite:**
- componentes críticos devem possuir limites e separação de recursos quando aplicável;
- uma falha em um serviço não deve necessariamente interromper toda a solução;
- a estratégia de isolamento deverá ser detalhada na arquitetura.

**Conexão com Sistemas Operacionais:**
- Processos;
- Containers;
- Virtualização;
- Limites de recursos.

---

### RNF08 — Rastreabilidade

As operações críticas devem possuir registros que permitam identificar o que ocorreu, quando ocorreu e qual componente estava envolvido.

**Critério de aceite:**
- eventos críticos devem possuir data e hora;
- registros devem permitir relacionar eventos a pedidos ou operações;
- logs devem possuir política de armazenamento e retenção.

**Conexão com Sistemas Operacionais:**
- Logs;
- Filesystem;
- Processos;
- Observabilidade.

---

## 4. Requisitos de operação

Além dos requisitos funcionais e não funcionais, a arquitetura deverá considerar os procedimentos necessários para manter a solução funcionando.

### RO01 — Inicialização dos serviços

Deve existir um procedimento documentado para iniciar os componentes necessários à operação.

### RO02 — Monitoramento

Deve existir uma estratégia para acompanhar serviços, processos, recursos e eventos relevantes.

### RO03 — Tratamento de falhas

Deve existir um procedimento para identificar falhas e recuperar os componentes afetados.

### RO04 — Backup

Deve existir uma rotina definida para execução e verificação dos backups.

### RO05 — Recuperação

Deve existir um procedimento documentado para restaurar dados e serviços após falhas.

### RO06 — Gestão de armazenamento

A arquitetura deve considerar capacidade, crescimento, limites, limpeza e disponibilidade do armazenamento.

---

## 5. Resumo dos requisitos

| Código | Tipo | Requisito | Conceito de SO |
|---|---|---|---|
| RF01 | Funcional | Consultar catálogo | Arquivos e processos |
| RF02 | Funcional | Consultar estoque | Armazenamento e concorrência |
| RF03 | Funcional | Criar pedido | Processos e persistência |
| RF04 | Funcional | Controlar concorrência | Sincronização |
| RF05 | Funcional | Registrar pagamento | Rede, I/O e logs |
| RF06 | Funcional | Produtos sob demanda | Processos e serviços externos |
| RF07 | Funcional | Atualizar pedido | Processos e logs |
| RF08 | Funcional | Registrar entrega | Rede e I/O |
| RF09 | Funcional | Registrar eventos | Logs e filesystem |
| RF10 | Funcional | Monitorar serviços | Processos e serviços |
| RF11 | Funcional | Realizar backup | Filesystem e I/O |
| RF12 | Funcional | Recuperar dados | Backup e recuperação |
| RNF01 | Não funcional | Disponibilidade | Serviços e restart |
| RNF02 | Não funcional | Desempenho | CPU, memória e I/O |
| RNF03 | Não funcional | Segurança | Permissões e usuários |
| RNF04 | Não funcional | Integridade | Concorrência e armazenamento |
| RNF05 | Não funcional | Observabilidade | Logs e monitoramento |
| RNF06 | Não funcional | Recuperabilidade | Backup e filesystem |
| RNF07 | Não funcional | Isolamento | Containers e processos |
| RNF08 | Não funcional | Rastreabilidade | Logs e observabilidade |
| RO01 | Operação | Inicialização | Serviços |
| RO02 | Operação | Monitoramento | Observabilidade |
| RO03 | Operação | Tratamento de falhas | Processos e serviços |
| RO04 | Operação | Backup | Armazenamento |
| RO05 | Operação | Recuperação | Filesystem e backup |
| RO06 | Operação | Gestão de armazenamento | Filesystem e I/O |

---

## 6. Relação com os riscos do negócio

Os requisitos foram definidos considerando os principais riscos identificados no cenário da LudCommerce.

| Risco | Requisitos relacionados | Conceitos de SO |
|---|---|---|
| Indisponibilidade de fornecedor | RF06, RF07, RNF01 | Processos, serviços e rede |
| Venda simultânea da última unidade | RF02, RF03, RF04, RNF04 | Concorrência e sincronização |
| Sobrecarga em períodos de alta demanda | RNF01, RNF02, RNF05, RNF07 | CPU, memória, I/O e processos |
| Falha de aplicação ou banco | RF09, RF10, RNF01, RNF06 | Processos, serviços, logs e recuperação |
| Falha ou perda de armazenamento | RF09, RF11, RF12, RNF06 | Filesystem, I/O e backup |
| Acesso indevido a dados | RNF03, RNF08 | Usuários, grupos e permissões |

---

## 7. Próximas etapas

Os requisitos deste documento servirão de entrada para:

1. definição dos componentes da arquitetura;
2. identificação dos processos e serviços;
3. elaboração dos diagramas;
4. definição das decisões técnicas;
5. planejamento de observabilidade;
6. definição de estratégias de backup e recuperação;
7. criação de evidências práticas relacionadas aos conceitos de Sistemas Operacionais.