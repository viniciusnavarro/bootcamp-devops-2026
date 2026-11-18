# Prática 09 — Publicando seu projeto no GitHub ☁️

**Objetivo:** criar sua conta e repositório no GitHub, enviar o `meu-projeto-devops` para a nuvem e abrir seu primeiro Pull Request.

**Onde:** navegador do **seu computador** + terminal conectado à VM **via SSH** — obrigatório hoje: você vai precisar colar um token longo (veja o [setup](../../setup/instalacao-ubuntu-vm.md), passo 5).

> 📝 Deixe a [cola do GitHub](../../recursos/cheat-sheet-github.md) aberta ao lado: o token campo a campo, o ciclo do Pull Request desenhado e o socorro dos erros.

## Passo 1 — Conta no GitHub pronta?

Você criou a conta na missão da Aula 08? Então siga para o Passo 2. 😉

Ainda não? Crie agora em **https://github.com/signup** (nome de usuário profissional — ele aparecerá no seu portfólio — e confirme o e-mail). Se o cadastro pedir alguma verificação, chame um monitor para não perder o ritmo.

## Passo 2 — Crie o repositório

No GitHub: botão **New** (ou https://github.com/new):

| Campo | Valor |
|-------|-------|
| Repository name | `meu-projeto-devops` |
| Description | Projeto do Bootcamp DevOps Matera 2026 |
| Choose visibility | **Public** (é portfólio!) |
| Add README | **Off** |
| Add .gitignore | **No .gitignore** |
| Add license | **No license** |


> Click no botão **"Create repository"**

## Passo 3 — Crie um token de acesso (PAT)

1. GitHub → seu avatar → **Settings** → **Developer settings** → **Personal access tokens** → **Fine-grained tokens** → **Generate new token**
2. Token Name: `bootcamp-matera` · Description: `Token bootcamp-matera` · Resource owner: `Seu username` · Expiration: `30 dias` · *Repository access*: **Only select repositories** → `meu-projeto-devops` · *Permissions*: **+ Add permissions** · **Contents: Read and write** e **Workflows: Read and write** (a segunda é obrigatória na Aula 10, quando você enviará a pipeline).
3. Clique em **Generate token** e **copie o token** (ele aparece uma única vez!).

> ⚡ **Atalho:** este link abre o formulário já com nome, descrição, validade de 30 dias e as duas permissões preenchidos. Falta só escolher o repositório em *Repository access* (**Only select repositories** → `meu-projeto-devops`) e gerar:
>
> <https://github.com/settings/personal-access-tokens/new?name=bootcamp-matera&description=Token+bootcamp-matera&expires_in=30&contents=write&workflows=write>
>
> Confira na tela, antes de gerar, se *Contents* e *Workflows* aparecem como **Read and write**.

> 📧 O GitHub só deixa criar token com o **e-mail da conta confirmado**. Se a página pedir a verificação, abra o e-mail de confirmação que o GitHub enviou no cadastro.

> 🔐 O token é sua senha para esta VM. **Não** o salve em arquivos do projeto, **não** poste print dele no chat.

## Passo 4 — Conecte o repositório local ao remoto

Antes de enviar, confira **o que** vai ser enviado. No terminal da VM:

```bash
cd ~/meu-projeto-devops
git status
git log --oneline --all --decorate
```

Resultado esperado: `On branch main`, `nothing to commit, working tree clean` e, no log, o commit mais recente (o do `compose.yaml`) com `(HEAD -> main)`.

- **Está em outra branch** (por exemplo `melhoria-healthcheck`, da Aula 06)? Os commits do Dockerfile e do compose podem ter ficado só nela, e o push da `main` subiria um projeto incompleto. Traga tudo para a `main`: `git checkout main` e depois `git merge --no-edit melhoria-healthcheck`.
- **Apareceram arquivos modificados?** Faça o commit deles antes (`git add` + `git commit`, como na Aula 06).

Agora ligue o repositório local ao remoto (troque `SEU-USUARIO` pelo seu usuário do GitHub):

```bash
git remote add origin https://github.com/SEU-USUARIO/meu-projeto-devops.git
git remote -v
```

- **Caso tenha informado a url errada para o origin** Se no comando anterior deveria informar a url do repositorio https://github.com/SEU-USUARIO/meu-projeto-devops.git, mas acabou informando https://github.com/SEU-USUARIO/meu-outro-java.git o comando git remote -v vai informar um repositorio diferente do que deveria ser o alvo no github. nesse caso altere usando:

```bash
git remote set-url origin https://github.com/SEU-USUARIO/meu-projeto-devops.git,
git remote -v
```

## Passo 5 — O primeiro push! 🚀

```bash
git push -u origin main
```

Quando pedir usuário: seu usuário do GitHub. Quando pedir senha: **cole o token** (nada aparece na tela — é normal; dê Enter).

Resultado esperado: várias linhas, entre elas `main -> main` e, por último, `branch 'main' set up to track 'origin/main'`. Atualize a página do repositório no navegador: **seu projeto está na nuvem!** Scripts, Dockerfile, compose, histórico — tudo lá. 🎉

> 💡 Para não colar o token a cada push: `git config credential.helper store`.
>
> ⚠️ Isso grava o token **em texto puro** no arquivo `~/.git-credentials` da VM. Aceitável aqui — é uma VM de estudo e o token vale 30 dias para um único repositório. Num computador de trabalho, prefira `git config --global credential.helper 'cache --timeout=7200'` (guarda só na memória, por 2 horas). E, ao fim do bootcamp, **revogue o token** em *Developer settings*.

## Passo 6 — Seu primeiro Pull Request

Vamos fazer uma melhoria pelo fluxo profissional completo. O GitHub mostra automaticamente, na página do repositório, um arquivo chamado `README.md` — então vamos renomear o `README.txt` da Aula 02 (`git mv` renomeia e já avisa o Git) e reescrevê-lo:

```bash
git checkout -b docs-readme
git mv README.txt README.md
vi README.md
```

Apague o que estava lá e escreva um README caprichado em **markdown** — a linguagem de formatação do GitHub, em que `#` vira título e `-` vira lista. Por exemplo:

```markdown
# Meu Projeto DevOps

Projeto construído no Bootcamp DevOps Matera 2026.

## O que tem aqui
- `scripts/` — health check e pipeline (build, test, deploy)
- `Dockerfile` — imagem da aplicação
- `compose.yaml` — app + Redis com docker compose

## Como rodar
docker compose up -d
```

Commit e push da branch:

```bash
git add README.md
git commit -m "adiciona README do projeto"
git push -u origin docs-readme
```

## Passo 7 — Abra e integre o PR

1. No navegador, o GitHub mostra por alguns minutos um aviso amarelo **Compare & pull request** — clique. (Sumiu? Aba **Pull requests** → **New pull request** → em *compare*, escolha `docs-readme`.)
2. Título: `Adiciona README do projeto`. Descreva **o que** e **por quê**.
3. **Create pull request**.
4. Explore a aba **Files changed** — é assim que um colega revisaria seu código.
5. **Merge pull request** → **Confirm merge**.

De volta à VM, sincronize:

```bash
git checkout main
git pull
```

Resultado esperado: o README integrado chegou à sua `main` local. Ciclo completo: branch → push → PR → review → merge → pull. **Esse é o fluxo de trabalho de milhões de devs, e agora é o seu.**

## Desafio bônus 🏆

Capriche no seu **perfil** do GitHub: foto, bio ("Estudante de DevOps — Bootcamp Matera 2026") e fixe (*pin*) o repositório `meu-projeto-devops` na página inicial do perfil.

## Deu errado? 😥

| Mensagem | Causa provável |
|----------|----------------|
| `Authentication failed` | Token colado errado/expirado, ou usou a senha da conta — gere/cole o PAT |
| `remote origin already exists` | `git remote remove origin` e refaça o Passo 4 |
| `error: src refspec main does not match any` | Sua branch se chama `master` (faltou o `init.defaultBranch` da Aula 06). Renomeie com `git branch -M main` e repita o push |
| Colei o token e nada apareceu | Normal: senhas não aparecem. Dê Enter |
| `error: failed to push some refs` | O repositório remoto foi criado com README — rode `git pull origin main --no-rebase --allow-unrelated-histories --no-edit` e repita o push |
| No GitHub faltam o `Dockerfile` e o `compose.yaml` | Eles ficaram em outra branch da VM: `git checkout main`, `git merge --no-edit nome-da-branch` e `git push` |
| `Repository not found` | URL com typo no usuário ou nome do repositório — confira com `git remote -v` |

Outra mensagem? O socorro completo está na [cola do GitHub](../../recursos/cheat-sheet-github.md#-socorro).

## Missão até a próxima aula 📌

1. Faça o desafio bônus (perfil + repositório fixado): é a sua vitrine a partir de agora.
2. Abra um **segundo Pull Request** sozinho(a): corrija ou melhore qualquer coisa no `README.md` pelo fluxo completo — branch → commit → push → PR → merge → `git pull`. Na próxima aula, a pipeline vai rodar dentro desse mesmo fluxo.
