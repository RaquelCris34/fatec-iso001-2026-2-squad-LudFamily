# Aula 03 - Reflexão individual

## 1. Ambiente

Kernel observado: 6.8.0-1052-azure

Memória disponível: 5.4 GiB

Uma informação que me chamou atenção: o ambiente utiliza Ubuntu 24.04.4 LTS sobre um kernel Linux executando em uma infraestrutura Azure. Também foi possível observar que o Codespace disponibiliza informações sobre memória, disco e processos por meio de comandos do próprio sistema operacional.

## 2. Processo

PID observado: 144720

PPID observado: 1063

Explique com suas palavras a diferença entre programa e processo: um programa é um conjunto de instruções armazenado em um arquivo. Quando esse programa é executado, o sistema operacional cria uma instância em execução, chamada processo. No laboratório, o comando `sleep 180` representou o programa sendo executado como um processo identificado pelo PID 144720. O processo também possui um PPID, que identifica seu processo pai.

## 3. Proteção

Quem negou a leitura do arquivo e por quê? O sistema operacional, por meio do kernel, negou a leitura porque o arquivo `segredo.txt` estava configurado com permissão `000`. Dessa forma, o usuário não possuía permissão para ler o arquivo. O comando `chmod 600` foi utilizado posteriormente para restaurar a permissão de leitura e escrita para o proprietário.

## 4. Projeto da squad

Escolha UM componente do projeto (API, banco, worker, storage, etc.).

Esse componente rodaria como quê? A Aplicação Web / API rodaria como um processo ou serviço no servidor Linux.

Se ele falhar, qual impacto de negócio aparece? Se a aplicação ficar indisponível, os clientes podem não conseguir consultar produtos, realizar pedidos ou acompanhar suas operações. Isso pode interromper vendas e afetar o controle de estoque.

Qual controle deveria existir? Deveriam existir logs, healthcheck e mecanismo de restart para identificar falhas, acompanhar o funcionamento do serviço e permitir sua recuperação.
