# Diagramas do Sistema: Electrocode OS

Visualização técnica de fluxos e estruturas do **Electrocode OS**.

---

## 1. Fluxo de Requisição (Request Pipeline)

Processamento de requisições do frontend até a persistência via proxy reverso.

```mermaid
graph TD
    User([Usuário Final]) -->|Vê/Interage| Frontend
    
    subgraph Infrastructure[Infraestrutura VPS]
        Nginx{Nginx Proxy}
        Frontend[React SPA]
        Backend[Node.js API]
        DB[(MySQL)]
    end

    Frontend -->|Chamada API / REST| Nginx
    Nginx -->|Route Proxy| Backend
    Backend -->|Sequelize ORM Query| DB
    DB -->|Data| Backend
    Backend -->|JSON Response| Nginx
    Nginx -->|Response| Frontend
```

---

## 2. Modelo de Dados Simplificado (ER Diagram)

Estrutura relacional para suporte a multi-tenancy e rastreabilidade.

```mermaid
erDiagram
    TENANT ||--o{ USER : "gerencia usuários"
    TENANT ||--o{ CUSTOMER : "atende clientes"
    TENANT ||--o{ SERVICE_ORDER : "processa S.Os"
    
    SERVICE_ORDER }|--o| CUSTOMER : "pertence a"
    SERVICE_ORDER ||--o{ PARTS_USED : "consoma itens"
    SERVICE_ORDER ||--o{ LABOR : "inclui mão de obra"
    SERVICE_ORDER ||--o| INVOICE : "gera financeiro"

    USER }|--|| ROLES : "possui permissão"
```

---

## 3. Fluxo de Ciclo de Vida da O.S. (Workflow)

Controle de status do ciclo de vida das ordens de serviço.

```mermaid
stateDiagram-v2
    [*] --> Aberta : Entrada de Equipamento
    Aberta --> Orcamento : Análise Técnica
    Orcamento --> Aprovada : Aceite do Cliente
    Orcamento --> Recusada : Cliente não aceitou
    Aprovada --> EmReparo : Execução
    EmReparo --> Finalizada : Testes de Qualidade
    Finalizada --> Entregue : Retirada do Cliente
    Recusada --> Entregue : Devolução s/ Reparo
    Entregue --> [*]
```

---

 **Erasmo Cardoso**
Electrocode

