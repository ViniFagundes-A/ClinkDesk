<img width="500" height="500" alt="clickdesk-logo" src="https://github.com/user-attachments/assets/00a3687d-736f-41e4-be90-d0a09eed3c94" />

# Click-Desk

> **Status:** Em andamento ⏳  
> **Relatórios/Docs/Vídeos:**  
> - **Relatório de Testes (PDF):** _(link aqui)_  
> - **Pasta de Documentação:** _(link aqui)_  
> - **Vídeo de Apresentação:** _(link aqui)_

---

## Desafio
Pequenas e médias empresas costumam atender clientes por canais dispersos (e-mail, WhatsApp, telefone) sem um processo único de registro, priorização e resolução. Isso gera:
- falta de rastreabilidade dos atendimentos e perda de histórico;
- dificuldade de cumprir e medir **SLA** (tempo de resposta e de resolução);
- ausência de indicadores confiáveis (volume por canal, backlog, motivos de reabertura, satisfação);
- pouca padronização de respostas e repetição de trabalho por falta de **base de conhecimento**;
- custos elevados e curva de aprendizado de ferramentas consolidadas do mercado;
- dificuldade de escalar o suporte mantendo qualidade e previsibilidade.

O desafio é entregar uma experiência de suporte organizada, mensurável e acessível — sem a complexidade/custo de plataformas enterprise — permitindo que o time enxergue prioridades, cumpra prazos e aprenda com os dados.

## Solução
**Clickdesk** é um **Helpdesk** moderno que centraliza os chamados e padroniza o ciclo de atendimento de ponta a ponta:

- **Central de Tickets:** criação por portal do cliente, e-mail e (futuro) WhatsApp/Chat; campos personalizados, categorias, anexos e marcação de prioridade.
- **SLA & Regras:** políticas de SLA por fila/cliente, contagem de tempo útil, alertas de violação e escalonamento automático.
- **Filas e Workflows:** roteamento por equipe/skill, estados do ticket (novo, em atendimento, pendente, resolvido), macros, automações e gatilhos.
- **Base de Conhecimento:** artigos pesquisáveis para agentes e clientes, reduzindo chamados repetitivos.
- **Portal do Cliente:** abertura/consulta de chamados e status em tempo real, com CSAT/NPS no fechamento.
- **Dashboards & Métricas:** tempo médio de 1ª resposta e resolução, tickets por canal/motivo, produtividade por agente, violação de SLA e reaberturas.
- **Perfis e Permissões:** papéis (agente, líder, admin) com auditoria de ações.
- **Integrações iniciais:** e-mail (IMAP/SMTP) e Webhooks/API para CRM/ERP; roadmap para WhatsApp/Telegram.
- **Arquitetura acessível:** pensada para PMEs — implantação simples, custos previsíveis e UX focada em rapidez do agente.

## Arquitetura do Projeto

Este repositório é um **meta-repo** que agrega os serviços via **submódulos**:

- **Frontend:** `./frontend` _(submódulo)_  
  SPA consumindo a API (ex.: React/Next.js). Responsável por abertura/consulta de chamados, painel do agente e portal do cliente.

- **Backend:** `./backend` _(submódulo)_  
  API (ex.: FastAPI/Node) com regras de negócio, autenticação/autorização, gestão de SLA, histórico e integrações.

- **Módulo de IA (roadmap):** classificação automática de prioridade/categoria e sugestões de resolução com base no histórico/FAQ.

- **Banco de Dados:** SQL relacional (ex.: MS SQL Server) para usuários, chamados, categorias, status, histórico, anexos e feedbacks.

- **Notificações/Integrações:** e-mail e webhooks/API para integração com ferramentas externas (CRM/ERP etc.).

- **Observabilidade:** métricas (TMR/TME, SLA cumprido, reaberturas), logs e auditoria por protocolo de chamado.

> (Opcional) Diagramas, decisões e ADRs em `./docs/`.

## Backlog do Produto

| ID    | História (quem/quer/para)                                      | Aceite (curto)                                                                    | Pri | Sprint |
|------:|-----------------------------------------------------------------|-----------------------------------------------------------------------------------|:--:|:-----:|
| US-01 | **Cliente** quer **abrir chamado** para **receber suporte**     | Cria ticket com nº/protocolo, status **Novo** e validações básicas               | 🔥 |  S1   |
| US-02 | **Cliente** quer **ver/filtrar chamados** para **acompanhar**   | Lista paginada, filtros por status/prioridade e detalhe do ticket                 | 🔥 |  S1   |
| US-03 | **Agente** quer **login** para **acessar painel**               | Autentica, trata erro de credencial e direciona para painel do agente             | 🔥 |  S1   |
| US-04 | **Agente** quer **mudar status** para **controlar fluxo**       | Transições: Novo→Em atendimento→Pendente→Resolvido com histórico/auditoria        | 🔥 |  S1   |
| US-05 | **Agente** quer **comentar/anexar** para **contexto do ticket** | Anexos válidos, comentários na timeline e bloqueio de tipos/tamanhos inválidos    | 🔥 |  S1   |
| US-06 | **Gestor** quer **configurar SLA** para **garantir prazos**     | Tempos de 1ª resposta e resolução por fila/categoria aplicados a novos tickets    | ⭐ |  S2   |
| US-07 | **Sistema** quer **alertar SLA** para **evitar violação**       | Marca “em risco” e notifica antes do prazo; registra violações                    | ⭐ |  S2   |
| US-08 | **Cliente** quer **avaliar (CSAT)** para **medir qualidade**    | Envio de pesquisa no fechamento; guarda nota/comentário                           | ⭐ |  S3   |
| US-09 | **Agente** quer **sugestão IA** para **priorizar rapidamente**  | Sugere prioridade/categoria; agente pode aceitar/ajustar e registrar decisão      | ✔️ |  S3   |
| US-10 | **Gestor** quer **dashboard** para **acompanhar operação**      | Exibe TMR, TME, %SLA, reaberturas, volume e produtividade por agente              | 🔥 |  S3   |

**Legenda:** Pri = 🔥 Alta · ⭐ Média · ✔️ Baixa



## ## DoR – Definition of Ready

Uma história está **PRONTA** para entrar na sprint quando atende a todos os itens abaixo:

- [ ] **Critérios de Aceite** escritos em BDD (Dado/Quando/Então) e sem ambiguidades
- [ ] **Escopo Claro** (fora/escopo explicitado) e **dependências** mapeadas
- [ ] **Valor de Negócio** e **prioridade** definidos; impacto alinhado ao objetivo da sprint
- [ ] **Design/Modelagem** disponíveis (telas, fluxos, DER/API) quando aplicável
- [ ] **Regras de Negócio** e **validações** documentadas (incl. estados/status)
- [ ] **Dados/Integrações** especificados (campos, contratos de API, mensagens/filas)
- [ ] **Critérios Não Funcionais** (perf, segurança/LGPD, acessibilidade) acordados
- [ ] **Testes** planejados (unitários/integração/aceitação) e dados de teste definidos
- [ ] **Estimativa** feita pela equipe e **risco** conhecido (assunções/mitigações)
- [ ] **Pronto para Deploy**: estratégia/rollback definidos quando relevante

## DoD – Definition of Done

Uma história está **CONCLUÍDA** quando cumpre **todos** os itens:

- [ ] **Critérios de Aceite** atendidos e aprovados (PO/parte interessada)
- [ ] **Código revisado** (1+ code review), **CI verde**, lint/format aplicado
- [ ] **Testes** unitários/integração/contrato passando (cobertura ≥ X%)
- [ ] **Segurança/LGPD**: sem exposição de dados sensíveis; segredos seguros
- [ ] **Performance & Acessibilidade** dentro do mínimo acordado
- [ ] **Logs/Monitoramento** e métricas adicionados (smoke/health check)
- [ ] **Documentação** atualizada (README, API/OpenAPI, CHANGELOG)
- [ ] **Migrações de BD** aplicadas e reversíveis (rollback testado)
- [ ] **Feature flag/fallback** definido (quando aplicável)
- [ ] **Homologado** em ambiente de testes e **aprovado** pelo negócio
- [ ] **Deploy** realizado/verificado **ou** pacote pronto para release
- [ ] **Métrica de sucesso**/tracking implementados (telemetria de uso)


## Cronograma de Sprints (resumido)

| Sprint | Período                   | Foco/Entregas (resumo)                                           | Link |
|:-----:|----------------------------|------------------------------------------------------------------|:----:|
| S1    | 19/08/2025 – 31/08/2025    | Fundações: GitHub/meta-repo, docs iniciais, diagramas, scaffolds, BD base | [Adicionar link]() |
| S2    | 01/09/2025 – 13/09/2025    | Fluxo core: login, abrir ticket, listar/filtrar meus chamados   | [Adicionar link]() |
| S3    | 14/09/2025 – 26/09/2025    | Detalhe do ticket, status/fluxo, anexos, histórico              | [Adicionar link]() |
| S4    | 27/09/2025 – 09/10/2025    | SLA: configuração, contagem de prazos, alertas; e-mail básico   | [Adicionar link]() |
| S5    | 10/10/2025 – 22/10/2025    | CSAT, Base de Conhecimento (MVP), webhooks/API; tuning de BD    | [Adicionar link]() |
| S6    | 23/10/2025 – 04/11/2025    | IA (prioridade/categoria), permissões/perfis, dashboard inicial | [Adicionar link]() |
| S7    | 05/11/2025 – 15/11/2025    | Hardening, testes/observabilidade, homologação, vídeo/entrega   | [Adicionar link]() |


## Tecnologias

- **Frontend (Web):** React + Next.js  
  _Opcional:_ Tailwind CSS, Zustand/Redux, Axios/React Query  
  _Mobile (roadmap):_ React Native  
  _Desktop (roadmap):_ Electron

- **Backend (API):** Python + FastAPI  
  _Extras:_ Pydantic, Uvicorn/Gunicorn, SQLAlchemy, Alembic (migrações)  
  _Docs:_ OpenAPI/Swagger (auto)

- **Banco de Dados:** Microsoft SQL Server  
  _Suporte:_ Migrations (Alembic), índices/views para métricas

- **Cache & Filas (opcional):** Redis (cache, rate limiting, sessões), RQ/Celery (jobs)  
  _Alternativa Node:_ BullMQ (se usar Node)

- **Autenticação & Segurança:** JWT (access/refresh), RBAC (perfis), CORS, .env/Secrets

- **Observabilidade:** Logs estruturados, métricas (Prometheus), dashboards (Grafana)

- **Integrações:** SMTP/IMAP (e-mail), Webhooks, API pública (tokens)

- **Qualidade & Testes:** Pytest (unit/integração), Coverage, Lint/Format (ruff/black)

- **DevOps:** Docker + Docker Compose, GitHub Actions (CI/CD), versionamento semântico  
  _Ambientes:_ Dev / Homolog / Prod

> Links para referências (adicione depois):  
> - Frontend: [Repo Frontend]()  
> - Backend: [Repo Backend]()  
> - Docs/API: [Swagger/OpenAPI]()  
> - Infra/DevOps: [Pipelines CI/CD]()  


## Manual de Instalação
- **Frontend:** ver `frontend/README.md`  
- **Backend:** ver `backend/README.md`  

## Equipe

- **André Luis dos Santos Barbosa** — Product Owner / Gestão do Projeto  
- **Kaique Loamir Siqueira Uchôa** — QA & Documentação / Suporte ao Frontend  
- **Vinicius de Andrade Fagundes** — Analista de Dados / Observabilidade  
- **Erika Aparecida Cordeiro** — Tech Lead / Backend

> (Opcional) Adicione links depois: [GitHub]() · [LinkedIn]()

