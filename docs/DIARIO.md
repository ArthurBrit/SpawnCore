# Diário do projeto

## 20/10/2026 — Sessão 1.1

* **Meta:** preparar a máquina e fazer o primeiro commit.
* **Fiz:** configurei o Git, instalei nvm e Node 24, criei o repositório.
* **Travou:**
  * criei o `.gitignore` como pasta em vez de arquivo, e um `.env` vazio acabou entrando no commit;
  * apaguei a pasta do projeto e recriei em `~/Documentos/projeto-servidores`; recuperei os docs pela lixeira.
* **Aprendi:**
  * a criar e organizar o `.gitignore`, e que ele precisa ser um arquivo;
  * que um segredo que entrou num commit continua no histórico mesmo se for apagado depois (tem que trocar a senha);
  * que antes do primeiro `push` o projeto só existe na minha máquina;
  * sobre a criação de uma rotina.

## 21/10/2026 — Sessão 1.2

* **Meta:** Aprender os comandos basicos do linux e passar do nivel 5 do Bandit
* **Fiz:** Usei todos os comandos basicos do linux, e consegui concluir ate o nivel 5.
* **Travou:**
  * Não consegui achar a senha ainda do nivel 5, mas não por dificuldade em usar os comandos basicos, mas sim por falta de atenção em certos momentos.
* **Aprendi:**
  * a utilizar os comandos file, du, ssh
  * os comandos basicos de busca do linux
  * criptografia de pastas
* **Desafio:**
  * Utilizamos o chmod 755 para dar as permissoẽs de leitura escrita e execução ao Dono no qual queriamos abrir.

## 22/10/2026 — Sessão 1.3

* **Meta:** Publicar o projeto no GitHub e praticar git branch e merge
* **Fiz:** Criei o repositorio no Github, fiz os desafios do learn git, defini o nome do projeto
* **Travou:**
  * Na criação da chave pulei a parte de definição da senha, mas consegui consertar, tive dificuldade de entender alguns comandos, não os comandos em si, mas as ramificações de um mesmo comando ex: -c -C -h e afins...
* **Aprendi:**
  * Como cria chave pessoal e a chave publica; como conectar o git com o github pelo terminal; diferentes explicações para git branch, git merge e git commit.
* **Fluxo com branch:** criei a `docs/readme`, commitei o README nela, voltei para a `main` e fiz o merge. Depois apaguei a branch com `git branch -d`. O `git reflog` mostra cada passo.
* **Por que o gráfico ficou reto:** o merge foi *fast-forward*. A `main` não recebeu commit, por isso o git avançou direto para o commit mais recente, do readme na `main`. 
* **`git reflog`:** mostra o histórico de onde o `HEAD` esteve (trocas de branch, commits, merges), mesmo depois que a branch é apagada.
* **Linha final no arquivo:** é bom todo arquivo terminar com uma linha em branco. Sem ela, o GitHub mostra um ⛔ no diff. O `README.md` ainda está sem.
* **Semana 1 concluída:** sessões 1.1, 1.2 e 1.3 feitas, e o repositório SpawnCore está público no GitHub com o README.
