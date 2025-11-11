```mermaid
graph TB
    Browser["🌐 Navegador"]
    
    subgraph "101 Estoques System"
        FE["Frontend Container<br/>React + Vite<br/>Material-UI"]
        BFF["BFF Container<br/>Node.js + Express<br/>Orquestrador"]
        MSALG["MS Aluguéis<br/>Node.js + Express<br/>Sequelize"]
        MSEST["MS Estoques<br/>Node.js + Express<br/>Mongoose"]
        SQLDB["SQL Database<br/>SQL Server/SQLite<br/>Aluguéis"]
        MONGODB["MongoDB<br/>Estoques"]
    end
    
    Browser -->|HTTP| FE
    FE -->|REST/JSON| BFF
    BFF -->|REST| MSALG
    BFF -->|REST| MSEST
    MSALG -->|Query| SQLDB
    MSEST -->|Query| MONGODB
    
    style FE fill:#f3e5f5
    style BFF fill:#e8f5e9
    style MSALG fill:#fff9c4
    style MSEST fill:#fff9c4
    style SQLDB fill:#ffccbc
    style MONGODB fill:#ffccbc
```

## C4 Model - Nível 2: Container

**Escopo**: Arquitetura dos principais containers que compõem o sistema

### Containers Principais

#### 1. **Frontend Container**
- **Tecnologia**: React 18, Vite, Material-UI
- **Responsabilidade**: Interface visual, navegação, validação de entrada
- **Comunicação**: HTTP/REST com BFF
- **Deployment**: Firebase Hosting

#### 2. **BFF Container** (Backend For Frontend)
- **Tecnologia**: Node.js, Express
- **Responsabilidade**: Orquestração, agregação de dados, roteamento
- **Comunicação**: 
  - Recebe requisições do Frontend
  - Roteia para microserviços
- **Deployment**: Firebase Cloud Functions

#### 3. **Microserviço Aluguéis**
- **Tecnologia**: Node.js, Express, Sequelize ORM
- **Responsabilidade**: CRUD de aluguéis, validação de negócio
- **Persistência**: SQL Server (produção) / SQLite (dev)
- **Deployment**: Firebase Cloud Functions

#### 4. **Microserviço Estoques**
- **Tecnologia**: Node.js, Express, Mongoose
- **Responsabilidade**: CRUD de estoques, gerenciamento de inventário
- **Persistência**: MongoDB Atlas (produção) / Local (dev)
- **Deployment**: Firebase Cloud Functions

#### 5. **SQL Database**
- **Tipo**: Relacional (SQL Server / SQLite)
- **Dados**: Aluguéis, clientes, datas, valores
- **Acesso**: Apenas MS Aluguéis

#### 6. **MongoDB**
- **Tipo**: Documento (NoSQL)
- **Dados**: Estoques, produtos, quantidades, localizações
- **Acesso**: Apenas MS Estoques

### Fluxos de Dados
1. Usuário acessa Frontend → Vite carrega SPA
2. Frontend envia requisição → BFF recebe
3. BFF roteia → MS Aluguéis OU MS Estoques
4. Microserviço consulta → Banco específico
5. Resposta volta → Frontend atualiza tela
