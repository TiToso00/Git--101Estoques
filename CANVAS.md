# CANVAS - 101 ESTOQUES

## 1. Business Case
Sistema para gerenciar estoques e aluguéis em tempo real, permitindo empresas de logística controlar inventário, registrar aluguéis de produtos e gerar relatórios de utilização.

## 2. Functional Overview
- Cadastro e gestão de estoques com controle de quantidade
- Sistema de aluguéis com datas de início e fim
- Listagem, atualização e exclusão de registros
- Visualização consolidada de dados via BFF
- Interface amigável para consultores e gerentes

## 3. Quality Goals
1. **Performance**: Resposta < 500ms para listagens
2. **Escalabilidade**: Suportar crescimento de dados sem degradação
3. **Confiabilidade**: 99.5% uptime em produção
4. **Manutenibilidade**: Código testável e bem documentado
5. **Segurança**: Validação de dados e proteção de endpoints

## 4. Architecture Hypotheses
- Microserviços reduzem acoplamento e facilitam deploy independente
- Separação de bancos por domínio (SQL para aluguéis, NoSQL para estoques) otimiza queries
- BFF centralizado melhora experiência do frontend
- Clean Architecture garante testabilidade e evolução sustentável

## 5. Technical Challenges & Risks

| Desafio | Risco | Mitigação |
|---------|-------|-----------|
| Consistência entre microserviços | Dados desincronizados | Event-driven communication |
| Latência de rede entre serviços | Degradação de performance | Cache + async operations |
| Complexidade operacional | Dificuldade em deploy e monitoring | Containerização + logs centralizados |
| Single Point of Failure no BFF | Indisponibilidade da aplicação | Load balancing + failover |

## 6. Organisational Constraints
- Equipe de 4 desenvolvedores (Henrique, Julio, Victor, Alexandre)
- Prazo de entrega definido (semestral)
- Conhecimento em Node.js e React consolidado
- Stack JavaScript/TypeScript padrão

## 7. Technical Constraints
- Hospedagem em Firebase (custo e limites da plataforma)
- Bancos de dados: SQL Server / SQLite + MongoDB
- Node.js 18+ obrigatório
- Sem acesso a Kubernetes inicialmente (Cloud Functions)
- Rate limiting do Firebase (100 requisições simultâneas)

## 8. Business Context
**Usuários**: Consultores de logística, Gerentes de estoque, Administradores
**Concorrentes**: Sistemas ERP complexos (SAP, Oracle), Soluções cloud (AWS, Azure)
**Diferencial**: Simples, rápido, focado em micro-negócios

