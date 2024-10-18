---
id: git-essentials
title: Comandos Essenciais do Git
sidebar_position: 2
---

# Comandos Essenciais do Git

Se você é um estudante que acabou de entrar como estagiário em uma empresa de softwares, é fundamental familiarizar-se com o Git, uma das ferramentas de controle de versão mais populares. O Git permite que os desenvolvedores acompanhem as alterações no código, colaborem com outros e revertam para versões anteriores quando necessário. Abaixo estão alguns dos comandos mais importantes que você precisará.

## 1. Inicializar um Repositório

Para iniciar um novo repositório Git, você pode usar o comando:

```bash
git init
```

Este comando cria um novo repositório vazio em um diretório.

## 2. Clonar um Repositório Existente

Se você deseja obter uma cópia de um repositório remoto, pode usar:

```bash
git clone <url-do-repositorio>
```

Por exemplo:

```bash
git clone https://github.com/usuario/exemplo.git
```

## 3. Verificar o Status do Repositório

Para verificar quais arquivos foram alterados, adicionados ou removidos, você pode usar:

```bash
git status
```

## 4. Adicionar Alterações ao Staging

Após fazer alterações nos arquivos, você pode adicioná-los à área de staging com:

```bash
git add <arquivo>
```

Para adicionar todos os arquivos alterados, use:

```bash
git add .
```

## 5. Fazer um Commit

Depois de adicionar suas alterações ao staging, é hora de confirmar essas alterações com um commit:

```bash
git commit -m "Mensagem do commit"
```

Por exemplo:

```bash
git commit -m "Adiciona a função de login"
```

## 6. Ver o Histórico de Commits

Para ver o histórico de commits do seu repositório, utilize:

```bash
git log
```

## 7. Criar e Mudar para uma Nova Branch

Para criar uma nova branch e mudar para ela, use:

```bash
git checkout -b <nome-da-branch>
```

Por exemplo:

```bash
git checkout -b nova-feature
```

## 8. Mudar para uma Branch Existente

Se você deseja mudar para uma branch existente, utilize:

```bash
git checkout <nome-da-branch>
```

## 9. Mesclar Branches

Após finalizar as alterações em uma branch, você pode mesclá-la com a branch principal (geralmente `main` ou `master`):

```bash
git checkout main
git merge <nome-da-branch>
```

## 10. Enviar Alterações para o Repositório Remoto

Para enviar suas alterações locais para um repositório remoto, use:

```bash
git push origin <nome-da-branch>
```

Por exemplo:

```bash
git push origin main
```

## 11. Puxar Alterações do Repositório Remoto

Para obter as últimas alterações do repositório remoto, utilize:

```bash
git pull
```

## 12. Reverter Alterações

Se você precisa desfazer alterações não confirmadas, pode usar:

```bash
git checkout -- <arquivo>
```

Se você quiser reverter um commit, você pode usar:

```bash
git revert <hash-do-commit>
```

## Conclusão

Estes são alguns dos comandos Git mais importantes que você precisará ao iniciar seu estágio. Praticar esses comandos ajudará a desenvolver suas habilidades em controle de versão e a colaborar efetivamente com sua equipe.
