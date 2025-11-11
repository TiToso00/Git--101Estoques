# arc42 – 101 ESTOQUES

**Autores:** Henrique Etzel, Julio Cesar Ramalho, Victor Rosa, Alexandre Dominski
**Data:** 2025-11-10

---

## 1. Introdução e objetivos
- Sistema para gerenciar estoques e aluguéis, focado em empresas de logística.
- Escopo: CRUD de estoques, gestão de aluguéis, agregação via BFF.
- Objetivo: entrega rápida, modularidade e facilidade de manutenção.

## 2. Requisitos de qualidade (Quality Goals)
- Performance: latência média de listagens < 500ms.
- Escalabilidade: suportar aumento linear de requisições sem >20% degradação.
- Confiabilidade: disponibilidade alvo 99.5%.

## 3. Contexto (Scope and Context)
- Atores: Usuário Final (consultor/gerente), Empresa de Logística.
- Sistemas adjacentes previstos: ERP (SAP), serviços de notificação e BI.
- Frontend (React) interage com BFF; BFF orquestra microserviços.

## 4. Conteinerização / Containers (Solution Strategy)
- Frontend: React + Vite — serve UI (deploy: Firebase Hosting).
- BFF: Node.js/Express — orquestra, agrega APIs (deploy: Cloud Functions).
- MS Aluguéis: Node.js + Sequelize — persiste em SQL Server/SQLite.
- MS Estoques: Node.js + Mongoose — persiste em MongoDB (Atlas recomendado).
- DBs: SQL Server (Aluguéis), MongoDB Atlas (Estoques).

## 5. Componentes (Component view)
- Cada MS segue padrão: Controller → UseCases → Repository → Model.
- MS Aluguéis: AluguelController, AluguelUseCases, AluguelRepository, AluguelModel.
- MS Estoques: EstoqueController, EstoqueUseCases, EstoqueRepository, EstoqueModel.
- Cross-cutting: Logger, Error Handler, Validators.

## 6. Runtime / Cenário (Runtime scenarios)
Fluxo: criar aluguel (resumido)
1. Frontend POST /alugueis → BFF
2. BFF roteia para MS Aluguéis
3. AluguelController valida entrada
4. Controller chama CriarAluguelUseCase
5. UseCase aplica regras e chama Repository
6. Repository persiste no SQL Server via Sequelize
7. Retorno sobe até Frontend com 201 Created

## 7. Deployment view (Infraestrutura)
- Hosting atual: Firebase Hosting + Cloud Functions.
- Bancos: SQL Server (produção) / SQLite (dev) para aluguéis; MongoDB Atlas para estoques.
- Sugestão: migrar Functions para Azure Functions e usar Azure Service Bus para events.

## 8. Cross-cutting concepts
- Logging: centralizado via módulo `logger` (dev/production modes).
- Error handling: middleware central que formata HTTP errors.
- Validation: validators aplicados em Controllers; regras em UseCases.
- Event-driven: arquitetura esperada (EDA) — atual estado: não implementado.

## 9. Decisões arquiteturais (Architectural decisions)
- Usar microserviços por domínio para desacoplamento e deploy independente.
- Introduzir BFF para otimizar respostas ao frontend e agregação.
- Escolha de bancos: SQL para transações (alugueis), NoSQL para inventário (estoques).
- Hospedar frontend e functions em Firebase para deploy rápido inicial.

## 10. Riscos e mitigação
- Risco: inconsistência entre MSs — Mitigação: adotar mensagens/eventos assíncronos.
- Risco: latência inter-serviços — Mitigação: cache e chamadas assíncronas.
- Risco: limitação do Firebase em escala — Mitigação: migrar para Azure Functions/AKS.
- Risco: complexidade operacional — Mitigação: containerizar e criar CI/CD.

## 11. Requisitos não funcionais / Restrições
- Node.js 18+ obrigatório.
- Hospedagem inicial: Firebase (limites de uso).
- Equipe: 4 desenvolvedores; prazo semestral.
- Sem Kubernetes inicialmente; usar Cloud Functions / Docker.

## 12. Anexos / Diagramas
- Diagrams mermaid já disponíveis:
  - `C4_LEVEL_1_CONTEXT.md`
  - `C4_LEVEL_2_CONTAINER.md`
  - `C4_LEVEL_3_COMPONENT.md`
  - `C4_LEVEL_4_CODE.md`
- Renderize os arquivos mermaid para obter diagramas visuais.

---


