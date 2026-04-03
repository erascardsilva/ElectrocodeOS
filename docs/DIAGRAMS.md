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
    [*] --> Garantia : Entrada em Garantia
    
    Aberta --> EmAnalise
    Garantia --> EmAnalise
    
    EmAnalise --> OrcamentoGerado
    OrcamentoGerado --> AguardandoAprovacao
    
    AguardandoAprovacao --> Aprovado : Cliente Aceitou
    AguardandoAprovacao --> Reprovado : Cliente Recusou
    
    Aprovado --> AguardandoPecas
    Aprovado --> EmReparo
    
    AguardandoPecas --> EmReparo
    
    EmReparo --> ProntoAvisar : Testes de Qualidade OK
    ProntoAvisar --> ProntoAguardando : Comunicação Enviada
    
    ProntoAguardando --> Finalizado : Entrega Comum
    ProntoAguardando --> FinalizadoFaturado : Entrega com Faturamento
    
    Reprovado --> FinalizadoReprovado : Devolução Recusada
    
    Finalizado --> [*]
    FinalizadoFaturado --> [*]
    FinalizadoReprovado --> [*]

    state "Em Análise" as EmAnalise
    state "Orçamento Gerado" as OrcamentoGerado
    state "Aguardando Aprovação" as AguardandoAprovacao
    state "Aguardando Peças" as AguardandoPecas
    state "Em Reparo" as EmReparo
    state "Pronto avisar cliente" as ProntoAvisar
    state "Pronto aguardando cliente" as ProntoAguardando
    state "Finalizado Faturado" as FinalizadoFaturado
    state "Finalizado Reprovado" as FinalizadoReprovado
```

---

## 4. Diagrama de Casos de Uso (MVP 2 - RBAC & Funcionalidades)

Representação das interações entre os atores do sistema e as funcionalidades de gestão Core e Multitenant.

```mermaid
graph LR
    subgraph Atores
        SAdmin([Superadmin Electrocode])
        CAdmin([Admin Empresa])
        Staff([Técnico/Equipe])
        System((Sistema/JWT))
    end

    subgraph "Funcionalidades (MVP 2)"
        UC1(Gerir Empresas/Tenants)
        UC2(Verificar Pagamentos)
        UC3(Login/JWT Auth)
        UC4(Gestão O.S. - Kanban/Trello)
        UC5(CRUD Clientes)
        UC6(Controle de Estoque)
        UC7(Financeiro - Vendas/Gastos/Recibos)
        UC8(Configurar Equipe/Dados)
        UC9(Dashboards/Gráficos)
    end

    SAdmin --> UC1
    SAdmin --> UC2
    
    CAdmin --> UC3
    CAdmin --> UC4
    CAdmin --> UC5
    CAdmin --> UC6
    CAdmin --> UC7
    CAdmin --> UC8
    CAdmin --> UC9

    Staff --> UC3
    Staff --> UC4
    Staff --> UC5
    Staff --> UC6

    System -.->|Valida Token| UC3
    System -.->|Calcula| UC9
```

---

 **Erasmo Cardoso**
Electrocode

