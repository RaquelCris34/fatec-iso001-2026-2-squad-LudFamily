# Aula 03 Reflexão individual

## 1. Ambiente
Kernel observado: 6.6.137+
Memória disponível: 7.7Gi (6.8Gi disponível)
Uma informação que me chamou atenção: A facilidade de consultar dados do SO diretamente no terminal.

## 2. Processo
PID observado: 9853
PPID observado: 9812
Explique com suas palavras a diferença entre programa e processo: Programa é o arquivo/código estático no disco; processo é o programa em execução na memória.

## 3. Proteção
Quem negou a leitura do arquivo e por quê? O Kernel do Sistema Operacional negou o acesso porque as permissões do arquivo foram alteradas para 000 (nenhum direito de leitura).

## 4. Projeto da squad
Escolha UM componente do projeto (API, banco, worker, storage, etc.).
Esse componente rodaria como quê? processo
Se ele falhar, qual impacto de negócio aparece? A aplicação fica indisponível para os usuários finais.
Qual controle deveria existir? Sistema de restart automático e logs de monitoramento.