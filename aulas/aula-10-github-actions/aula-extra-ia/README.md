# Aula Extra — IA e DevOps: o que importa é saber o que pedir 🎁

> **Aula extra aninhada na Aula 10**, logo depois da prática (**18/11, 20:50–21:15**, antes do Q&A final). Para a turma, é "a surpresa final": não anunciar o conteúdo antes. Para a equipe, é uma aula com roteiro, prompt e deck próprios.
>
> 📽️ Slides: [`slides/aula-extra.odp`](slides/aula-extra.odp) (roteiro editável em [`slides/aula-extra.json`](slides/aula-extra.json)). Prompt da demo: [`prompt-detalhado.txt`](prompt-detalhado.txt).
>
> ⏱ Na Aula 10, prática + aula extra somam **1 hora** (20:15–21:15): 35 min de prática e 25 min aqui. A prática precisa terminar às 20:50 — por isso o badge e o desafio bônus já são missão de casa. Depois da aula extra, o deck da Aula 10 fecha a live com encerramento e Q&A (21:15–21:35).

## Agenda (25 min)

| Horário | Bloco | Minutos |
|---------|-------|---------|
| 20:50 | A chamada + enquete no chat | 3 |
| 20:53 | O pedido: a especificação na tela | 4 |
| 20:57 | Ao vivo: a IA constrói o projeto e prova que funciona | 7 |
| 21:04 | É o nosso projeto? Comparação com o repositório de um aluno | 5 |
| 21:09 | A virada: a turma revisa a IA + mensagem pedagógica | 6 |
| 21:15 | Encerramento da Aula 10 (de volta ao deck da Aula 10, com Q&A, até 21:35) | 20 |

## A ideia

Durante duas semanas, a turma construiu com as próprias mãos: estrutura de projeto, health check, pipeline de build/teste/deploy, Dockerfile, compose, repositório no GitHub e CI com Actions.

O plot twist: **mostrar, ao vivo, uma IA recriando tudo isso em poucos minutos, a partir de um único prompt.**

E a lição por trás do truque: **o que importa agora é saber o que pedir — e como pedir.** O prompt da demo é uma especificação de 65 linhas, e cada linha dela é vocabulário que a turma aprendeu em 10 aulas: `set -e`, `grep -q`, código de saída, `nginx:alpine`, serviço do compose, gatilho do workflow. Quem não fez o bootcamp não saberia escrever esse pedido — nem conferir o resultado.

## O objetivo pedagógico (o mais importante!)

O impacto inicial é o "uau" (e um friozinho na barriga 😅). A mensagem final deve ser **energizante, não desanimadora**:

1. **A IA só fez em minutos porque VOCÊS agora sabem julgar o que ela fez.** Sem as 10 aulas, o resultado seria um bloco de texto indecifrável. Com elas, vocês leem cada arquivo e sabem exatamente o que é.
2. **O trabalho do profissional DevOps mudou de lugar:** sai do "digitar comandos" e vai para **entender, revisar, decidir e operar**. A IA escreve o script; quem responde pelo deploy em produção é você.
3. **Quem domina os fundamentos multiplica a própria produtividade com IA.** Quem não domina, apenas copia e cola — e não sabe consertar quando quebra (e sempre quebra!).

## O prompt

O [`prompt-detalhado.txt`](prompt-detalhado.txt) descreve o projeto da turma item a item:

| Bloco do prompt | O que especifica |
|---|---|
| Estrutura | Os 11 arquivos, com nome e caminho |
| Scripts | O que cada um imprime e faz: mensagens `[OK]`/`[FALHA]`/`[BUILD]`/`[TEST]`/`[DEPLOY]`, `set -e`, `grep -q`, `exit 1` |
| Containers | `Dockerfile` com `nginx:alpine`; `compose.yaml` com os serviços `site` e `visitas` |
| CI | `ci.yml` igual ao da prática de hoje |
| Prova | Pipeline verde, teste quebrado de propósito barrando o deploy, `docker compose up`, primeiro commit |

Ele foi testado numa máquina limpa, sem acesso ao material: o resultado sai igual ao projeto da turma, até o `test.sh`. No ensaio de 17/11 levou **55 segundos** (sem contar as autorizações).

## Passo a passo na VM da demo

A VM da demo é uma VM **separada** da VM da prática (igual à do [setup](../../../setup/README.md), com Docker, Compose, Git e a CLI de IA).

### Antes da live

1. Entre na VM da demo por SSH. O prompt do terminal deve mostrar `aluno@bootcamp-ia`.
2. Zere a demo:

   ```bash
   ~/reset-demo.sh
   ```

   Ele apaga `~/meu-projeto-devops`, `~/producao` e os containers das rodadas anteriores.

   O script tem duas linhas (crie-o na home da VM se ainda não existir):

   ```bash
   #!/usr/bin/env bash
   docker ps -aq | xargs -r docker rm -f >/dev/null
   rm -rf ~/meu-projeto-devops ~/producao
   ```
3. Confira que a CLI está logada: digite `claude`, veja se abre sem pedir login e saia com `/exit`.
4. No seu computador, deixe aberto o arquivo do prompt (para mostrar e copiar) e, no navegador, o repositório de um aluno.

### Ao vivo

1. Fique na home. **Não crie pasta nenhuma:** a especificação já diz onde o projeto vai morar (`~/meu-projeto-devops`), e a IA cria.

   ```bash
   cd ~
   claude
   ```

   Na primeira vez em cada pasta ela pergunta se você confia na pasta: confirme.
2. Copie o conteúdo do [`prompt-detalhado.txt`](prompt-detalhado.txt), cole no `claude` e dê Enter.
3. A IA pede autorização antes de criar arquivos e de rodar comandos. Aprove — de preferência com a opção que **não pergunta de novo**, para a demo andar. (É um bom gancho: "ela pede licença; quem decide é a gente".)
4. Narre enquanto ela trabalha ("criou o `build.sh`… agora está rodando a pipeline… olha o teste falhando de propósito") e deixe a prova rodar até o commit.
5. Quando ela terminar, saia com `/exit` e mostre o que nasceu:

   ```bash
   ls ~/meu-projeto-devops ~/meu-projeto-devops/scripts
   cat ~/meu-projeto-devops/scripts/test.sh
   ```

O projeto fica em `~/meu-projeto-devops` e a "produção" em `~/producao` — os mesmos lugares do projeto da turma.

### Comparação

O projeto da turma aparece no **navegador** (repositório de um aluno no GitHub); o da IA, no terminal. Assim ninguém precisa trocar de VM ao vivo.

> ⏱ Os 55 segundos do ensaio foram medidos sem as autorizações. Aprovando na tela, conte com 2 a 3 minutos. Se o tempo apertar, abra a IA com `claude --dangerously-skip-permissions`: ela executa tudo sem perguntar. Só use isso nesta VM descartável.

## Roteiro da demo (25 min)

1. **Setup prévio:** siga o *Antes da live* do [passo a passo](#passo-a-passo-na-vm-da-demo): VM da demo zerada, CLI logada, nenhum token visível. Dupla: um narra, outro digita.
2. **A chamada (3 min):** "Vocês levaram 10 aulas para construir esse projeto. Quanto tempo uma IA levaria?" — enquete no chat.
3. **O pedido (4 min):** mostre o prompt na tela e dê zoom em 2 ou 3 trechos (as mensagens `[OK]`/`[FALHA]`, o `grep -q`, o serviço `visitas`). Pergunte: "reconhecem isso?" A frase-chave: **"cada linha desse pedido é algo que vocês aprenderam aqui."**
4. **Ao vivo (7 min):** abra o `claude` na home (`cd ~`), cole a especificação e narre. Celebre o verde.
5. **Comparação (5 min):** abra o `test.sh` da IA ao lado do `test.sh` de um aluno. Pergunte ao chat: "é o nosso projeto?" — mesmos arquivos, mesmas mensagens, mesmo `ci.yml`.
6. **A virada (6 min):** "a IA errou algo? o que vocês fariam diferente?" — deixe a turma revisar a IA. Feche com a mensagem pedagógica acima e, às 21:15, volte ao deck da Aula 10 para o encerramento (próximos passos, carreira e o aviso de que o certificado será enviado pela organização).

## Checklist de riscos

- [ ] **Ensaio do prompt** na VM da demo, seguindo o passo a passo; anotar o tempo. Depois do ensaio, rodar `~/reset-demo.sh`.
- [ ] Internet do estúdio testada (a demo baixa imagens Docker).
- [ ] Imagens `nginx:alpine` e `redis:alpine` já baixadas na máquina da demo (cache).
- [ ] Vídeo de backup gravado do fluxo completo.
- [ ] Nenhum token/segredo visível na tela durante a demo (usar conta de demonstração!).
- [ ] Combinar quem narra e quem digita (dupla funciona melhor).
