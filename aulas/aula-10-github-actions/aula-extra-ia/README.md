# Aula Extra — IA e DevOps: o que importa é saber o que pedir 🎁

> **Aula extra aninhada na Aula 10**, logo depois da prática (**18/11, 20:50–21:15**, antes do Q&A final). Para a turma, é "a surpresa final": não anunciar o conteúdo antes. Para a equipe, é uma aula com roteiro, prompt e deck próprios.
>
> 📽️ Slides: [`slides/aula-extra.odp`](slides/aula-extra.odp) (roteiro editável em [`slides/aula-extra.json`](slides/aula-extra.json)). Prompts da demo: [`prompt-simples.txt`](prompt-simples.txt) e [`prompt-detalhado.txt`](prompt-detalhado.txt).
>
> ⏱ Na Aula 10, prática + aula extra somam **1 hora** (20:15–21:15): 35 min de prática e 25 min aqui. A prática precisa terminar às 20:50 — por isso o badge e o desafio bônus já são missão de casa. Depois da aula extra, o deck da Aula 10 fecha a live com encerramento e Q&A (21:15–21:35).

## Agenda (25 min)

| Horário | Bloco | Minutos |
|---------|-------|---------|
| 20:50 | A chamada + enquete no chat | 3 |
| 20:53 | Prompt 1, ao vivo: o pedido simples (9 linhas) | 7 |
| 21:00 | Funcionou… mas é o nosso projeto? Comparação lado a lado | 5 |
| 21:05 | Prompt 2: a especificação — o resultado igual ao da turma | 4 |
| 21:09 | A virada: a turma revisa a IA + mensagem pedagógica | 6 |
| 21:15 | Encerramento da Aula 10 (de volta ao deck da Aula 10, com Q&A, até 21:35) | 20 |

## A ideia

Durante duas semanas, a turma construiu com as próprias mãos: estrutura de projeto, health check, pipeline de build/teste/deploy, Dockerfile, compose, repositório no GitHub e CI com Actions.

O plot twist: **mostrar, ao vivo, uma IA recriando tudo isso em poucos minutos, a partir de um único prompt.**

E a lição por trás do truque: **o que importa agora é saber o que pedir — e como pedir.** Um pedido vago produz um projeto que *funciona*, mas não é o nosso; uma especificação precisa produz o projeto da turma. A diferença entre os dois prompts é exatamente o vocabulário que a turma aprendeu em 10 aulas.

## O objetivo pedagógico (o mais importante!)

O impacto inicial é o "uau" (e um friozinho na barriga 😅). A mensagem final deve ser **energizante, não desanimadora**:

1. **A IA só fez em minutos porque VOCÊS agora sabem julgar o que ela fez.** Sem as 10 aulas, o resultado seria um bloco de texto indecifrável. Com elas, vocês leem cada arquivo e sabem exatamente o que é.
2. **O trabalho do profissional DevOps mudou de lugar:** sai do "digitar comandos" e vai para **entender, revisar, decidir e operar**. A IA escreve o script; quem responde pelo deploy em produção é você.
3. **Quem domina os fundamentos multiplica a própria produtividade com IA.** Quem não domina, apenas copia e cola — e não sabe consertar quando quebra (e sempre quebra!).

## Dois prompts, um objetivo

| | Prompt 1 — o pedido simples | Prompt 2 — a especificação |
|---|---|---|
| Arquivo | [`prompt-simples.txt`](prompt-simples.txt) (9 linhas) | [`prompt-detalhado.txt`](prompt-detalhado.txt) (63 linhas) |
| O que diz | O que queremos, em linguagem natural, com o vocabulário do bootcamp (build, teste, deploy, pipeline, nginx, compose, redis, workflow) | Nomes de arquivos, caminhos, mensagens, comportamentos e a prova, item a item |
| Funciona? | **Sim**: pipeline verde, teste quebrado barra o deploy, commit — em ~1 min | **Sim**, igual |
| É o projeto da turma? | **Não.** Num dos ensaios (muda a cada rodada — aponte o que aparecer na hora) a IA decidiu sozinha: `dist/` em vez de `app/`; produção dentro do projeto em vez de `~/producao`; título "Meu Projeto DevOps"; mensagens `[build]`/`[test]` e 5 verificações no teste; `nginx:1.27-alpine`; serviço `redis` com volume e `restart`; workflow em qualquer push + upload de artefato; `set -euo pipefail`; `.gitignore` e README que ninguém pediu | **Sim.** 11 arquivos com os mesmos nomes, mensagens `[OK]`/`[FALHA]`/`[BUILD]`/`[TEST]`/`[DEPLOY]`, `nginx:alpine`, serviço `visitas`, `ci.yml` igual |

Os dois foram testados numa máquina limpa, sem acesso ao material. Nenhum dos dois está "errado": o primeiro mostra o que a IA faz quando a gente não sabe o que quer; o segundo mostra o que ela faz quando a gente sabe.

## Prompt 1 — o pedido simples (ao vivo)

```text
Crie um projeto chamado meu-projeto-devops com scripts em bash:
- um build que gera uma pagina index.html com a data do build;
- um teste que verifica a pagina e falha com codigo de saida diferente de zero se ela estiver errada;
- um deploy que copia a pagina para uma pasta de "producao";
- uma pipeline que roda build, teste e deploy nessa ordem e para no primeiro erro.
Inclua um Dockerfile com nginx para servir a pagina, um compose com o site e um redis,
e um workflow do GitHub Actions que roda build e teste a cada push.
Rode a pipeline para provar que funciona e depois quebre o teste de proposito
para mostrar que o deploy nao acontece. Por fim, inicie o repositorio git e faca o primeiro commit.
```

Narre enquanto a IA trabalha ("ela criou um `build.sh`… olha, decidiu chamar a pasta de `dist`") e deixe a prova rodar: pipeline verde, teste quebrado sem deploy, commit.

## Prompt 2 — a especificação (ao vivo também)

O [`prompt-detalhado.txt`](prompt-detalhado.txt) descreve o projeto da turma item a item. No ensaio de 17/11 ele levou **55 segundos**, então cabe ao vivo: mostre o prompt na tela (dê zoom em 2 ou 3 trechos: as mensagens `[OK]`/`[FALHA]`, o `grep -q`, o serviço `visitas`), rode e abra o `test.sh` da IA — idêntico ao `test.sh` da turma. Se algo travar, use o vídeo de backup.

## Passo a passo na VM da demo

Os dois prompts rodam na **mesma VM**, em **lugares diferentes** — por isso um não atrapalha o outro:

| | Onde rodar | Onde o projeto nasce | Tempo no ensaio |
|---|---|---|---|
| Prompt 1 — simples | `~/demo-simples` | `~/demo-simples/meu-projeto-devops` | 82 s |
| Prompt 2 — detalhado | `~` (a home) | `~/meu-projeto-devops` e `~/producao` | 55 s |

A VM da demo é uma VM **separada** da VM da prática (igual à do [setup](../../../setup/README.md), com Docker, Compose, Git e a CLI de IA).

### Antes da live

1. Entre na VM da demo por SSH. O prompt do terminal deve mostrar `aluno@bootcamp-ia`.
2. Zere a demo:

   ```bash
   ~/reset-demo.sh
   ```

   Ele apaga `~/demo-simples`, `~/meu-projeto-devops`, `~/producao` e os containers das rodadas anteriores.

   O script tem duas linhas (crie-o na home da VM se ainda não existir):

   ```bash
   #!/usr/bin/env bash
   docker ps -aq | xargs -r docker rm -f >/dev/null
   rm -rf ~/demo-simples ~/meu-projeto-devops ~/producao
   ```
3. Confira que a CLI está logada: digite `claude`, veja se abre sem pedir login e saia com `/exit`.
4. No seu computador, deixe abertos os dois arquivos de prompt (para copiar) e, no navegador, o repositório de um aluno.

### Prompt 1 — o pedido simples

1. Crie uma pasta vazia e entre nela. É dentro dela que a IA vai criar o projeto:

   ```bash
   mkdir ~/demo-simples
   cd ~/demo-simples
   ```

2. Abra a IA:

   ```bash
   claude
   ```

   Na primeira vez em cada pasta ela pergunta se você confia na pasta: confirme.
3. Copie o conteúdo do [`prompt-simples.txt`](prompt-simples.txt), cole no `claude` e dê Enter.
4. A IA pede autorização antes de criar arquivos e de rodar comandos. Aprove — de preferência com a opção que **não pergunta de novo**, para a demo andar. (É um bom gancho: "ela pede licença; quem decide é a gente".)
5. Quando ela terminar, saia com `/exit` e mostre o que nasceu:

   ```bash
   ls -R meu-projeto-devops
   cat meu-projeto-devops/scripts/test.sh
   ```

O projeto fica em `~/demo-simples/meu-projeto-devops`.

### Prompt 2 — a especificação

1. Volte para a home. **Não crie pasta nenhuma:** a especificação já diz onde o projeto vai morar (`~/meu-projeto-devops`), e a IA cria.

   ```bash
   cd ~
   claude
   ```

2. Copie o conteúdo do [`prompt-detalhado.txt`](prompt-detalhado.txt), cole e dê Enter. Aprove as autorizações como antes.
3. Quando terminar, saia com `/exit` e mostre:

   ```bash
   ls ~/meu-projeto-devops ~/meu-projeto-devops/scripts
   cat ~/meu-projeto-devops/scripts/test.sh
   ```

O projeto fica em `~/meu-projeto-devops` e a "produção" em `~/producao` — os mesmos lugares do projeto da turma, e por isso o resultado sai igual.

### Comparação

O projeto da turma aparece no **navegador** (repositório de um aluno no GitHub); os dois da IA, no terminal. Assim ninguém precisa trocar de VM ao vivo.

> ⏱ Os tempos da tabela foram medidos sem as autorizações. Aprovando na tela, conte com 2 a 3 minutos por prompt. Se o tempo apertar, abra a IA com `claude --dangerously-skip-permissions`: ela executa tudo sem perguntar. Só use isso nesta VM descartável.

## Roteiro da demo (25 min)

1. **Setup prévio:** siga o *Antes da live* do [passo a passo](#passo-a-passo-na-vm-da-demo): VM da demo zerada, CLI logada, nenhum token visível. Dupla: um narra, outro digita.
2. **A chamada (3 min):** "Vocês levaram 10 aulas para construir esse projeto. Quanto tempo uma IA levaria?" — enquete no chat.
3. **Prompt 1 ao vivo (7 min):** crie `~/demo-simples`, abra o `claude` dentro dela, cole o pedido simples e narre. Celebre o verde: *funcionou*.
4. **Comparação (5 min):** abra o projeto da IA ao lado do projeto de um aluno. Pergunte ao chat: "é o nosso projeto?" — e vá apontando as diferenças da tabela acima. A turma vai perceber que *sabe* ver a diferença.
5. **Prompt 2 (4 min):** mostre a especificação, abra o `claude` na home (`cd ~`), cole-a e abra o `test.sh`, idêntico ao da turma. A frase-chave: **"a diferença entre os dois prompts é o que vocês aprenderam aqui."**
6. **A virada (6 min):** "a IA errou algo? o que vocês fariam diferente?" — deixe a turma revisar a IA. Feche com a mensagem pedagógica acima e, às 21:15, volte ao deck da Aula 10 para o encerramento (próximos passos, carreira e o aviso de que o certificado será enviado pela organização).

## Checklist de riscos

- [ ] **Ensaio com os dois prompts** na VM da demo, seguindo o passo a passo; anotar o tempo e as decisões que a IA tomou sozinha no Prompt 1. Depois do ensaio, rodar `~/reset-demo.sh`.
- [ ] Internet do estúdio testada (a demo baixa imagens Docker).
- [ ] Imagens `nginx:alpine` e `redis:alpine` já baixadas na máquina da demo (cache).
- [ ] Vídeo de backup gravado do fluxo completo.
- [ ] Nenhum token/segredo visível na tela durante a demo (usar conta de demonstração!).
- [ ] Combinar quem narra e quem digita (dupla funciona melhor).
