# Painel de Servidores — Documento do Projeto

> Nome provisório. Criado em 19/10/2026.

## 1. Por que este projeto existe

Aprender, construindo um único sistema real, tudo o que um dev **back-end júnior** precisa saber, com foco em **infraestrutura** (caminho para DevOps/SRE). O resultado deve:

- ser usado de verdade por amigos e conhecidos;
- ficar público no GitHub como portfólio ("chamariz" para recrutadores);
- ser explicável em entrevista: cada decisão tem um porquê.

**Ponto de partida:** sei o básico e um pouco de lógica de programação. Ainda não sei TypeScript.

## 2. O que o sistema faz

Uma plataforma para **criar, ligar, desligar e monitorar servidores de jogo** que rodam em containers Docker numa VPS, no estilo do Pterodactyl/Aternos.

**Versão 1 (meta dos ~8 meses):**

- Cadastro e login de usuários.
- Criar um servidor de **Minecraft** (nome, versão, memória).
- Ligar, desligar, reiniciar e excluir o servidor.
- Ver status (ligado/desligado), uso de CPU e RAM.
- Ver o console ao vivo e enviar comandos.
- Permissões: o dono convida amigos para controlar o servidor dele.
- Backups automáticos do mundo.
- Duas interfaces: **painel web** e **bot do Discord**, ambas usando a mesma API.
- Alertas no Discord quando um servidor cai.

**Fora da versão 1 (fica para a "v2", se eu quiser continuar):**

- Outros jogos (Terraria, Valheim, CS2).
- Vários servidores físicos (VPS) gerenciados ao mesmo tempo.
- Kubernetes.
- Cobrança, planos pagos e cadastro aberto ao público.

## 3. Stack

| Parte | Ferramenta | Por quê |
|---|---|---|
| Linguagem | TypeScript (Node.js) | Uma linguagem para API, painel e bot; muitas vagas júnior |
| API | Fastify | Simples, rápido, boa documentação |
| Banco | PostgreSQL + Prisma | SQL de verdade, padrão de mercado; Prisma facilita migrações |
| Controle do Docker | dockerode | Biblioteca Node para falar com o Docker |
| Painel web | React + shadcn/ui | Componentes prontos, pouco CSS para escrever |
| Bot | discord.js | A biblioteca de bot mais madura |
| Testes | Vitest | Rápido e simples |
| Infra | Docker, Docker Compose, Caddy (HTTPS) | Rodar tudo igual no PC e na VPS |
| CI/CD | GitHub Actions | Testar e publicar a cada push |
| Observabilidade | Prometheus + Grafana | Métricas e gráficos padrão de mercado |

## 4. Arquitetura

```
  [Painel web (React)]      [Bot do Discord]
            \                     /
             \     HTTP/JSON     /
              v                 v
            [ API (Fastify) ] ----> [ PostgreSQL ]
                    |
                    | dockerode (socket do Docker)
                    v
            [ Docker na VPS ]
              ├─ mc-servidor-1 (container Minecraft)
              └─ mc-servidor-2 (container Minecraft)
```

**Regra principal:** só a API fala com o banco e com o Docker. O painel e o bot são "clientes burros", que apenas chamam a API. Assim, uma regra (por exemplo, "só o dono pode excluir") existe num lugar só.

**Organização do repositório** (um repositório com várias partes):

```
projeto-servidores/
├─ apps/
│  ├─ api/     ← back-end (o coração do projeto)
│  ├─ web/     ← painel React
│  └─ bot/     ← bot do Discord
├─ infra/      ← docker-compose, Caddy, Prometheus, Grafana
└─ docs/       ← este documento, diário, decisões
```

## 5. Dados principais (primeira versão do modelo)

- **Usuário:** id, nome, e-mail, senha (guardada como hash), data de criação.
- **Servidor:** id, nome, jogo, versão, memória (MB), porta, status, id do container, dono.
- **Membro:** qual usuário pode mexer em qual servidor, e com qual papel (dono, operador, visualizador).
- **Backup:** id, servidor, arquivo, tamanho, data.

O modelo vai mudar ao longo do projeto, e tudo bem: cada mudança vira uma *migração* do Prisma.

## 6. Como um pedido funciona (exemplo: ligar servidor)

1. O usuário clica em "Ligar" no painel ou digita `/start meu-mundo` no Discord.
2. O cliente chama `POST /servers/:id/start` com o token de login.
3. A API confere: o token é válido? O usuário tem permissão nesse servidor?
4. A API pede ao Docker para iniciar o container e atualiza o status no banco.
5. A API responde, e o cliente mostra "Ligando..." até o status virar "Ligado".

**Erros que precisam de resposta clara:** sem login (401), sem permissão (403), servidor não existe (404), dados inválidos (400), Docker fora do ar ou falta de memória na VPS (503, com mensagem explicando).

## 7. Testes

- **Unitários:** regras puras (por exemplo, quem pode fazer o quê).
- **Integração:** rotas da API com um banco de teste.
- **Docker nos testes:** o acesso ao Docker fica atrás de uma interface, para que os testes usem uma versão falsa e não precisem subir Minecraft de verdade.
- Os testes rodam no GitHub Actions a cada push (a partir da fase 7).

## 8. Fases

Ritmo: 5 a 10h por semana, cerca de 35 semanas no total. Cada fase termina com **algo funcionando**.

| # | Fase | Semanas | Entrega no fim |
|---|---|---|---|
| 1 | Fundamentos: Git, terminal Linux, TypeScript, HTTP | ~4 | Script em TS que liga e desliga um container Minecraft |
| 2 | API e banco | ~6 | API REST com PostgreSQL controlando servidores de verdade |
| 3 | Usuários e segurança | ~3 | Login, senhas com hash, permissões por servidor, validação de dados |
| 4 | Testes | ~2 | Testes automatizados cobrindo as rotas principais |
| 5 | Painel web | ~4 | Painel React simples. **Primeira versão para os amigos** |
| 6 | Docker e deploy | ~3 | Tudo em containers na VPS, com domínio e HTTPS |
| 7 | CI/CD | ~2 | GitHub Actions testa e publica sozinho |
| 8 | Bot do Discord | ~3 | `/start`, `/stop`, `/status` usando a mesma API |
| 9 | Tempo real e tarefas em segundo plano | ~3 | Console ao vivo, fila de tarefas, backups automáticos |
| 10 | Observabilidade | ~3 | Logs, métricas de CPU e RAM, alertas no Discord |
| 11 | Acabamento de portfólio | ~2 | README com arquitetura, documentação da API, demo gravada |

As semanas são estimativas. Atrasar uma fase não é falha; pular uma fase é.

## 9. Regras de constância

O maior risco deste projeto não é técnico: é parar no meio. Por isso:

1. **Dias e horários fixos.** Combinar comigo mesmo, por exemplo, 3 blocos de 2 a 3h nos mesmos dias, toda semana.
2. **Toda sessão termina com um commit.** Mesmo pequeno. Os commits são meus: é o registro da minha jornada.
3. **Entrega semanal pequena.** Cada semana tem uma meta do tipo "algo que roda", não "estudar o capítulo X".
4. **Regra do mínimo.** Em semana ruim, 20 minutos contam. O que quebra o hábito é zerar a semana.
5. **Diário em `docs/DIARIO.md`.** Duas ou três linhas por sessão: o que fiz, o que travou, o que aprendi.
6. **Sem trocar de linguagem ou stack** até terminar a versão 1. Dúvidas viram anotação no diário, não mudança de rumo.

## 10. Como saber que deu certo

- Pelo menos 3 amigos usaram o painel ou o bot para jogar.
- O repositório tem README claro, testes passando no CI e deploy automático.
- Consigo explicar em entrevista, sem colar, como um pedido sai do Discord e liga um container.
- O diário mostra constância: sessões registradas na maioria das semanas.
