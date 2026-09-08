# 01 - Cenário de Negócio

## 1. Visão geral

A LudCommerce é uma empresa de médio porte que atua no comércio eletrônico de produtos de informática. A plataforma comercializa diferentes tipos de hardware e periféricos, atendendo tanto consumidores quanto empresas.

O modelo de negócio é baseado em vendas online. O cliente consulta o catálogo, seleciona os produtos, adiciona os itens ao carrinho, escolhe a forma de pagamento e acompanha o pedido até a entrega.

A LudCommerce trabalha com estoque próprio para produtos disponíveis e também realiza compras sob demanda junto a fornecedores parceiros quando determinado produto não está disponível internamente.

## 2. Problema de negócio

A LudCommerce precisa garantir que as operações de catálogo, estoque, pedidos, vendas e conciliação sejam realizadas de maneira consistente e que a plataforma permaneça disponível mesmo durante períodos de alta demanda ou diante de falhas de processos e serviços.

Um dos principais riscos ocorre quando diferentes clientes tentam comprar simultaneamente um produto com disponibilidade limitada. O sistema precisa evitar que uma mesma unidade seja vendida para mais de um cliente e garantir que as informações do pedido e do estoque permaneçam consistentes.

Outro risco está relacionado à dependência de serviços externos, como fornecedores, meios de pagamento e serviços de entrega. Uma indisponibilidade ou falha de comunicação pode interromper uma operação de venda e precisa ser tratada de maneira adequada.

A plataforma também precisa lidar com períodos de maior volume de acessos, nos quais o aumento da quantidade de processos e operações pode provocar consumo elevado de CPU, memória, armazenamento e recursos de entrada e saída.

## 3. Impacto do problema

Falhas nas operações podem provocar:

- venda de produtos sem disponibilidade;
- inconsistência entre pedidos e estoque;
- interrupção ou atraso no processamento de pedidos;
- indisponibilidade da plataforma;
- perda ou dificuldade de recuperação de informações;
- dificuldade para identificar a causa de falhas;
- problemas na conciliação das vendas e pagamentos;
- prejuízos financeiros e insatisfação dos clientes.

Por esse motivo, a solução deve considerar não apenas as funcionalidades do e-commerce, mas também os mecanismos necessários para garantir disponibilidade, integridade, segurança, observabilidade e recuperação das operações.

## 4. Atores

### Cliente

Pessoa física ou empresa que utiliza a LudCommerce para consultar produtos, realizar compras, efetuar pagamentos e acompanhar pedidos.

### Administrador

Responsável pela administração da plataforma, incluindo gerenciamento de produtos, informações de estoque, usuários e acompanhamento das operações.

### Equipe operacional

Responsável pelo acompanhamento dos pedidos, relacionamento com fornecedores e preparação das operações de expedição.

### Fornecedor

Empresa parceira responsável pelo fornecimento de produtos adquiridos sob demanda pela LudCommerce.

### Serviço de pagamento

Sistema externo responsável pelo processamento e retorno do status de pagamentos realizados por Pix, cartão ou boleto.

### Transportadora ou Correios

Serviço externo responsável pela etapa de entrega dos produtos aos clientes.

## 5. Principais operações do negócio

As principais operações consideradas no projeto são:

1. Cadastro e manutenção dos produtos.
2. Consulta do catálogo.
3. Adição de produtos ao carrinho.
4. Criação de pedidos.
5. Processamento do pagamento.
6. Verificação e atualização do estoque.
7. Solicitação de produtos a fornecedores quando necessário.
8. Preparação e expedição dos pedidos.
9. Envio por transportadora ou Correios.
10. Acompanhamento do pedido.
11. Conciliação das vendas e pagamentos.
12. Registro e consulta de informações operacionais.

## 6. Formas de pagamento

A LudCommerce disponibiliza três formas de pagamento:

- Pix;
- cartão;
- boleto.

O processamento do pagamento é considerado uma integração com serviço externo. O sistema deve registrar o estado da operação e tratar situações em que o serviço externo esteja indisponível ou não responda adequadamente.

## 7. Entrega

A LudCommerce não possui uma frota própria. As entregas são realizadas por transportadoras parceiras ou pelos Correios.

A integração com esses serviços será considerada parte do cenário arquitetural, mas não será necessário implementar uma integração real para o projeto da disciplina.

## 8. Modelo de estoque

A LudCommerce utiliza dois cenários de disponibilidade:

### Estoque disponível

Produtos que já estão disponíveis para venda e podem ser separados para atendimento dos pedidos.

### Compra sob demanda

Produtos que não estão disponíveis internamente podem ser adquiridos junto a fornecedores parceiros após a realização do pedido, conforme as condições de fornecimento.

Essa característica cria uma dependência entre o processamento do pedido e a disponibilidade dos fornecedores.

## 9. Premissas

Para o desenvolvimento do projeto, serão consideradas as seguintes premissas:

- A LudCommerce é uma empresa de médio porte.
- A plataforma atende pessoas físicas e empresas.
- A empresa comercializa produtos de informática e hardware.
- O modelo de negócio é de e-commerce tradicional.
- A plataforma possui catálogo de produtos.
- A plataforma precisa controlar pedidos e disponibilidade de produtos.
- A empresa utiliza fornecedores parceiros para aquisição sob demanda.
- Os pagamentos podem ser realizados por Pix, cartão ou boleto.
- As entregas são realizadas por transportadoras parceiras ou pelos Correios.
- Serviços de pagamento, fornecedores e entrega são considerados sistemas externos.
- A arquitetura deve considerar disponibilidade, segurança, armazenamento, logs, backup, monitoramento e recuperação.
- A implementação completa de uma aplicação comercial não faz parte do escopo obrigatório do projeto.

## 10. Relação com Sistemas Operacionais

O funcionamento da LudCommerce depende de recursos e mecanismos fornecidos pelo Sistema Operacional.

Entre os principais pontos que serão analisados ao longo do projeto estão:

- gerenciamento de processos e serviços;
- concorrência entre operações de venda;
- utilização de CPU e memória;
- entrada e saída de dados;
- armazenamento e filesystem;
- permissões de acesso;
- geração e armazenamento de logs;
- monitoramento e observabilidade;
- backup e recuperação;
- isolamento e virtualização por containers;
- disponibilidade e reinicialização de serviços.

Esses aspectos serão aprofundados nas etapas seguintes do projeto, relacionando os riscos do negócio às decisões técnicas da arquitetura.