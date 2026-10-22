# Plano da Fase 1 — Fundamentos (semanas 1 a 4)

**Objetivo da fase:** sair de "sei um pouco de lógica" para **um script em TypeScript que liga, desliga e mostra o status de um servidor Minecraft rodando em Docker**.

**Documento do projeto:** [`PROJETO.md`](PROJETO.md)

**Ritmo:** 3 sessões por semana, de 2 a 3h cada (cerca de 7,5h por semana). Se uma sessão não couber, ela passa para a próxima. Não pule a entrega da semana.

---

## Como usar este plano

**Toda sessão segue o mesmo ritual:**

1. Abra o `docs/DIARIO.md` e escreva a data e a meta da sessão (1 linha).
2. Estude o material e faça a tarefa.
3. Rode o **teste de "pronto"** da tarefa. Se passou, marque o `[ ]` como `[x]`.
4. Faça o commit (as mensagens abaixo são sugestões, use as suas palavras se quiser).
5. Volte no diário: o que fiz, o que travou, o que aprendi (2 ou 3 linhas).

**Quando travar:**

- Tente sozinho por 30 minutos: leia a mensagem de erro inteira e pesquise o erro exato.
- Depois disso, peça ajuda (para mim, Claude, ou num fórum), mas **peça explicação, não código pronto**. Por exemplo: "por que esse erro acontece?" em vez de "escreve isso pra mim". Quem escreve o código é você. É assim que o conhecimento fica.
- Anote no diário o que te destravou.

**Semana ruim?** Faça 20 minutos de qualquer item e registre no diário. Vale mais que zerar a semana.

---

## Semana 1 — Ambiente, terminal e Git

**Entrega da semana:** repositório público no GitHub com `docs/PROJETO.md`, `docs/PLANO-FASE-1.md`, `docs/DIARIO.md` e um `README.md`, com pelo menos 3 commits seus.

### Sessão 1.1 — Preparar a máquina e o primeiro commit

- [X] Instalar o Git e configurar nome e e-mail (`git config --global user.name` / `user.email`).
- [X] Instalar o **nvm** e, com ele, o Node.js LTS (`nvm install --lts`).
- [X] Instalar o VS Code (ou o editor que preferir).
- [X] Dentro de `~/Documentos/projeto-servidores`, rodar `git init`.
- [X] Criar `docs/DIARIO.md` com a primeira entrada.
- [X] Criar um `.gitignore` com `node_modules/` e `.env`.

**Pronto quando:** `node --version`, `npm --version` e `git --version` mostram versões, e `git log` mostra seu primeiro commit.

**Commit sugerido:** `docs: adiciona documento do projeto, plano da fase 1 e diário`

**Materiais:**
- nvm: https://github.com/nvm-sh/nvm
- Pro Git (livro grátis em português), capítulos 1 e 2: https://git-scm.com/book/pt-br/v2

### Sessão 1.2 — Terminal Linux

Aprender a se mover pelo sistema sem interface gráfica. É a base de tudo em infraestrutura.

- [x] Praticar: `pwd`, `ls -la`, `cd`, `mkdir`, `touch`, `cp`, `mv`, `rm`, `cat`, `less`, `grep`, `find`, `chmod`, `ps`, `top`, `man`.
- [x] Entender permissões de arquivo (`rwx`, dono, grupo) e o que o `sudo` faz.
- [x] Jogar o **OverTheWire Bandit** do nível 0 ao 5 (é um jogo de terminal via SSH).
- [x] Anotar no diário os comandos novos que você aprendeu e para que servem.

**Pronto quando:** você passou do nível 5 do Bandit e consegue explicar o que `chmod 755 arquivo` faz.

**Commit sugerido:** `docs: registra estudos de terminal no diário`

**Materiais:**
- OverTheWire Bandit: https://overthewire.org/wargames/bandit/
- The Linux Command Line (livro grátis, em inglês), parte 1: https://linuxcommand.org/tlcl.php

### Sessão 1.3 — Git de verdade e GitHub

- [x] Fazer a trilha **"Introduction Sequence"** do Learn Git Branching (tem português).
- [x] Entender: commit, branch, merge, `git status`, `git diff`, `git log --oneline`.
- [x] Criar uma conta no GitHub (se não tiver) e configurar uma chave SSH.
- [x] Criar o repositório público e fazer `git push`.
- [x] Escrever um `README.md` curto: o que é o projeto, a stack, o status ("Fase 1 em andamento") e um link para `docs/PROJETO.md`.
- [x] Praticar o fluxo com branch: criar `git switch -c docs/readme`, commitar o README, voltar para a `main` e fazer o merge.

**Pronto quando:** o repositório aparece no GitHub com o README renderizado e o `git log --oneline --graph` mostra o merge.

**Commit sugerido:** `docs: adiciona README inicial`

**Materiais:**
- Learn Git Branching: https://learngitbranching.js.org/?locale=pt_BR
- GitHub Docs, chave SSH: https://docs.github.com/pt/authentication/connecting-to-github-with-ssh

---

## Semana 2 — JavaScript e TypeScript

Você já sabe lógica de programação com Python. Agora é aprender **a mesma lógica com outra escrita**. Anote no diário as diferenças que perceber: isso fixa muito.

**Entrega da semana:** `estudos/semana-2/servidores.ts` rodando com `npx tsx`, com tipos e funções sobre uma lista de servidores de mentira.

### Sessão 2.1 — Base do JavaScript

- [ ] Ler o javascript.info, parte 1, capítulo 2 ("JavaScript Fundamentals"), ou o mesmo assunto no Guia da MDN em português: variáveis (`let`/`const`), tipos, condições, laços, funções e arrow functions.
- [ ] Criar `estudos/semana-2/` e rodar um `ola.ts` com `npx tsx ola.ts`.
- [ ] Refazer em TS 3 exercícios simples que você já fez em Python (por exemplo: par ou ímpar, tabuada, maior de uma lista).

**Pronto quando:** os 3 exercícios rodam e você sabe explicar a diferença entre `let` e `const`.

**Commit sugerido:** `chore: adiciona primeiros exercícios em TypeScript`

**Materiais:**
- javascript.info (em inglês, o mais completo; use o tradutor do navegador se precisar): https://javascript.info/
- MDN, Guia de JavaScript: https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Guide

### Sessão 2.2 — Arrays e objetos

- [ ] Estudar objetos e arrays (javascript.info, capítulos 4 e 5): `map`, `filter`, `find`, `reduce`, desestruturação e spread (`...`).
- [ ] Em `estudos/semana-2/servidores.ts`, criar uma lista de 5 servidores de mentira, cada um com `nome`, `jogo`, `memoriaMb` e `status` (`"ligado"` ou `"desligado"`).
- [ ] Escrever funções que: listam só os ligados, somam a memória total usada pelos ligados e buscam um servidor pelo nome.

**Pronto quando:** `npx tsx servidores.ts` imprime as três respostas corretas.

**Commit sugerido:** `feat(estudos): manipula lista de servidores com map e filter`

### Sessão 2.3 — Tipos do TypeScript

- [ ] Ler o TypeScript Handbook: "The Basics" e "Everyday Types".
- [ ] Fazer o tutorial gratuito "Beginners TypeScript" da Total TypeScript.
- [ ] Voltar no `servidores.ts` e tipar tudo: `type Servidor = { ... }`, `type Status = "ligado" | "desligado"`, e os tipos de parâmetro e retorno de cada função.
- [ ] Provocar erros de propósito (status `"quebrado"`, memória como texto) e ler o que o TypeScript reclama.
- [ ] Instalar o TypeScript no projeto e rodar `npx tsc --noEmit` para checar tipos.

**Pronto quando:** `npx tsc --noEmit` não mostra erros e o script continua rodando.

**Commit sugerido:** `refactor(estudos): adiciona tipos ao exemplo de servidores`

**Materiais:**
- TypeScript Handbook: https://www.typescriptlang.org/docs/handbook/intro.html
- Total TypeScript, Beginners Tutorial (grátis): https://www.totaltypescript.com/tutorials/beginners-typescript

---

## Semana 3 — Assíncrono, HTTP e primeiro teste

Uma API passa o dia esperando: banco, Docker, rede. Entender código assíncrono e HTTP é obrigatório para o back-end.

**Entrega da semana:** um script que busca na internet a lista de versões do Minecraft, mostra a última versão estável e tem um teste automatizado da função principal.

### Sessão 3.1 — Promises e async/await

- [ ] Ler o javascript.info, capítulo 11 ("Promises, async/await") até "Async/await" (https://javascript.info/async).
- [ ] Em `estudos/semana-3/espera.ts`: criar uma função `ligarServidor(nome: string): Promise<string>` que "demora" 2 segundos (`setTimeout`) e devolve `"<nome> ligado"`. Chamar a função para 3 servidores, primeiro um depois do outro e depois todos juntos com `Promise.all`, medindo o tempo.

**Pronto quando:** você vê no terminal que a versão em sequência leva cerca de 6s e a com `Promise.all` cerca de 2s, e sabe explicar por quê.

**Commit sugerido:** `feat(estudos): compara execução sequencial e paralela com promises`

### Sessão 3.2 — Como a web funciona: HTTP

- [ ] Ler a "Visão geral do HTTP" da MDN: método, URL, cabeçalhos, corpo e status.
- [ ] Decorar os status principais: 200, 201, 204, 400, 401, 403, 404, 500 e 503. Eles estão na seção 6 do `PROJETO.md`.
- [ ] Usar o `curl -i` no terminal contra a URL do manifesto do Minecraft (abaixo) e identificar o status, os cabeçalhos e o corpo JSON.
- [ ] Anotar no diário: qual a diferença entre GET e POST? O que é JSON?

**Pronto quando:** você consegue explicar, sem olhar, o que significam 401, 403 e 404.

**Materiais:**
- MDN, Visão geral do HTTP: https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Guides/Overview
- MDN, códigos de status HTTP: https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Reference/Status
- Manifesto de versões do Minecraft (JSON público): https://piston-meta.mojang.com/mc/game/version_manifest_v2.json

### Sessão 3.3 — Buscar dados e o primeiro teste

- [ ] Iniciar um `package.json` (`npm init -y`) e instalar como dev: `typescript`, `tsx`, `vitest`.
- [ ] Em `estudos/semana-3/versoes.ts`: escrever `ultimaVersaoEstavel(manifesto: Manifesto): string`. Ela é uma **função pura**: recebe o JSON já baixado e devolve `manifesto.latest.release`. Tipe o `Manifesto` só com os campos que você usa.
- [ ] Escrever `buscarManifesto(): Promise<Manifesto>`, usando `fetch` na URL acima.
- [ ] Juntar as duas no script: buscar, calcular e imprimir `"Última versão estável: X"`.
- [ ] **Escrever o teste antes de mexer mais:** em `estudos/semana-3/versoes.test.ts`, testar `ultimaVersaoEstavel` com um manifesto de mentira em que `latest.release = "1.21.1"`, esperando `"1.21.1"`.
- [ ] Adicionar o script `"test": "vitest run"` no `package.json`.
- [ ] Tratar erro: se o `fetch` voltar com status diferente de 200, lançar um erro com uma mensagem clara, e o script mostrar essa mensagem em vez de quebrar feio. (Teste desligando a internet.)

**Pronto quando:** `npm test` passa; `npx tsx versoes.ts` mostra a versão; e sem internet aparece uma mensagem de erro clara.

**Commit sugerido:** `feat(estudos): busca última versão do Minecraft com teste`

**Materiais:**
- Node.js, aprender (fetch, módulos): https://nodejs.org/en/learn
- Vitest, Getting Started: https://vitest.dev/guide/

> **Por que separar `buscarManifesto` de `ultimaVersaoEstavel`?** Assim dá para testar a lógica sem internet. É a mesma ideia que o `PROJETO.md` usa para o Docker (seção 7).

---

## Semana 4 — Docker e a entrega da fase

**Entrega da fase 1:** `npx tsx estudos/semana-4/servidor.ts start|stop|status` controla um servidor Minecraft real rodando em Docker na sua máquina.

### Sessão 4.1 — Conceitos de Docker

- [ ] Instalar o Docker Engine no Debian seguindo a documentação oficial.
- [ ] Entender o que é: imagem, container, porta (`-p`), volume (`-v`), variável de ambiente (`-e`), `docker ps`, `docker logs`, `docker stop`, `docker rm`.
- [ ] Fazer o "Get started" oficial do Docker (partes de conceitos e de rodar containers).
- [ ] Ler sobre o grupo `docker`: colocar seu usuário nele evita digitar `sudo`, mas dá a ele poder de root. Anote isso no diário; é assunto de entrevista.

**Pronto quando:** `docker run hello-world` funciona e você sabe explicar a diferença entre imagem e container.

**Materiais:**
- Docker Engine no Debian: https://docs.docker.com/engine/install/debian/
- Docker, Get started: https://docs.docker.com/get-started/

### Sessão 4.2 — Minecraft no Docker, à mão

- [ ] Ler o README da imagem `itzg/minecraft-server`.
- [ ] Subir o servidor à mão com `docker run`, usando `-e EULA=TRUE`, `-e MEMORY=1G`, `-p 25565:25565`, um volume para a pasta `/data` e `--name mc-teste`.
- [ ] Acompanhar `docker logs -f mc-teste` até aparecer `Done`.
- [ ] Parar, ligar de novo e confirmar que o mundo continua lá (por causa do volume).
- [ ] Se você ou um amigo tiver Minecraft Java: conectar em `localhost`.
- [ ] Anotar no diário: o que acontece com o mundo se você apagar o container **sem** volume?

**Pronto quando:** o servidor sobe, para e volta com o mesmo mundo.

**Commit sugerido:** `docs: registra comandos do servidor Minecraft em Docker`

**Materiais:**
- itzg/minecraft-server, documentação: https://docker-minecraft-server.readthedocs.io/

### Sessões 4.3 e 4.4 — Controlando o Docker com TypeScript

Agora você faz pelo código o que fez à mão. Essa é a semente da API da fase 2.

- [ ] Instalar `dockerode` e `@types/dockerode`.
- [ ] Em `estudos/semana-4/docker.ts`, escrever três funções:
  - `statusServidor(nome: string): Promise<"ligado" | "desligado" | "inexistente">`
  - `ligarServidor(nome: string): Promise<void>`: se o container não existir, cria com as mesmas opções da sessão 4.2; se existir e estiver parado, só liga.
  - `desligarServidor(nome: string): Promise<void>`
- [ ] Em `estudos/semana-4/servidor.ts`, ler o comando de `process.argv` (`start`, `stop` ou `status`) e chamar a função certa com o nome `mc-teste`.
- [ ] Tratar os erros com mensagem clara: comando desconhecido (mostrar como usar), Docker desligado ("O Docker não está rodando?"), ligar algo já ligado e desligar algo já desligado (avisar, sem quebrar).
- [ ] Testar com Vitest a parte que não depende do Docker: a função que interpreta o comando digitado (`interpretarComando(args: string[])`), cobrindo `start`, `stop`, `status`, comando vazio e comando inválido.
- [ ] Atualizar o README: status "Fase 1 concluída", com um GIF ou print do script funcionando.

**Pronto quando:**
- `npx tsx servidor.ts start`, depois `status` mostra `ligado`;
- `npx tsx servidor.ts stop`, depois `status` mostra `desligado`;
- `npx tsx servidor.ts voar` mostra como usar;
- com o Docker parado (`sudo systemctl stop docker`), aparece uma mensagem clara em vez de um erro enorme;
- `npm test` passa.

**Commits sugeridos:**
- `feat(estudos): controla container Minecraft com dockerode`
- `test(estudos): testa interpretação de comandos do script`
- `docs: marca fase 1 como concluída no README`

**Materiais:**
- dockerode: https://github.com/apocas/dockerode
- Node.js, `process.argv`: https://nodejs.org/api/process.html#processargv

---

## Fechamento da fase 1

- [ ] Reler o diário das 4 semanas e escrever um parágrafo: o que foi mais difícil e o que ficou fácil.
- [ ] Conferir o "pronto" de cada sessão.
- [ ] Me chamar (Claude) para montar o **plano da fase 2 (API e banco)**. A pasta `estudos/` fica como registro, e o código de verdade começa em `apps/api/`.

**Commit sugerido:** `docs: retrospectiva da fase 1`
