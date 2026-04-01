# 🏗️ Arquitetura de Software: Electrocode OS

Este documento detalha as decisões arquiteturais e de engenharia aplicadas no desenvolvimento do **Electrocode OS**, demonstrando a solidez técnica por trás de uma aplicação de gestão enterprise.

---

## 1. Visão Geral da Arquitetura

O sistema utiliza uma arquitetura **Client-Server** desacoplada, com um Frontend Single Page Application (SPA) e um Backend RESTful API, orquestrados via **Docker**.

### Modelagem de Dados (MySQL)
A escolha do MySQL como banco de dados relacional foi estratégica devido à natureza transacional do sistema (Ordens de Serviço, Financeiro e Estoque).
- **Integridade Referencial**: Uso de FKs rigorosas para evitar inconsistências em deletação de clientes/OS.
- **Performance**: Indexação otimizada para buscas rápidas em grandes volumes de históricos de serviço.
- **Sequelize ORM**: Camada de abstração que garante segurança contra SQL Injection e agilidade no desenvolvimento.

---

## 2. Backend Engine (Node.js & Express)

O backend segue o padrão **MVC (Model-View-Controller)**, com uma camada adicional de **Services** para isolar a lógica de negócio pesada dos controladores.

### Pilares do Backend:
- **Middleware-First**: Implementação de pipeline de segurança com `cors`, `helmet`, `express-rate-limit` e logs estruturados.
- **JWT Authentication**: Sistema de tokens com expiração configurável e extração de claims para controle de `RBAC`.
- **Backup Pipeline**: Um subsistema dedicado que compacta os dados (JSON) e arquivos de uma empresa específica em formato ZIP para download imediato pelo Admin.

---

## 3. Frontend (React & Material-UI)

O frontend foi projetado para ser uma ferramenta de trabalho rápida e intuitiva.

### Destaques Técnicos:
- **Design System via MUI**: Customização profunda do tema Material-UI para refletir a marca Electrocode, garantindo consistência visual em todos os módulos.
- **State Management**: Uso estratégico de `Context API` para estados globais como autenticação de usuário e configurações da empresa.
- **Responsividade**: Interface 100% responsiva (Mobile/Tablet/Desktop), permitindo que técnicos consultem ordens diretamente no celular enquanto realizam manutenções.

---

## 4. Infraestrutura e Deployment

O sistema é entregue como uma solução **Containerized**, o que permite alta portabilidade.

### Fluxo de Deployment:
1. **Nginx**: Atua como Proxy Reverso e servidor de arquivos estáticos, além de gerenciar certificados SSL/TLS.
2. **Docker Compose**: Orquestra três containers principais: `frontend`, `backend` e `mysql`.
3. **VPS Monitoring**: Um dos diferenciais é o painel de monitoramento em tempo real (exclusivo para Superadmin), que coleta métricas via comandos shell do sistema (`df`, `os_stats`) e Docker API (`docker stats`), apresentando gráficos de consumo de CPU/RAM/Disco.

---

## 5. Decisões de Engenharia (Why?)

- **MVC vs Microservices**: Para o estágio atual e escala do projeto, uma arquitetura monolítica modular (Modular Monolith) sob MVC provê menor latência e maior facilidade de manutenção.
- **Docker**: Escolhido para eliminar o problema de "funciona na minha máquina", permitindo deploys consistentes em qualquer VPS Linux sem necessidade de instalar dependências manualmente no host.
- **PWA Capabilities**: Adicionadas para permitir que o sistema seja "instalado" no desktop do usuário como um aplicativo nativo, melhorando o engajamento.

---

> [!CAUTION]
> As informações contidas aqui são de caráter descritivo para fins de portfólio. Detalhes de implementação específica de rotas e credenciais são confidenciais.

**Erasmo Cardoso**
Analista Desenvolvedor de Sistemas | Electrocode
