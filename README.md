# 101 ESTOQUES - Sistema de Gestão de Estoques e Aluguéis

**Alunos**: Henrique Etzel, Julio Cesar Ramalho, Victor Rosa, Alexandre Dominski

## 📋 Visão Geral

Aplicação de gestão de estoques e aluguéis em arquitetura de microserviços com Clean Architecture e Vertical Slice.

## 🏗️ Arquitetura

### Componentes Principais
- **Frontend**: React 18 + Vite + Material-UI
- **BFF**: Node.js/Express - Orquestração de microserviços
- **Microserviço Aluguéis**: Node.js + Sequelize + SQL Server/SQLite
- **Microserviço Estoques**: Node.js + Mongoose + MongoDB
- **Hosting**: Firebase (Frontend, BFF, Cloud Functions)

### Padrões Utilizados
- **Clean Architecture**: Separação clara de camadas (Domain, Application, Infrastructure, Interfaces)
- **Vertical Slice Architecture**: Features isoladas (aluguel, estoque)
- **Repository Pattern**: Abstração de persistência
- **Use Cases**: Lógica de negócio desacoplada

### Estrutura de Pastas (por feature)
```
features/
├── aluguel/
│   ├── aluguelController.js     (Interfaces)
│   ├── aluguelUseCases.js       (Application)
│   ├── aluguelRepository.js     (Infrastructure)
│   ├── aluguelRoutes.js         (Routes)
│   └── index.js
└── estoque/
    ├── estoqueController.js     (Interfaces)
    ├── estoqueUseCases.js       (Application)
    ├── estoqueRepository.js     (Infrastructure)
    ├── estoqueRoutes.js         (Routes)
    └── index.js
```

## 🚀 Como Rodar

### Pré-requisitos
- Node.js 18+
- MongoDB (local ou Atlas)
- SQL Server / SQLite

### Setup Local

**1. Frontend**
```bash
cd microfrontend
npm install
npm run dev
```

**2. BFF**
```bash
cd functions/bff-node
npm install
npm run dev
```

**3. Microserviço Aluguéis**
```bash
cd functions/microservice-alugueis
npm install
npm run dev
```

**4. Microserviço Estoques**
```bash
cd functions/microservice-estoques
npm install
npm run dev
```

## 📊 Tecnologias

| Camada | Tecnologia |
|--------|-----------|
| Frontend | React 18, Vite, Material-UI, React Router |
| BFF | Express.js, Axios |
| Backend | Express.js, Sequelize, Mongoose |
| BD | SQL Server / SQLite, MongoDB |
| Deploy | Firebase, Cloud Functions |

## 🔗 Endpoints

### BFF (localhost:3000)
- `GET /alugueis` - Listar aluguéis
- `POST /alugueis` - Criar aluguel
- `GET /estoques` - Listar estoques
- `POST /estoques` - Criar estoque

### MS Aluguéis (localhost:3002)
- `GET /api/alugueis`
- `POST /api/alugueis`
- `PUT /api/alugueis/:id`
- `DELETE /api/alugueis/:id`

### MS Estoques (localhost:3001)
- `GET /api/estoques`
- `POST /api/estoques`
- `PUT /api/estoques/:id`
- `DELETE /api/estoques/:id`

## 🧪 Testes

```bash
# Executar testes (em cada microserviço)
npm test

# Com cobertura
npm test -- --coverage
```

## 📦 Deploy

```bash
# Firebase
firebase deploy

# Docker (cada microserviço)
docker build -t ms-alugueis .
docker run -p 3002:3002 ms-alugueis
```

## 📚 Documentação Adicional

- [C4 Model - Nível 1 (Context)](./C4_LEVEL_1_CONTEXT.md)
- [C4 Model - Nível 2 (Container)](./C4_LEVEL_2_CONTAINER.md)
- [C4 Model - Nível 3 (Component)](./C4_LEVEL_3_COMPONENT.md)
- [Canvas Architecture](./CANVAS.md)
