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
| ID    | História                                                                 | Critérios de Aceite (BDD)                                                                                                                                                                | Prioridade | Sprint |
|-------|--------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------|
| US-01 | Como **cliente**, quero **abrir um chamado** para **obter suporte**      | **Dado** que estou autenticado **Quando** envio um formulário válido **Então** o ticket é criado com nº de protocolo, status **Novo** e registro no histórico                            | Alta      | S1     |
| US-02 | Como **cliente**, quero **listar e filtrar meus chamados**               | **Dado** que tenho tickets **Quando** acesso “Meus Chamados” **Então** vejo lista paginada, filtros por status/prioridade e posso abrir o detalhe                                         | Alta      | S1     |
| US-03 | Como **agente**, quero **entrar no sistema** para **atender tickets**    | **Dado** credenciais válidas **Quando** faço login **Então** acesso o painel do agente; **E** com inválidas recebo erro e não acesso                                                     | Alta      | S1     |
| US-04 | Como **agente**, quero **alterar status** para **controlar o fluxo**     | **Dado** um ticket **Quando** mudo de Novo→Em atendimento→Pendente→Resolvido **Então** a mudança é auditada no histórico e visível para cliente                                          | Alta      | S1     |
| US-05 | Como **agente**, quero **comentar e anexar arquivos** ao ticket          | **Dado** um ticket **Quando** adiciono comentário/anexo válido **Então** o item aparece na timeline; **E** com tipo/tamanho inválido recebo validação                                    | Alta      | S1     |
| US-06 | Como **gestor**, quero **definir políticas de SLA**                      | **Dado** filas/categorias **Quando** configuro tempos de 1ª resposta e resolução **Então** os prazos passam a ser aplicados a novos tickets                                              | Alta      | S2     |
| US-07 | Como **sistema**, quero **monitorar SLA e notificar violações**          | **Dado** um ticket com SLA **Quando** estiver a X min de violar **Então** enviar alerta ao agente e marcar como “Em risco”; **E** se violar, registrar ocorrência                        | Alta      | S2     |
| US-08 | Como **cliente**, quero **avaliar o atendimento (CSAT)**                 | **Dado** ticket Resolvido **Quando** recebo convite de avaliação **Então** posso dar nota/comentário; **E** o resultado fica salvo para relatórios                                       | Média     | S2     |
| US-09 | Como **agente**, quero **classificação automática (IA) de prioridade**   | **Dado** a descrição do ticket **Quando** criar/atualizar **Então** o sistema sugere prioridade/categoria; **E** posso aceitar/ajustar e isso é registrado                               | Média     | S2     |
| US-10 | Como **agente**, quero **pesquisar Base de Conhecimento**                 | **Dado** uma dúvida recorrente **Quando** pesquiso por termos **Então** recebo artigos relevantes; **E** consigo vincular artigo ao ticket                                               | Média     | S3     |
| US-11 | Como **gestor**, quero **dashboard de métricas**                          | **Dado** dados de operação **Quando** acesso o dashboard **Então** vejo TMR, TME, % SLA, reaberturas, volume por categoria/canal, produtividade por agente                               | Alta      | S3     |
| US-12 | Como **admin**, quero **perfis e permissões**                             | **Dado** papéis (cliente, agente, gestor, admin) **Quando** configuro permissões **Então** cada papel enxerga apenas o que é permitido e ações ficam auditadas                           | Alta      | S3     |


## DoR – Definition of Ready
- Critérios de aceite definidos  
- Escopo claro e dependências mapeadas  
- Design/Modelagem disponíveis (se aplicável)

## DoD – Definition of Done
- Código revisado e testado  
- Documentação atualizada (README/Docs/API)  
- Homologado e demonstrado

## Cronograma de Sprints
| Sprint | Período | Entregas/Docs |
|-------|---------|----------------|
| S1 | dd/mm – dd/mm | link |
| S2 | dd/mm – dd/mm | link |
| S3 | dd/mm – dd/mm | link |

## Tecnologias
- Frontend: _(ex: React/Next.js)_  
- Backend: _(ex: FastAPI/Node)_  
- Banco: _(ex: Postgres)_  
- Outros: CI/CD, Docker, etc.

## Manual de Instalação
- **Frontend:** ver `frontend/README.md`  
- **Backend:** ver `backend/README.md`  

## Equipe
- Nome – papel  
- Nome – papel
