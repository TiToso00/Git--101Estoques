```mermaid
graph TB
    User["👤 Usuários"]
    Company["🏢 Empresa de Logística"]
    
    User -->|Acessa| WebApp["🌐 Aplicação Web<br/>React + Vite"]
    
    WebApp -->|HTTP/REST| System["📦 Sistema 101 Estoques"]
    
    System -->|Gerencia| Inventory["📊 Estoques"]
    System -->|Registra| Rentals["🔄 Aluguéis"]
    
    Company -->|Utiliza| System
    
    style User fill:#e1f5ff
    style Company fill:#fff3e0
    style WebApp fill:#f3e5f5
    style System fill:#e8f5e9
    style Inventory fill:#fff9c4
    style Rentals fill:#ffe0b2
```

## C4 Model - Nível 1: Context

**Escopo**: Sistema 101 Estoques em seu contexto empresarial

### Atores Principais
1. **Usuário Final**: Consultor de logística ou gerente de estoque
2. **Empresa de Logística**: Cliente que utiliza o sistema
3. **Sistema 101 Estoques**: Aplicação central

### Relacionamentos
- Usuários acessam a aplicação web para gerenciar estoques e aluguéis
- Sistema fornece informações consolidadas sobre inventário e operações
- Empresa utiliza dados para tomar decisões operacionais

### Sistemas Externos
- (Futuros) Integração com SAP/ERP
- (Futuros) API de notificações (email/SMS)
- (Futuros) Análise de dados (BI)
