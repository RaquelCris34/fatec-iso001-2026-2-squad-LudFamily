# 03 - Arquitetura Técnica

## 1. Objetivo

A arquitetura da LudCommerce foi definida para sustentar as principais operações de um e-commerce de médio porte, considerando catálogo, estoque, pedidos, pagamentos, fornecedores e entregas.

A solução foi projetada de forma conceitual, sem representar uma implantação real em produção. O objetivo é demonstrar como os componentes poderiam ser organizados em um ambiente corporativo e como essa organização se relaciona com os conceitos de Sistemas Operacionais.

A arquitetura considera principalmente:

- execução da aplicação em servidor Linux;
- processamento das operações por uma aplicação Web/API;
- persistência dos dados em banco de dados;
- armazenamento separado para arquivos;
- integração com serviços externos;
- registro de logs e informações de operação;
- mecanismos de monitoramento, recuperação e controle de recursos.

---

## 2. Visão geral da solução

A LudCommerce possui três grupos principais de usuários:

- **Cliente:** consulta produtos, realiza pedidos e acompanha suas compras.
- **Administrador:** gerencia catálogo, estoque e configurações da plataforma.
- **Equipe Operacional:** acompanha pedidos, estoque, pagamentos, entregas e ocorrências.

A aplicação também se comunica com sistemas externos:

- serviço de pagamento;
- fornecedor parceiro;
- Correios ou transportadora.

A arquitetura foi organizada em camadas, permitindo separar o acesso dos usuários, o processamento da aplicação, a persistência dos dados e as integrações externas.

De forma simplificada, o fluxo principal é:

**Usuários → Proxy/Servidor Web → Aplicação Web/API → Banco de Dados e Armazenamento**

A aplicação também se comunica com os serviços externos necessários para pagamento, fornecimento e entrega.

Os diagramas detalhados da arquitetura estão disponíveis no diretório `diagrams/`:

- `diagrams/contexto.mmd`
- `diagrams/contexto.png`
- `diagrams/containers.mmd`
- `diagrams/containers.png`
- `diagrams/deployment.mmd`
- `diagrams/deployment.png`

---

## 3. Diagrama de contexto

O diagrama de contexto apresenta a LudCommerce como uma solução central que se relaciona com seus principais usuários e sistemas externos.

Os atores identificados são:

- Cliente;
- Administrador;
- Equipe Operacional;
- Fornecedor Parceiro;
- Serviço de Pagamento;
- Correios / Transportadora.

O cliente utiliza a plataforma para consultar produtos, realizar pedidos e acompanhar suas compras.

O administrador utiliza a plataforma para gerenciar catálogo, estoque e operações administrativas.

A equipe operacional utiliza a solução para acompanhar pedidos, estoque, pagamentos, entregas e ocorrências.

A LudCommerce também realiza integrações externas para:

- solicitar e receber informações de fornecedores;
- processar pagamentos;
- enviar e receber informações relacionadas às entregas.

O arquivo-fonte do diagrama está em:

`diagrams/contexto.mmd`

A representação visual exportada está em:

`diagrams/contexto.png`

---

## 4. Arquitetura de containers

A arquitetura de containers representa os principais componentes lógicos da solução.

Dentro da fronteira da LudCommerce estão:

- Aplicação Web / API;
- Banco de Dados;
- Armazenamento de Arquivos.

Os usuários acessam a Aplicação Web / API.

A aplicação é responsável por processar as operações de negócio e realizar as comunicações necessárias com os demais componentes.

A Aplicação Web / API possui comunicação com:

- Banco de Dados;
- Armazenamento de Arquivos;
- Serviço de Pagamento;
- Fornecedor Parceiro;
- Correios / Transportadora.

Embora a aplicação concentre diferentes responsabilidades de negócio, essas responsabilidades podem ser organizadas internamente em módulos ou serviços lógicos.

A opção por uma aplicação central reduz a complexidade inicial da infraestrutura e facilita sua administração.

O arquivo-fonte do diagrama está em:

`diagrams/containers.mmd`

A representação visual exportada está em:

`diagrams/containers.png`

---

## 5. Arquitetura de deployment

A arquitetura de deployment apresenta uma visão de como os componentes poderiam ser organizados em um ambiente computacional.

A solução considera um **servidor Linux** contendo:

- Proxy / Servidor Web;
- Aplicação Web / API;
- Banco de Dados;
- Armazenamento de Arquivos.

Os usuários acessam o Proxy / Servidor Web.

O proxy encaminha as requisições para a Aplicação Web / API.

A aplicação realiza as operações necessárias utilizando o Banco de Dados e o Armazenamento de Arquivos.

Também realiza comunicação com os sistemas externos:

- Serviço de Pagamento;
- Fornecedor Parceiro;
- Correios / Transportadora.

Essa representação é conceitual e não significa que a solução esteja implantada dessa forma em um ambiente real.

A finalidade é demonstrar a distribuição dos componentes e sua relação com o sistema operacional e os recursos computacionais.

O arquivo-fonte do diagrama está em:

`diagrams/deployment.mmd`

A representação visual exportada está em:

`diagrams/deployment.png`

---

## 6. Componentes da arquitetura

### 6.1 Cliente

Representa o usuário que acessa a plataforma para consultar produtos, realizar compras e acompanhar pedidos.

O cliente utiliza a aplicação por meio da camada de entrada disponibilizada pelo Proxy / Servidor Web.

O cliente não possui acesso direto ao Banco de Dados ou ao Armazenamento de Arquivos.

### 6.2 Administrador

Representa o usuário responsável pelas atividades administrativas da LudCommerce.

Entre suas principais atividades estão:

- gerenciamento do catálogo;
- atualização de informações dos produtos;
- acompanhamento do estoque;
- administração das operações da plataforma.

O administrador possui permissões diferentes das utilizadas por clientes comuns.

### 6.3 Equipe Operacional

Representa os usuários responsáveis pelo acompanhamento das operações da empresa.

A equipe operacional pode acompanhar:

- pedidos;
- disponibilidade de produtos;
- pagamentos;
- entregas;
- ocorrências;
- situações que necessitem de intervenção.

O acesso também deve respeitar as permissões definidas para o perfil operacional.

### 6.4 Proxy / Servidor Web

Representa a camada de entrada da infraestrutura.

Suas principais responsabilidades são:

- receber requisições dos usuários;
- encaminhar requisições para a aplicação;
- atuar como ponto de entrada da solução;
- contribuir para o controle de acesso;
- apoiar mecanismos de segurança e observabilidade.

O proxy é executado no servidor Linux utilizado pela solução.

### 6.5 Aplicação Web / API

É o principal componente de processamento da LudCommerce.

A aplicação concentra as regras necessárias para as principais operações do negócio:

- catálogo;
- consulta de estoque;
- criação de pedidos;
- reserva de estoque;
- processamento do fluxo de pagamento;
- comunicação com fornecedores;
- comunicação com serviços de entrega;
- acompanhamento operacional.

Essas responsabilidades estão representadas dentro de um único componente de aplicação.

Internamente, elas podem ser organizadas em módulos ou serviços lógicos, sem que isso implique necessariamente em processos ou servidores independentes.

Essa decisão reduz a complexidade operacional inicial da solução.

### 6.6 Banco de Dados

O Banco de Dados é responsável pela persistência das informações estruturadas da plataforma.

Entre os dados armazenados estão:

- produtos;
- clientes;
- estoque;
- pedidos;
- itens dos pedidos;
- informações relacionadas aos pagamentos;
- informações relacionadas às entregas;
- registros necessários para controle das operações.

O banco é um componente crítico da arquitetura.

Sua indisponibilidade pode impedir consultas, criação de pedidos, atualização de estoque e outras operações fundamentais.

### 6.7 Armazenamento de Arquivos

Representa o espaço destinado aos arquivos utilizados pela plataforma.

O Armazenamento de Arquivos é mantido separado do Banco de Dados.

Essa separação facilita:

- organização dos dados;
- controle de permissões;
- gerenciamento do espaço disponível;
- realização de backups;
- recuperação dos arquivos.

O sistema operacional é responsável por disponibilizar o sistema de arquivos utilizado por esse componente.

### 6.8 Logs

Os eventos relevantes da aplicação e da operação devem ser registrados em logs.

Os registros podem ser utilizados para:

- identificar falhas;
- investigar ocorrências;
- acompanhar operações;
- auxiliar no diagnóstico;
- fornecer evidências de execução.

Os logs também precisam ser administrados para evitar crescimento excessivo dos arquivos e consumo indevido de armazenamento.

---

## 7. Processos e serviços

A arquitetura considera processos e serviços necessários para o funcionamento da LudCommerce.

### 7.1 Processo da aplicação

O processo da aplicação executa as regras de negócio e recebe as requisições encaminhadas pelo proxy.

Esse processo utiliza recursos do sistema operacional, principalmente:

- CPU;
- memória;
- armazenamento;
- rede.

Em períodos de alta demanda, o aumento da quantidade de requisições pode elevar o consumo desses recursos.

### 7.2 Processo do Proxy / Servidor Web

O proxy recebe as conexões externas e encaminha as requisições para a aplicação.

Sua utilização como camada de entrada permite separar o recebimento das requisições do processamento das regras de negócio.

Esse processo também representa um ponto importante para observação de disponibilidade e falhas de comunicação.

### 7.3 Serviço de Banco de Dados

O Banco de Dados funciona como serviço responsável pela persistência das informações estruturadas.

Seu funcionamento depende de processos que utilizam:

- CPU;
- memória;
- armazenamento;
- operações de entrada e saída.

Uma sobrecarga do banco pode aumentar o tempo de resposta da aplicação.

### 7.4 Serviço de armazenamento

O armazenamento de arquivos representa um recurso utilizado pelos processos da aplicação.

As operações de leitura e gravação dependem do sistema de arquivos e dos dispositivos de armazenamento disponibilizados pelo sistema operacional.

O espaço disponível deve ser acompanhado para evitar falhas de gravação.

### 7.5 Logs e monitoramento

Os mecanismos de logs e monitoramento acompanham o funcionamento da solução.

Devem permitir observar:

- disponibilidade dos serviços;
- consumo de CPU;
- consumo de memória;
- utilização do armazenamento;
- falhas de processos;
- falhas de comunicação;
- eventos importantes da aplicação.

### 7.6 Serviços externos

A aplicação depende de serviços externos para:

- processamento de pagamentos;
- confirmação ou consulta de disponibilidade junto a fornecedores;
- informações relacionadas à entrega.

Esses serviços não fazem parte da infraestrutura interna da LudCommerce.

Portanto, a aplicação precisa considerar a possibilidade de indisponibilidade, atraso ou falha de comunicação.

---

## 8. Fluxo de uma operação de compra

Um fluxo simplificado de compra pode ocorrer da seguinte maneira:

1. O cliente acessa a plataforma.
2. O Proxy / Servidor Web recebe a requisição.
3. A requisição é encaminhada para a Aplicação Web / API.
4. A aplicação consulta o Banco de Dados para obter as informações do produto.
5. A aplicação consulta a disponibilidade do estoque.
6. O pedido é criado conforme as regras da operação.
7. O estoque é reservado de acordo com as regras definidas.
8. A aplicação solicita o processamento do pagamento ao serviço externo.
9. O resultado do pagamento é recebido pela aplicação.
10. Quando necessário, a aplicação consulta ou solicita informações ao fornecedor parceiro.
11. A aplicação envia as informações necessárias ao serviço de entrega.
12. Os eventos relevantes são registrados nos logs.
13. A equipe operacional pode acompanhar o pedido pela plataforma.
14. O cliente recebe as informações relacionadas ao andamento do pedido.

Esse fluxo demonstra a dependência entre processos internos, Banco de Dados, Armazenamento de Arquivos, rede e serviços externos.

---

## 9. Dependências da solução

A operação da LudCommerce possui dependências internas e externas.

### 9.1 Dependências internas

Os principais elementos internos são:

- servidor Linux;
- Proxy / Servidor Web;
- Aplicação Web / API;
- Banco de Dados;
- Armazenamento de Arquivos;
- sistema de arquivos;
- CPU;
- memória;
- armazenamento;
- rede;
- mecanismos de logs;
- mecanismos de monitoramento.

### 9.2 Dependências externas

Os principais sistemas externos são:

- Serviço de Pagamento;
- Fornecedor Parceiro;
- Correios ou Transportadora.

Essas dependências estão fora do controle direto da infraestrutura da LudCommerce.

Uma indisponibilidade externa pode impedir ou atrasar determinada etapa do processamento de um pedido.

---

## 10. Relação com Sistemas Operacionais

A arquitetura foi definida considerando diretamente os recursos e responsabilidades do sistema operacional.

### 10.1 Processos

A aplicação, o proxy e o Banco de Dados são executados como processos ou serviços no servidor Linux.

Uma falha em um processo pode afetar uma parte específica ou, dependendo do componente, várias operações da plataforma.

O acompanhamento dos processos permite identificar situações como:

- processo encerrado;
- processo travado;
- consumo elevado de CPU;
- consumo elevado de memória;
- reinicializações inesperadas.

### 10.2 CPU

As operações da LudCommerce utilizam processamento de CPU.

Entre as atividades que podem gerar consumo estão:

- consultas;
- processamento de pedidos;
- atualização de estoque;
- processamento de informações;
- geração de logs;
- comunicação com serviços externos.

Em períodos de alta demanda, o aumento das requisições pode elevar a utilização do processador.

O monitoramento da CPU é necessário para identificar possíveis gargalos.

### 10.3 Memória

A aplicação e os demais serviços utilizam memória durante sua execução.

O consumo excessivo de memória pode provocar:

- degradação do desempenho;
- lentidão;
- encerramento de processos;
- instabilidade;
- indisponibilidade da aplicação.

Por esse motivo, a utilização de memória deve ser monitorada e considerada nas decisões de operação.

### 10.4 Sistema de arquivos

O sistema de arquivos é utilizado para armazenar:

- arquivos da aplicação;
- arquivos utilizados pela plataforma;
- logs;
- arquivos relacionados a backup.

O sistema operacional controla o acesso aos arquivos por meio de usuários, grupos e permissões.

O espaço disponível também deve ser monitorado.

### 10.5 Permissões

Os recursos do servidor devem possuir permissões adequadas para impedir acessos indevidos.

Os processos devem possuir somente os privilégios necessários para realizar suas funções.

A aplicação, o banco, os arquivos e os logs devem ser protegidos contra alterações ou acessos não autorizados.

A arquitetura considera o princípio de menor privilégio como uma regra básica de segurança.

### 10.6 Entrada e saída

A arquitetura utiliza operações de entrada e saída principalmente para:

- leitura e gravação no Banco de Dados;
- leitura e gravação de arquivos;
- registro de logs;
- comunicação pela rede.

Essas operações podem se tornar pontos de gargalo em períodos de alta utilização.

Por exemplo, uma grande quantidade de operações de gravação pode aumentar a utilização do armazenamento e afetar o tempo de resposta.

### 10.7 Rede

A comunicação entre clientes, proxy, aplicação e serviços externos depende da infraestrutura de rede.

Falhas ou lentidão na comunicação podem afetar:

- processamento de pagamentos;
- consulta a fornecedores;
- atualização de informações de entrega;
- acesso dos usuários à plataforma.

Por isso, falhas de rede devem ser consideradas na operação e no diagnóstico de incidentes.

---

## 11. Segurança

A arquitetura considera controles básicos de segurança relacionados ao ambiente operacional.

Entre eles:

- autenticação dos usuários;
- diferenciação de perfis;
- controle de permissões;
- princípio de menor privilégio;
- proteção de informações sensíveis;
- não armazenamento de segredos diretamente no código;
- registro de acessos e eventos relevantes;
- separação entre componentes internos e serviços externos.

Os diferentes perfis de usuário devem possuir somente os acessos necessários para suas atividades.

O administrador, a equipe operacional e o cliente não devem possuir os mesmos privilégios.

O controle de permissões também deve ser aplicado aos recursos do servidor, incluindo arquivos, diretórios, logs e demais recursos utilizados pela aplicação.

---

## 12. Observabilidade

A operação da LudCommerce precisa permitir identificar problemas antes que eles provoquem impactos maiores.

Os principais mecanismos considerados são:

- logs da aplicação;
- logs do servidor;
- monitoramento de CPU;
- monitoramento de memória;
- monitoramento de armazenamento;
- monitoramento dos processos;
- monitoramento da disponibilidade dos serviços;
- health checks;
- alertas para situações críticas.

A observabilidade permite relacionar problemas de negócio com eventos técnicos.

Por exemplo, um aumento no tempo de resposta de pedidos pode estar relacionado a:

- aumento do uso de CPU;
- falta de memória;
- alto uso de I/O;
- problemas no Banco de Dados;
- indisponibilidade de serviço externo.

Os registros devem conter informações suficientes para auxiliar na investigação dos problemas.

---

## 13. Disponibilidade e recuperação

A arquitetura considera mecanismos para manter ou recuperar a operação após falhas.

Entre as estratégias consideradas estão:

- health checks;
- monitoramento dos processos;
- reinício de processos ou serviços quando necessário;
- monitoramento de recursos;
- backup dos dados importantes;
- procedimentos de restauração;
- controle do espaço de armazenamento;
- identificação de dependências externas indisponíveis.

A recuperação não depende somente da aplicação.

Ela também envolve:

- sistema operacional;
- processos;
- Banco de Dados;
- sistema de arquivos;
- armazenamento;
- rede;
- serviços externos.

A estratégia de backup deve considerar principalmente o Banco de Dados e os arquivos necessários para a operação da plataforma.

---

## 14. Riscos operacionais

Os principais riscos identificados para a arquitetura são:

| Risco | Impacto | Relação com Sistemas Operacionais |
|---|---|---|
| Indisponibilidade de fornecedor | O pedido pode não ser atendido conforme planejado | Processos e rede |
| Compra simultânea da última unidade | Pode ocorrer inconsistência de estoque | Processos, concorrência e persistência |
| Alta demanda | Pode provocar lentidão ou indisponibilidade | CPU, memória e I/O |
| Falha da aplicação | Pode interromper diversas operações | Processos e serviços |
| Falha do Banco de Dados | Pode impedir acesso aos dados operacionais | Processos, memória e armazenamento |
| Falha no armazenamento | Pode impedir gravação ou acesso a arquivos | Filesystem e I/O |
| Falta de espaço para logs | Pode impedir novas gravações e prejudicar diagnóstico | Filesystem e armazenamento |
| Acesso não autorizado | Pode comprometer dados e operações | Usuários e permissões |
| Falha de serviço externo | Pode afetar pagamento, fornecimento ou entrega | Rede e I/O |

---

## 15. Pontos críticos da arquitetura

Os principais pontos que exigem atenção operacional são:

### 15.1 Aplicação

A aplicação é o principal ponto de processamento da solução.

Uma falha pode afetar diversas funcionalidades simultaneamente.

Por isso, seu processo deve ser monitorado e possuir procedimentos de reinício e recuperação.

### 15.2 Banco de Dados

O Banco de Dados é crítico para a persistência das informações de pedidos, estoque e demais dados da operação.

Problemas no banco podem impedir consultas e atualizações importantes.

### 15.3 Armazenamento

A falta de espaço pode impedir novas gravações e afetar arquivos e logs.

O armazenamento deve ser monitorado para permitir ação preventiva.

### 15.4 Recursos do servidor

CPU, memória e I/O podem se tornar gargalos durante períodos de alta demanda.

O acompanhamento desses recursos permite identificar situações de degradação antes que provoquem indisponibilidade.

### 15.5 Serviços externos

Pagamento, fornecedor e entrega dependem de sistemas externos.

Esses sistemas podem apresentar:

- indisponibilidade;
- lentidão;
- falhas de comunicação;
- respostas inesperadas.

A arquitetura precisa considerar esses cenários no tratamento das operações.

---

## 16. Estratégia de evolução

A arquitetura inicial foi mantida relativamente simples para reduzir a complexidade operacional.

Caso a LudCommerce cresça ou os requisitos mudem, componentes específicos poderão ser separados conforme a necessidade.

Possíveis evoluções incluem:

- separação de serviços;
- utilização de containers;
- isolamento de recursos;
- distribuição de carga;
- expansão do armazenamento;
- mecanismos adicionais de monitoramento;
- estratégias mais avançadas de disponibilidade;
- definição de limites de recursos para processos.

Essas evoluções devem ser justificadas a partir de novos requisitos, riscos ou gargalos identificados.

A adoção de containers ou outras formas de isolamento, por exemplo, pode ser avaliada posteriormente para separar componentes e controlar melhor seus recursos.

---

## 17. Conclusão

A arquitetura da LudCommerce organiza os principais componentes necessários para sustentar um e-commerce de médio porte.

A solução considera:

- usuários;
- aplicação;
- proxy;
- Banco de Dados;
- armazenamento;
- logs;
- serviços externos;
- processos;
- recursos computacionais;
- rede;
- segurança;
- observabilidade;
- disponibilidade;
- backup e recuperação.

A arquitetura também estabelece uma relação direta entre o problema de negócio e os conceitos de Sistemas Operacionais.

Os principais conceitos envolvidos são:

- processos;
- CPU;
- memória;
- sistema de arquivos;
- permissões;
- entrada e saída;
- rede;
- logs;
- observabilidade;
- disponibilidade;
- backup;
- recuperação.

Dessa forma, a arquitetura não representa apenas a estrutura lógica da aplicação, mas também os recursos operacionais necessários para manter a plataforma funcionando de maneira consistente, observável e recuperável.