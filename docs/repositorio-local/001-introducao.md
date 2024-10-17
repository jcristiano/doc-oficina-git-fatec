---
id: repo-intro
title: Introdução
sidebar_position: 1
sidebar_label: Alinhamento
---


# O que é um Repositório Git?

Um **repositório Git** é um local onde os arquivos do projeto são armazenados, versionados e gerenciados. Ele permite que você acompanhe as mudanças feitas no código ao longo do tempo, facilitando o trabalho colaborativo, a recuperação de versões antigas e a resolução de conflitos. No Git, você pode ter tanto repositórios locais quanto remotos.

## Repositório Local

Um **repositório local** é a cópia do repositório Git armazenada diretamente na sua máquina. Quando você clona um repositório remoto, cria uma cópia completa no seu ambiente local, incluindo o histórico de commits e todas as ramificações. O repositório local é onde você faz as alterações, cria novos commits e prepara o código antes de enviar as alterações para o repositório remoto.

### Importância de um Repositório Local

O repositório local é essencial para o fluxo de trabalho com Git por vários motivos:

- **Desenvolvimento Desconectado**: Permite que você trabalhe e faça commits no seu projeto, mesmo sem conexão à internet. Todas as operações principais do Git (commits, branch, merges) são realizadas localmente.
  
- **Controle e Segurança**: Como você tem uma cópia completa do repositório, pode explorar o histórico de commits, testar novas funcionalidades em branches separadas e reverter mudanças sem afetar o código principal.

- **Performance**: As operações locais são extremamente rápidas, uma vez que não dependem de uma rede ou servidor externo. 

- **Preparação para o Repositório Remoto**: Antes de enviar as mudanças para um repositório remoto (como GitHub, GitLab ou Bitbucket), você pode organizar o histórico de commits, garantindo um código mais limpo e revisado.

Ter um repositório local faz parte da natureza distribuída do Git, onde cada desenvolvedor possui uma cópia integral do projeto, possibilitando um ambiente de trabalho colaborativo e seguro.
