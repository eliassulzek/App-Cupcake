# 🏗️ Arquitetura do Sistema - App Cupcakes

## 📋 Visão Geral

O **App Cupcakes** foi desenvolvido utilizando a arquitetura **serverless** e **no-code** da plataforma **Base44**, com foco em escalabilidade, segurança e manutenibilidade dentro do que a plataforma oferece.

> **Nota:** este documento descreve o sistema do ponto de vista do projeto. Detalhes internos da plataforma (infraestrutura, segurança, backup, disponibilidade) são gerenciados pela Base44 e **não foram auditados** neste projeto. Para informações oficiais, consulte a documentação da Base44.

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
│  • Aplicação web responsiva                                      │
│  • Gerado pela plataforma (no-code)                              │
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
│  • Backup gerenciado                                             │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🌐 Camada de Apresentação (Frontend)

### Tecnologias Base44

- **Framework**: interface gerada pela plataforma Base44
- **Responsividade**: design adaptável (Desktop, Tablet, Mobile)
- **Implementação**: gerenciada pela plataforma, sem código manual

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
  - Escolha de método de pagamento (simulado)
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
  - Exportação de dados (CSV e JSON)

---

## ⚙️ Camada de Lógica (Backend)

### Arquitetura Serverless Base44

O backend é gerenciado pela plataforma Base44, em modelo **serverless**:

- **Funções sob demanda**: não há servidores próprios para administrar
- **Escalabilidade**: gerenciada pela plataforma
- **Sem configuração de infraestrutura**: o desenvolvimento foca nas regras de negócio

### API REST

A plataforma disponibiliza operações RESTful para cada entidade. O quadro abaixo é uma **representação conceitual** das operações do sistema. Os nomes e rotas reais são gerenciados pela Base44:

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
   Gera registro de pagamento (simulado)
        ↓
   Retorna confirmação ao cliente
   ```

4. **Controle de Status**
   - Pedidos: Aguardando Pagamento → Em Preparo → Em Rota → Entregue → Cancelado
   - Pagamentos: Pendente → Aprovado → Recusado
   - Produtos: Ativo → Inativo

---

## 💾 Camada de Dados

### Banco de Dados Relacional (PostgreSQL)

- **Tipo**: PostgreSQL gerenciado pela Base44
- **Localização**: cloud (infraestrutura da Base44)
- **Backup e replicação**: responsabilidade da plataforma, sem configuração própria neste projeto

### Estrutura de Tabelas

#### Principais Entidades

| Tabela | Descrição | Volume estimado (hipotético) |
|--------|-----------|------------------------------|
| `cliente` | Dados dos usuários clientes | Milhares |
| `produto` | Catálogo de cupcakes | Dezenas |
| `pedido` | Pedidos realizados | Milhares |
| `pedido_item` | Itens de cada pedido | Dezenas de milhares |
| `pagamento` | Registros de pagamento (simulado) | Milhares |
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

O sistema usa a autenticação integrada da Base44:

- **Registro de Usuários**
  - Criação de conta com verificação por e-mail (código de autenticação)
  - Validação de e-mail único

- **Login/Logout**
  - Autenticação por credenciais
  - Controle de sessão gerenciado pela plataforma

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

Os mecanismos de segurança da camada de autenticação e da infraestrutura (armazenamento de senhas, sessões, HTTPS, proteção contra ataques comuns) são fornecidos pela plataforma e **não foram auditados** neste projeto.

No escopo do projeto foram aplicados:

1. **Validações de entrada** configuradas nos formulários e nas regras de negócio
2. **Proteção de rotas administrativas** por role (Cliente/Administrador)
3. **Pagamento simulado**: nenhum dado de cartão ou financeiro real é processado

---

## 🚀 Deploy e Hospedagem

### Infraestrutura Base44

- **Hospedagem**: cloud gerenciada pela Base44
- **Domínio**: subdomínio da Base44 (`*.base44.app`)
- **Protocolo**: HTTPS

### Processo de Deploy

```
Desenvolvimento Visual na Base44
        ↓
Teste em Ambiente de Preview
        ↓
Publicação pela plataforma
        ↓
Sistema Disponível Online
```

### Monitoramento

Logs e métricas estão disponíveis conforme o painel da plataforma. Não foi configurado monitoramento próprio.

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
9. Escolhe método de pagamento (simulado)
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
2. Visualiza novos pedidos (status: Aguardando Pagamento)
3. Revisa detalhes do pedido
4. Atualiza status para "Em Preparo"
5. Prepara o pedido
6. Atualiza status para "Em Rota"
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

- **Autenticação**: sistema nativo
- **Upload de Arquivos**: armazenamento da Base44
- **E-mails**: verificação de conta pela plataforma

### Externas (não implementadas)

- **Gateway de Pagamento**: pagamento simulado no sistema atual
  - Poderia ser integrado a Stripe, PagSeguro, Mercado Pago
- **Sistema de Entregas**: não implementado
  - Possível integração com serviços de entrega
- **Análise**: não implementado
  - Possível integração com Google Analytics

---

## 📈 Escalabilidade

Em um modelo serverless gerenciado, a escalabilidade e a disponibilidade dependem da plataforma e do plano contratado. Este projeto **não realizou testes de carga**, e portanto não há medições de capacidade.

---

## 🛠️ Dependências e Tecnologias

### Stack Tecnológico

| Camada | Tecnologia | Detalhes |
|--------|-----------|----------|
| **Frontend** | Interface gerada pela Base44 | No-code |
| **Backend** | Base44 Serverless | Gerenciado |
| **Banco de Dados** | PostgreSQL | Gerenciado |
| **Autenticação** | Base44 Auth | Integrada |
| **Hospedagem** | Base44 Cloud | Gerenciada |
| **Protocolo** | HTTPS | - |

### Dependências Externas

- **Nenhuma**: sistema contido na Base44
- **Imagens**: armazenadas na infraestrutura da Base44

---

## 📝 Considerações Técnicas

### Vantagens da Arquitetura Escolhida

✅ **Desenvolvimento Rápido**: prototipagem e implementação ágil  
✅ **Manutenção Simplificada**: infraestrutura gerenciada  
✅ **Foco no negócio**: tempo dedicado a requisitos, dados e testes  

### Limitações

⚠️ **Customização**: limitada às capacidades da Base44  
⚠️ **Vendor Lock-in**: dependência da plataforma  
⚠️ **Portabilidade**: código não exportável  
⚠️ **Integrações**: dependentes do suporte da Base44  
⚠️ **Pagamento e entrega**: apenas simulados/não implementados  

---

## 🎯 Conclusão

A arquitetura do **App Cupcakes** foi pensada para ser:

- **Simples**: fácil de entender e manter
- **Documentada**: com modelo de dados, fluxos e testes descritos
- **Adequada ao contexto acadêmico**: foco em análise de requisitos e modelagem

A escolha da plataforma Base44 permitiu concentrar o esforço nas funcionalidades de negócio, sem a complexidade de gerenciar infraestrutura.

---

**Documentação Técnica - App Cupcakes**  
*Última atualização: Novembro 2026*
