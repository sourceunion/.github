# Como Contribuir

Este é um grupo para aprendizado, e a colaboração é a parte mais importante. Para mantermos o projeto organizado e garantirmos que todos possam contribuir de forma eficaz, seguimos um fluxo de trabalho específico, padrão em projetos de código aberto.

## Fluxo de Trabalho

Usamos o modelo **Fork & Pull Request**. Isso significa que ninguém envia código diretamente para o repositório principal. Em vez disso, cada contribuidor trabalha em uma cópia pessoal (um **fork**) e propõe suas mudanças através de um **Pull Request (PR)**.

### Passo 1: Escolha uma Tarefa

Encontre uma tarefa para trabalhar na seção de **Issues** de um dos nossos repositórios no GitHub.

> **Importante:** Antes de começar, verifique se ninguém mais está trabalhando na mesma tarefa. Se for uma **Issue**, atribua a si mesmo (**assign yourself**). Isso evita trabalho duplicado.

### Passo 2: Fork, Clone e Configure os Remotos

![](https://docs.github.com/assets/cb-34352/mw-1440/images/help/repository/fork-button.webp)


Primeiro, [você precisa criar uma cópia do projeto na sua conta do GitHub](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo) (um **fork**) e configurar seu ambiente local.

```bash
### 1. FAÇA O FORK
#
# Vá até a página do repositório principal no GitHub e clique no botão "Fork".

### 2. CLONE O SEU FORK
# 
# 2.1. Clone a sua cópia para a sua máquina.
# 2.2. Substitua '<SEU-USUARIO>' pelo seu nome de usuário.
# 2.3. Substitua '<NOME-DO-REPOSITORIO>' pelo nome do seu repositório.

git clone https://github.com/<SEU-USUARIO>/<NOME-DO-REPOSITORIO>.git
cd <NOME-DO-REPOSITORIO>

### 3. ADICIONE O REPOSITÓRIO ORIGINAL COMO "UPSTREAM":
#
# Isso permite que você mantenha seu fork atualizado com o projeto principal.

git remote add upstream https://github.com/USUARIO-OU-ORGANIZACAO-DONO/NOME-DO-REPOSITORIO.git

## 4. VERIFIQUE A CONFIGURAÇÃO:

git remote -v

# A saída deve mostrar 'origin' (apontando para o seu fork) e 'upstream' (apontando para o repositório original).
```

### Passo 3: Sincronize e Crie sua Branch de Trabalho

Antes de começar a codificar, sempre sincronize sua branch `main` com o projeto original e crie uma nova branch para sua tarefa.

```bash
# Vá para a sua branch principal local
git checkout main

# Baixe as últimas alterações do repositório original (upstream)
git pull upstream main

# Crie uma nova branch para sua funcionalidade ou correção.
# Use um nome descritivo (ex: feature/set-command, fix/parser-bug).
git checkout -b feature/implementar-feature-x
```

### Passo 4: Codifique e Faça Commits

Implemente a funcionalidade ou correção na sua branch. Faça commits pequenos e atômicos. Cada commit deve representar uma única mudança lógica e ter uma mensagem clara.

#### Codificação

Esta é a parte consiste em criar e modificar arquivos. Enquanto trabalha, você pode usar o comando `git status` a qualquer momento para ver o que foi alterado.

```bash
# Mostra quais arquivos foram modificados, quais são novos, etc.
git status
```

A saída mostrará os arquivos em `Changes not staged for commit`. Isso significa que o Git viu as mudanças, mas elas ainda não foram selecionadas para serem salvas no próximo commit.

#### Staging Area

Antes de "salvar" (commitar), você precisa dizer ao Git exatamente **quais mudanças** quer incluir nesse save point. Isso é feito com o comando `git add`. Essa área de preparação (chamada de *Staging Area*) permite que você crie commits muito precisos.

Você pode adicionar arquivos um por um:

```bash
# Adiciona um arquivo específico à Staging Area
git add src/parser.js

# Adiciona outro arquivo
git add tests/parser.test.js
```

Ou, se tiver certeza de que quer incluir **todas** as suas mudanças, pode usar o ponto:

```bash
# Adiciona todos os arquivos modificados no diretório atual e subdiretórios
git add .
```

> **Dica:** Use `git add .` com cuidado. É fácil incluir acidentalmente arquivos de log, dependências ou mudanças de depuração (`console.log`) que não deveriam fazer parte do commit. Ser explícito com `git add <arquivo>` é mais seguro.

Depois de usar `git add`, rode `git status` novamente. Você verá que os arquivos agora estão em `Changes to be committed`.

####  Commit

Agora que você preparou as mudanças, é hora de salvá-las permanentemente no histórico com `git commit`. Cada commit precisa de uma **mensagem** que descreva o que foi feito.

A mensagem é a parte mais importante para a colaboração. Ela explica o **"porquê"** da mudança para seus colegas (e para o seu "eu" do futuro).

```bash
git commit -m "tipo: Descrição curta da mudança"
```

Nós seguimos um padrão para as mensagens de commit para manter o histórico limpo e legível:

*   **`feat:`** Para adicionar uma nova funcionalidade.
*   **`fix:`** Para corrigir um bug.
*   **`docs:`** Para mudanças na documentação.
*   **`style:`** Para mudanças de formatação (ponto e vírgula, etc.) que não alteram a lógica.
*   **`refactor:`** Para mudanças no código que não adicionam funcionalidades nem corrigem bugs.
*   **`test:`** Para adicionar ou corrigir testes.

Por exemplo:

*   `feat: Adiciona parser para o comando SET`
*   `fix: Corrige cálculo de offset em leituras de arquivo`
*   `docs: Atualiza a seção de contribuição do README`

### Passo 5: Envie sua Branch para o Seu Fork

Até agora, todos os seus commits existem apenas no seu computador. Eles estão seguros no seu repositório local, mas invisíveis para o resto da equipe no GitHub.

Para compartilhar seu trabalho, quando estiver satisfeito (ou quiser um feedback inicial), envie sua branch para o seu fork remoto no GitHub (`origin`).

```bash
# O -u estabelece uma ligação entre sua branch local e a remota no seu fork
git push -u origin feature/implementar-feature-x
```

Quando você executa o `push` pela **primeira vez** com a flag `-u`, você está dizendo ao Git duas coisas:

1.  Envie a branch `feature/implementar-feature-x` para o meu repositório `origin`.
2.  E, a partir de agora, **estabeleça um link permanente** entre a minha branch local `feature/implementar-feature-x` e a nova branch remota com o mesmo nome que será criada no `origin`.

Depois de fazer esse primeiro push com `-u`, sua vida fica muito mais fácil. Para enviar commits futuros na **mesma branch**, você não precisa mais especificar o destino e a branch. O Git já se lembra da conexão que você criou.

```bash
# A PRIMEIRA VEZ que você envia esta branch, use -u:
# O Git agora sabe que a sua branch local está ligada à do seu fork.
git push -u origin feature/implementar-feature-x

# DAQUI EM DIANTE, para enviar mais atualizações, basta fazer:
git push
```

### Passo 6: Abra um Pull Request (PR)

![](https://docs.github.com/assets/cb-87213/mw-1440/images/help/pull_requests/pull-request-review-edit-branch.webp)

No GitHub, vá para o seu fork e você verá um aviso para [criar um **Pull Request** a partir da sua nova branch](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request). Preencha o template do PR:

*   **Título:** Dê um título claro e conciso (ex: "Feature: Implementa a Feature XYZ").
*   **Descrição:** Explique **o que** você fez e **por que**. Se o PR resolve uma **Issue**, mencione-a com `Closes #123`.

### Passo 7: Participe da Revisão de Código

Um ou mais membros da equipe irão revisar seu código. A revisão é um processo colaborativo para melhorar a qualidade do código. Esteja aberto a sugestões e críticas construtivas. Faça as alterações solicitadas e envie-as para a mesma branch. O PR será atualizado automaticamente.

### Passo 8: Merge e Limpeza

Após a aprovação, [seu PR será "mergeado" na branch `main` do repositório principal](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/merging-a-pull-request). Parabéns, sua contribuição agora faz parte do projeto!
