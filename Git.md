# 📘 Manual de Fluxo Git: Feature Branch Workflow

Este documento cobre o ciclo de vida de uma tarefa, desde a criação até a entrega em produção, e como resolver problemas comuns.

> **Regra de Ouro**
> **Nunca faça merge de `qa` para `main`**.
> 
>As branches `qa` e `dev` são apenas **ambientes** de teste descartáveis.

---
## Sumário
  - [PARTE 1: Fluxo Padrão](#parte-1-fluxo-padrão)
    - [Fase 1: Início e Desenvolvimento](#fase-1-início-e-desenvolvimento)
    - [Fase 2: Homologação (Enviando para QA)](#fase-2-homologação-enviando-para-qa)
    - [Fase 3: Aprovação e Produção (Main)](#fase-3-aprovação-e-produção-main)
    - [Fase 4: Limpeza Local](#fase-4-limpeza-local)
  - [PARTE 2: Solução de Problemas e Manutenção](#parte-2-solução-de-problemas-e-manutenção)
    - [**Cenario A:** Usuário encontrou um BUG no QA](#cenario-a-usuário-encontrou-um-bug-no-qa)
    - [**Cenario B:** Erro de código e conflitos na branch QA](#cenario-b-erro-de-código-e-conflitos-na-branch-qa)
    - [**Cenario C:** O Servidor de QA "quebrou" ou não atualizou](#cenario-c-o-servidor-de-qa-quebrou-ou-não-atualizou)
    - [**Cenario D:** Manutenção Periódica (Opcional)](#cenario-d-manutenção-periódica-opcional)
    - [**Cenario E:** Hotfix](#cenario-e-hotfix)
    - [**Cenario F:** Limpar Branchs](#cenario-f-limpar-branchs)
---

## PARTE 1: Fluxo Padrão

Use este passo a passo quando for iniciar uma nova tarefa.

### Fase 1: Início e Desenvolvimento
**Objetivo:** Criar um ambiente isolado para trabalhar.

1. **Vá para a base segura (Main):**
   ```bash
   git checkout main
   git pull origin main
2. **Crie a branch da tarefa: Use um padrão de nome (ex: feature/numero-nome).**
   ```bash
   git checkout -b feature/
3. **Desenvolva e Salve: Codifique e teste na sua máquina, depois salve o progresso.**
   ```bash
   git add .
   git commit -m "feat: descricao do que foi feito"
4. **Envie a branch para o GitHub: Isso garante que a branch apareça lá para criar o PR**
   ```bash
   git push origin feature/
### Fase 2: Homologação (Enviando para QA)
**Objetivo:** Colocar seu código no servidor de QA para o usuário testar, sem "sujar" sua branch original.

1. **Garanta que sua feature está atualizada:**
   ```bash
    git checkout feature/99-nova-funcionalidade
    # Se a main mudou enquanto você trabalhava, traga as novidades (opcional, mas recomendado)
    git pull origin main
2. **Vá para o ambiente QA e junte seu código:**
   ```bash
    git checkout qa
    git pull origin qa  # Garante que seu QA local está igual ao remoto
    git merge feature/

    #Nota: Se abrir um editor de texto (Vim), digite :wq e pressione Enter.
3. **Envie para o Servidor:**
   ```bash
    git push origin qa
4. **Avisar Usuário: "A tarefa está disponível em QA para testes.**
### Fase 3: Aprovação e Produção (Main)
**Objetivo:** O usuário aprovou. Hora de oficializar.

1. **Crie o Pull Request (PR):**
    - Vá ao GitHub (site).
    - Clique em "New Pull Request".
    - Base: main | Compare: feature/99-nova-funcionalidade.
    - Revise os arquivos e crie o PR.
    - Faça o Merge Pull Request.
### Fase 4: Limpeza Local
**Objetivo:** Organizar a casa para a próxima tarefa.

1. **Atualize sua Main local:**
    ```bash
    git checkout main
    git pull origin main
2. **Delete a branch da feature (ela já está na main):**
    ```bash
    git branch -D feature/
3. **Apagar as Branchs já mergeadas:**
    ```bash
    git fetch --prune
---

## PARTE 2: Solução de Problemas e Manutenção

Use esta seção quando algo der errado ou para "resetar" os ambientes.<br>
### **Cenario A:** Usuário encontrou um BUG no QA<br>
O que fazer: Nunca corrija direto na branch qa.
1. **Volte para sua branch de trabalho:**
    ```bash
    git checkout feature/99-nova-funcionalidade
2. **Corrija o código.**
3. **Faça o commit:**
    ```bash
    git commit -m "fix: correcao do bug tal"
4. **Repita a Fase 2 (Merge para QA e Push) para atualizar o servidor de testes.**
<br><br>

### **Cenario B:** Erro de código e conflitos na branch QA<br>
**Sintoma:** Ao fazer merge em QA, aparecem erros de código duplicado ou conflitos de arquivo. A branch QA está "poluída".<br>
**Ação:** Resetar a branch QA para ser uma cópia limpa da Main.
1. **Resete o QA na sua máquina:**
    ```bash
    git checkout qa
    git fetch origin
    git reset --hard origin/main
2. **Reaplique sua feature (opcional, se você estava testando algo):**
    ```bash
    git merge feature/99-nova-funcionalidade
3. **Force a atualização no GitHub:**
    ```bash
    git push origin qa --force
<br><br>

### **Cenario C:** O Servidor de QA "quebrou" ou não atualizou<br>
**Sintoma:** Você fez tudo certo na sua máquina, deu git push origin qa, mas ao acessar o site de QA, o erro persiste.<br>
**Causa:** O servidor físico onde o site roda não conseguiu sincronizar com o GitHub (possivelmente por causa de um force push anterior).<br>
**Ação:** Você precisa acessar o terminal do SERVIDOR (via SSH/Putty) e rodar os comandos lá dentro.
1. **Acesse a pasta do projeto no servidor.**
2. **Baixe as informações (sem aplicar):**
    ```bash
    git fetch origin
3. **Force o servidor a aceitar a versão do GitHub:**
    ```bash
    git reset --hard origin/qa
Isso apaga qualquer alteração manual feita direto no servidor e sincroniza com o repositório.
<br><br>

### **Cenario D:** Manutenção Periódica (Opcional)<br>
**Quando fazer:** Uma vez por semana ou após grandes entregas, para garantir que dev e qa não fiquem muito defasados da main. Cuidado: Só faça isso se ninguém estiver testando nada importante no momento.
1. **Resetar DEV:**
    ```bash
    git checkout dev
    git reset --hard origin/main
    git push origin dev --force
2. **Baixe as informações (sem aplicar):**
    ```bash
    git checkout qa
    git reset --hard origin/main
    git push origin qa --force
<br><br>

### **Cenario E:** Hotfix<br>
**Quando fazer:** Quando houver um problema crítico em produção que precisa ser resolvido com urgência.
1. **Criar a branch a partir da main:**
    ```bash
    git checkout main
    git pull origin main
    git checkout -b hotfix/
2. **Fazer o ajuste → commit → push:**
    ```bash
    git add .
    git commit -m "fix: descricao-do-erro. closes #"
    git push origin hotfix/
3. **Criar PR para main:**<br>
No GitHub:
    - Base: `main`.
    - Compare: `hotfix/descricao-do-erro`.
4. **Após PR → no ambiente de Produção:**<br>
execute:
    ```bash
    git fetch origin
    git reset --hard origin/main
5. **Na sua Máquina atualize sua Main local:**
    ```bash
    git checkout main
    git pull origin main
6. **Delete a branch da feature (ela já está na main):**
    ```bash
    git branch -D feature/99-nova-funcionalidade
<br>

**Somente execute o trecho OPCIONAL caso não tenha desenvolvimentos inacabados em DEV e/ou QA:**<br>

7. **Resetar DEV (OPCIONAL):**
    ```bash
    git checkout dev
    git reset --hard origin/main
    git push origin dev --force
8. **Resetar QA (OPCIONAL):**
    ```bash
    git checkout qa
    git reset --hard origin/main
    git push origin qa --force

<br><br>

### **Cenario F:** Limpar Branchs<br>
**Quando fazer:** Quando fazer o merge da branch para main.
1. **Listar as branchs:**
    ```bash
    git branch -a
2. **Apagar as Branchs já mergeadas:**
    ```bash
    git fetch --prune
