# 📊 Diagramas do Sistema: Electrocode OS

Este documento apresenta a visualização técnica dos fluxos e estruturas que compõem o ecossistema do **Electrocode OS**.

---

## 1. Fluxo de Requisição (Request Pipeline)

O diagrama abaixo ilustra como as requisições dos usuários são processadas, desde a interface frontend até a persistência no banco de dados, através da camada de proxy reverso.

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

A estrutura relacional foi projetada para suportar alta granularidade de permissões e rastreabilidade total de cada item físico ou financeiro.

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

O fluxo de negócio implementado permite o controle rígido do status de cada equipamento em manutenção.

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

### Notas Técnicas:
1. **Segurança**: Todas as comunicações entre Nginx, Backend e Frontend são protegidas por criptografia SSL/TLS em ambientes de produção.
2. **Separação de Dados**: O sistema utiliza o conceito de Multi-Tenancy (baseado em IDs de empresa), garantindo que dados de diferentes empresas jamais se cruzem.
3. **Escalabilidade**: Os componentes dentro da VPS podem ser distribuídos para múltiplos nós caso a carga de usuários aumente excessivamente.

**Erasmo Cardoso**
Analista Desenvolvedor de Sistemas | Electrocode
