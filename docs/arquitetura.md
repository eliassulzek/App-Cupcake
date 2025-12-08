# 🏗️ Arquitetura do Sistema - App Cupcakes

## 📋 Visão Geral

O **App Cupcakes** foi desenvolvido utilizando a arquitetura **serverless** e **no-code** da plataforma **Base44**, seguindo princípios modernos de desenvolvimento cloud-native com foco em escalabilidade, segurança e manutenibilidade.

---

## 🎯 Arquitetura de Alto Nível

```
┌─────────────────────────────────────────────────────────────────┐
│                         USUÁRIOS                                 │
│                    (Cliente / Admin)                             │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                      FRONTEND (Base44)                           │
│  • Interface Responsiva                                          │
│  • Single Page Application (SPA)                                 │
│  • React/Vue (gerado automaticamente)                            │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                    CAMADA DE AUTENTICAÇÃO                        │
│  • Login/Logout                                                  │
│  • Controle de Sessão                                            │
│  • Gestão de Permissões (Cliente/Admin)                          │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                   API REST (Backend Serverless)                  │
│  • Endpoints Automáticos                                         │
│  • Lógica de Negócios Visual                                     │
│  • Validações e Regras                                           │
│  • Processamento de Pedidos                                      │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│               BANCO DE DADOS (PostgreSQL)                        │
│  • Tabelas Relacionais                                           │
│  • Constraints e Índices                                         │
│  • Backup Automático                                             │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🌐 Camada de Apresentação (Frontend)

### Tecnologias Base44

- **Framework**: Interface gerada automaticamente pela Base44
- **Paradigma**: Single Page Application (SPA)
- **Responsividade**: Design adaptável automático (Desktop, Tablet, Mobile)
- **Estado**: Gerenciamento de estado nativo da plataforma

### Componentes Principais

#### 1. Área do Cliente

- **Catálogo de Produtos**
  - Grid responsivo de cupcakes
  - Cards com imagem, nome, preço e descrição
  - Sistema de paginação

- **Barra de Busca e Filtros**
  - Busca textual por nome/descrição
  - Filtros por categoria (sabores)
  - Filtros por faixa de preço
  - Ordenação (menor/maior preço, nome)

- **Carrinho de Compras**
  - Visualização de itens adicionados
  - Ajuste de quantidades (+/-)
  - Remoção de itens
  - Cálculo automático de subtotal e total

- **Checkout**
  - Formulário de dados pessoais
  - Seleção de endereço de entrega
  - Escolha de método de pagamento
  - Aplicação de cupom de desconto
  - Resumo do pedido

- **Histórico e Rastreamento**
  - Lista de pedidos anteriores
  - Status visual do pedido (progress bar)
  - Detalhes de cada pedido

- **Perfil do Usuário**
  - Edição de dados cadastrais
  - Gerenciamento de endereços
  - Alteração de senha

#### 2. Área Administrativa

- **Dashboard**
  - Cards com métricas principais
  - Gráficos de vendas
  - Tabela de últimos pedidos
  - Alertas de estoque baixo

- **Gestão de Produtos**
  - Listagem completa com busca
  - Formulários de cadastro/edição
  - Upload de imagens
  - Status ativo/inativo

- **Gerenciamento de Pedidos**
  - Filtros por status e data
  - Atualização de status
  - Visualização detalhada

- **Sistema de Cupons**
  - Criação de cupons de desconto
  - Definição de validade
  - Tipos: percentual ou valor fixo

- **Relatórios**
  - Vendas por período
  - Produtos mais vendidos
  - Exportação de dados

---

## ⚙️ Camada de Lógica (Backend)

### Arquitetura Serverless Base44

O backend é completamente gerenciado pela plataforma Base44, seguindo uma arquitetura **serverless**:

- **Funções sob Demanda**: Não há servidores fixos rodando
- **Escalabilidade Automática**: Recursos alocados conforme necessidade
- **Alta Disponibilidade**: Infraestrutura distribuída
- **Custo Otimizado**: Pagamento apenas pelo uso real

### API REST Gerada Automaticamente

A Base44 gera automaticamente endpoints RESTful para cada entidade:

```
/api/produtos
  ├─ GET     /          # Listar produtos (com paginação e filtros)
  ├─ GET     /{id}      # Obter produto específico
  ├─ POST    /          # Criar novo produto
  ├─ PUT     /{id}      # Atualizar produto
  └─ DELETE  /{id}      # Excluir produto

/api/pedidos
  ├─ GET     /          # Listar pedidos
  ├─ GET     /{id}      # Obter pedido específico
  ├─ POST    /          # Criar novo pedido
  └─ PUT     /{id}      # Atualizar pedido (status)

/api/clientes
  ├─ GET     /{id}      # Obter perfil do cliente
  └─ PUT     /{id}      # Atualizar perfil

/api/avaliacoes
  ├─ GET     /          # Listar avaliações
  └─ POST    /          # Criar avaliação

/api/cupons
  ├─ GET     /          # Listar cupons
  ├─ POST    /          # Criar cupom
  └─ GET     /validar   # Validar cupom
```

### Lógica de Negócios

Implementada visualmente na Base44:

1. **Validações de Entrada**
   - Campos obrigatórios
   - Formatos de dados (email, telefone, CPF)
   - Valores mínimos/máximos

2. **Regras de Negócio**
   - Verificação de estoque antes de adicionar ao carrinho
   - Cálculo de desconto de cupons
   - Atualização de estoque após pedido
   - Validação de pedido mínimo

3. **Processamento de Pedidos**
   ```
   Cliente finaliza compra
        ↓
   Valida estoque disponível
        ↓
   Aplica cupom (se houver)
        ↓
   Cria registro do pedido
        ↓
   Cria itens do pedido
        ↓
   Atualiza estoque dos produtos
        ↓
   Gera registro de pagamento
        ↓
   Retorna confirmação ao cliente
   ```

4. **Controle de Status**
   - Pedidos: Pendente → Preparando → Em Entrega → Entregue → Cancelado
   - Pagamentos: Pendente → Aprovado → Recusado
   - Produtos: Ativo → Inativo

---

## 💾 Camada de Dados

### Banco de Dados Relacional (PostgreSQL)

- **Tipo**: PostgreSQL gerenciado pela Base44
- **Localização**: Cloud (infraestrutura Base44)
- **Backup**: Automático e periódico
- **Replicação**: Gerenciada pela plataforma

### Estrutura de Tabelas

#### Principais Entidades

| Tabela | Descrição | Registros Esperados |
|--------|-----------|---------------------|
| `cliente` | Dados dos usuários clientes | Milhares |
| `produto` | Catálogo de cupcakes | Dezenas |
| `pedido` | Pedidos realizados | Milhares |
| `pedido_item` | Itens de cada pedido | Dezenas de milhares |
| `pagamento` | Registros de pagamento | Milhares |
| `avaliacao` | Avaliações dos clientes | Milhares |
| `cupom` | Cupons de desconto | Centenas |

> Para detalhes completos do modelo de dados, consulte: [modelagem-de-dados.md](./modelagem-de-dados.md)

### Relacionamentos Principais

```
cliente (1) ──────── (N) pedido
                            │
                            │ (1)
                            │
                            ├─────── (N) pedido_item
                            │               │
                            │               │ (N)
                            │               │
                            │               └─────── (1) produto
                            │
                            ├─────── (1) pagamento
                            │
                            └─────── (1) cupom (opcional)

produto (1) ──────── (N) avaliacao ──────── (1) cliente
```

---

## 🔐 Camada de Autenticação e Segurança

### Sistema de Autenticação

A Base44 fornece sistema de autenticação integrado:

- **Registro de Usuários**
  - Criação de conta com email/senha
  - Validação de email único
  - Criptografia automática de senhas

- **Login/Logout**
  - Autenticação por credenciais
  - Geração de token de sessão
  - Expiração automática de sessão

- **Controle de Acesso (RBAC)**
  - **Role: Cliente**
    - Acesso apenas à área pública
    - Visualização de produtos
    - Gestão do próprio perfil
    - Criação e visualização dos próprios pedidos
  
  - **Role: Administrador**
    - Acesso total ao painel admin
    - CRUD completo de produtos
    - Visualização de todos os pedidos
    - Gestão de cupons
    - Acesso a relatórios

### Segurança

1. **Proteção de Dados**
   - Senhas criptografadas (hash)
   - Comunicação HTTPS obrigatória
   - Tokens de sessão seguros

2. **Validações Backend**
   - Todas as entradas são validadas no servidor
   - Proteção contra SQL Injection (ORM da Base44)
   - Sanitização de dados

3. **Proteção de Rotas**
   - Rotas administrativas protegidas por role
   - Verificação de token em cada requisição
   - Logout automático em caso de token inválido

---

## 🚀 Deploy e Hospedagem

### Infraestrutura Base44

- **Hospedagem**: Cloud gerenciada pela Base44
- **CDN**: Distribuição de conteúdo estático
- **SSL/TLS**: Certificado automático (HTTPS)
- **Domínio**: Subdomínio Base44 ou domínio customizado

### Processo de Deploy

```
Desenvolvimento Visual na Base44
        ↓
Teste em Ambiente de Preview
        ↓
Publicação com Um Clique
        ↓
Deploy Automático para Produção
        ↓
Sistema Disponível Online
```

### Monitoramento

- **Logs de Aplicação**: Registrados pela Base44
- **Uptime**: Monitorado pela plataforma
- **Métricas**: Disponíveis no painel Base44

---

## 📊 Fluxos Principais do Sistema

### 1. Fluxo de Compra (Cliente)

```
1. Cliente acessa o catálogo
2. Navega pelos produtos / Usa busca e filtros
3. Adiciona produtos ao carrinho
4. Ajusta quantidades se necessário
5. Vai para o checkout
6. Preenche/confirma dados pessoais
7. Seleciona endereço de entrega
8. Aplica cupom de desconto (opcional)
9. Escolhe método de pagamento
10. Finaliza pedido
11. Sistema cria pedido no banco
12. Atualiza estoque dos produtos
13. Gera confirmação
14. Cliente recebe número do pedido
15. Cliente acompanha status
```

### 2. Fluxo de Gestão de Pedidos (Admin)

```
1. Admin acessa painel administrativo
2. Visualiza novos pedidos (status: Pendente)
3. Revisa detalhes do pedido
4. Atualiza status para "Preparando"
5. Prepara o pedido
6. Atualiza status para "Em Entrega"
7. Após entrega, atualiza para "Entregue"
8. Sistema registra histórico de mudanças
```

### 3. Fluxo de Cadastro de Produto (Admin)

```
1. Admin acessa gestão de produtos
2. Clica em "Novo Produto"
3. Preenche formulário:
   - Nome do cupcake
   - Descrição
   - Preço
   - Categoria/Sabor
   - Quantidade em estoque
   - Upload de imagem
4. Salva produto
5. Sistema valida dados
6. Produto criado e disponível no catálogo
```

---

## 🔄 Integrações

### Internas (Base44)

- **Autenticação**: Sistema nativo
- **Upload de Arquivos**: Armazenamento Base44
- **Emails**: Sistema de notificações (se habilitado)

### Externas (Potenciais)

- **Gateway de Pagamento**: Simulado no sistema atual
  - Pode ser integrado com Stripe, PagSeguro, MercadoPago
- **Sistema de Entregas**: Não implementado
  - Possível integração com Correios, Loggi, etc.
- **Análise**: Não implementado
  - Possível integração com Google Analytics

---

## 📈 Escalabilidade

### Vantagens da Arquitetura Serverless

1. **Escalabilidade Horizontal Automática**
   - Base44 aumenta recursos conforme demanda
   - Sem limite rígido de usuários simultâneos

2. **Performance**
   - CDN para assets estáticos
   - Cache automático de queries comuns
   - Otimização de banco de dados

3. **Disponibilidade**
   - Múltiplas zonas de disponibilidade
   - Redundância automática
   - SLA garantido pela Base44

---

## 🛠️ Dependências e Tecnologias

### Stack Tecnológico

| Camada | Tecnologia | Versão/Detalhes |
|--------|-----------|-----------------|
| **Frontend** | Base44 Framework | Última versão |
| **Backend** | Base44 Serverless | Cloud-native |
| **Banco de Dados** | PostgreSQL | Gerenciado |
| **Autenticação** | Base44 Auth | Integrado |
| **Hospedagem** | Base44 Cloud | Global |
| **Protocolo** | HTTPS | TLS 1.3 |

### Dependências Externas

- **Nenhuma**: Sistema 100% contido na Base44
- **Imagens**: Armazenadas na infraestrutura Base44
- **Assets**: Servidos via CDN Base44

---

## 📝 Considerações Técnicas

### Vantagens da Arquitetura Escolhida

✅ **Desenvolvimento Rápido**: Prototipagem e implementação ágil  
✅ **Manutenção Simplificada**: Infraestrutura gerenciada  
✅ **Custo Previsível**: Modelo de precificação transparente  
✅ **Segurança**: Práticas de segurança embutidas  
✅ **Atualizações Automáticas**: Plataforma sempre atualizada  

### Limitações

⚠️ **Customização**: Limitada às capacidades da Base44  
⚠️ **Vendor Lock-in**: Dependência da plataforma  
⚠️ **Portabilidade**: Código não exportável  
⚠️ **Integrações**: Dependente do suporte da Base44  

---

## 🎯 Conclusão

A arquitetura do **App Cupcakes** foi desenhada para ser:

- **Simples**: Fácil de entender e manter
- **Robusta**: Confiável e escalável
- **Moderna**: Utilizando tecnologias cloud-native
- **Segura**: Com proteções em todas as camadas
- **Eficiente**: Otimizada para performance

A escolha da plataforma Base44 permitiu focar nas funcionalidades de negócio, entregando um produto completo e profissional sem a complexidade de gerenciar infraestrutura.

---

**Documentação Técnica - App Cupcakes**  
*Última atualização: Dezembro 2025*
