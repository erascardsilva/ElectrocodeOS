# Electrocode OS: Gestão para Assistência Técnica

![Electrocode OS Logo](docs/assets/logo.png)

**Electrocode OS** é um sistema de gestão para empresas de assistência técnica, laboratórios de eletrônica e prestadores de serviços. Concebido com arquitetura escalável para eficiência operacional.

---

## Visão Geral do Projeto

Este repositório serve como uma **Documentação de Referência e Estudo de Caso (Showcase)** para o sistema Electrocode OS. O código-fonte original é mantido de forma privada por questões estratégicas e comerciais da **Electrocode**.

### O Problema que Resolvemos
Assistências técnicas enfrentam desafios críticos como desorganização de ordens de serviço, perda de prazos, falta de controle de estoque de peças e comunicação ineficiente com o cliente. O Electrocode OS centraliza essas operações em uma plataforma única, segura e baseada em nuvem.

---

## Stack Tecnológica

Tecnologias utilizadas no projeto:

- **Frontend**: `React.js` + `Material-UI (MUI)`
- **Backend**: `Node.js` (Arquitetura RESTful)
- **Banco de Dados**: `MySQL` (Modelagem Relacional com Sequelize)
- **Infraestrutura**: `Docker` + `Nginx` (Proxy Reverso)
- **Segurança**: Autenticação em estágios via `JWT` e controle de acesso baseado em papéis (`RBAC`).

---

## Funcionalidades e Recursos

Principais módulos do **Electrocode OS**:

### Gestão de Ordens de Serviço (O.S)
- **Ciclo Completo**: Acompanhamento desde a entrada do equipamento, orçamento, aprovação, execução até a entrega final.
- **Relatórios de O.S**: Geração de relatórios detalhados com histórico de reparo e termos de garantia.
- **Checklists Personalizados**: Criação de até 5 modelos de checklist (com até 15 itens cada) para garantir o padrão de qualidade.
- **Etiquetas de Identificação**: Geração e impressão de etiquetas para organização física dos aparelhos no laboratório.
- **Registro Visual**: Anexação de fotos dos equipamentos diretamente às O.S para máxima transparência.

### Módulo de Vendas e Estoque
- **PDV Integrado**: Módulo de vendas com controle de estoque automatizado.
- **Integração de Peças**: Baixa automática de componentes utilizados nas ordens de serviço.
- **Comprovantes Flexíveis**: Emissão de recibos de venda em PDF (A4) ou formato para impressoras térmicas.

### Gestão Financeira e Dashboards
- **Controle de Fluxo**: Gestão detalhada de entradas e saídas.
- **Gráficos Analíticos**: Dashboards intuitivos que mostram lucratividade, desempenho da equipe e status das ordens.

### Agenda e Kanban
- **Visualização de Prazos**: Agenda mensal e semanal para controle de datas de fechamento.
- **Cards de Tarefas**: Sistema interativo para organizar tarefas diárias do laboratório.

---

## Diferenciais Competitivos

| Recurso | Detalhes |
| :--- | :--- |
| **Integração WhatsApp** | Envio de orçamentos e status da O.S direto para o cliente. |
| **Impressão Térmica** | Suporte para impressoras não fiscais de 80mm (OS, Recibos e Vendas). |
| **PWA & Mobilidade** | Uso otimizado em Smartphones, Tablets e PCs via navegador. |
| **Segurança (LGPD)** | Criptografia de dados e conformidade com a LGPD. |

---

## Planos e Escalabilidade

O sistema foi modelado para suportar o modelo de negócio SaaS (Software as a Service) com multitenancy:

| Plano | Sub-usuários | Acessos Totais | Recomendação |
| :--- | :---: | :---: | :--- |
| **Básico** | 0 | 1 | Técnicos Independentes |
| **Essencial** | 1 | 2 | Microempresas |
| **Profissional** | 2 | 3 | Assistências em Crescimento |
| **Empresarial** | 3 | 4 | Médias Empresas |
| **Master** | 4 | 5 | Grandes Centros Técnicos |

*Todos os planos contam com recursos ilimitados (O.S., Clientes, Vendas) e acesso 24/7 via nuvem.*

---

## Arquitetura e Engenharia

O projeto segue o padrão **MVC (Model-View-Controller)** no backend, garantindo separação clara de responsabilidades:

- **Escalabilidade**: Preparado para deploy via containers Docker, facilitando a migração e o crescimento entre VPS.
- **Resiliência**: Pipeline de backup automatizado (JSON/ZIP) para recuperação rápida de dados por empresa.
- **Experiência do Usuário (UX)**: Design responsivo e PWA (Progressive Web App) para uso em bancada ou dispositivos móveis.

Para detalhes sobre a arquitetura, fluxos de dados e casos de uso, acesse os guias de [Arquitetura de Sistemas](ARCHITECTURE.md) e o [Mapa de Diagramas](docs/DIAGRAMS.md).

---

## Gestão de Equipe e Permissões (RBAC)

O sistema conta com um controle de acesso rigoroso por perfis, garantindo a integridade dos dados:

| Funcionalidade | Admin | Técnico | Financeiro | Atendente |
| :--- | :---: | :---: | :---: | :---: |
| Ordens de Serviço | Sim | Sim | - | Sim |
| Clientes | Sim | Sim | - | Sim |
| Estoque / Produtos | Sim | Sim | Sim | - |
| Financeiro | Sim | - | Sim | - |
| Backup / Relatórios | Sim | - | Sim | - |
| Gestão de Usuários | Sim | - | - | - |

---

## Autor

**Erasmo Cardoso**
Fundador na **Electrocode**


- [Site Oficial](https://www.electrocode.com.br/electrocodeos)
- [Acesso ao Sistema](https://www.electrocode.com.br/app/authentication/sign-in)
- [Teste por 7 Dias](https://www.electrocode.com.br/formulario/teste-gratis/)


---

## Licença e Propriedade

Este repositório de documentação é de propriedade da **Electrocode**. A utilização ou reprodução deste material sem autorização prévia é proibida.

---

Designed by **ElectroCode** | 2025  
Copyright © ElectroCode All Rights Reserved

