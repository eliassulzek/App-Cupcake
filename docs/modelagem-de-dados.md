# 💾 Modelagem de Dados - App Cupcakes

## 📋 Visão Geral

Este documento descreve a estrutura completa do banco de dados do sistema **App Cupcakes**, incluindo todas as tabelas, colunas, tipos de dados, constraints e relacionamentos.

---

## 🗄️ Diagrama Entidade-Relacionamento (Textual)

```
┌──────────────┐
│   CLIENTE    │
└──────┬───────┘
       │ 1
       │
       │ N
┌──────▼───────┐         ┌──────────────┐
│    PEDIDO    │────────▶│    CUPOM     │
└──────┬───────┘    N:1  └──────────────┘
       │ 1
       │
       ├──────────────┐
       │              │
       │ N            │ 1
┌──────▼───────┐ ┌───▼──────────┐
│ PEDIDO_ITEM  │ │  PAGAMENTO   │
└──────┬───────┘ └──────────────┘
       │ N
       │
       │ 1
┌──────▼───────┐
│   PRODUTO    │
└──────┬───────┘
       │ 1
       │
       │ N
┌──────▼───────┐
│  AVALIACAO   │────────▶ CLIENTE
└──────────────┘    N:1
```

---

## 📊 Tabelas do Sistema

### 1. Tabela: `cliente`

Armazena os dados dos usuários clientes do sistema.

| Coluna | Tipo | Tamanho | Constraints | Descrição |
|--------|------|---------|-------------|-----------|
| `id` | INTEGER | - | PRIMARY KEY, AUTO_INCREMENT | Identificador único do cliente |
| `nome` | VARCHAR | 100 | NOT NULL | Nome completo do cliente |
| `email` | VARCHAR | 100 | NOT NULL, UNIQUE | Email para login e contato |
| `senha` | VARCHAR | 255 | NOT NULL | Senha criptografada (hash) |
| `cpf` | VARCHAR | 14 | NOT NULL, UNIQUE | CPF do cliente (formato: 000.000.000-00) |
| `telefone` | VARCHAR | 20 | NOT NULL | Telefone de contato |
| `data_nascimento` | DATE | - | NULL | Data de nascimento do cliente |
| `cep` | VARCHAR | 10 | NOT NULL | CEP do endereço (formato: 00000-000) |
| `endereco` | VARCHAR | 200 | NOT NULL | Logradouro completo |
| `numero` | VARCHAR | 10 | NOT NULL | Número do endereço |
| `complemento` | VARCHAR | 100 | NULL | Complemento do endereço (apto, bloco, etc.) |
| `bairro` | VARCHAR | 100 | NOT NULL | Bairro do cliente |
| `cidade` | VARCHAR | 100 | NOT NULL | Cidade do cliente |
| `estado` | VARCHAR | 2 | NOT NULL | UF do estado (ex: SP, RJ, MG) |
| `data_cadastro` | TIMESTAMP | - | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Data e hora do cadastro |
| `ativo` | BOOLEAN | - | NOT NULL, DEFAULT TRUE | Indica se o cliente está ativo |

**Índices:**
- `idx_cliente_email` em `email` (para login rápido)
- `idx_cliente_cpf` em `cpf` (para validações)

**Relacionamentos:**
- `cliente` 1:N `pedido` (um cliente pode fazer vários pedidos)
- `cliente` 1:N `avaliacao` (um cliente pode fazer várias avaliações)

---

### 2. Tabela: `produto`

Catálogo de cupcakes disponíveis para venda.

| Coluna | Tipo | Tamanho | Constraints | Descrição |
|--------|------|---------|-------------|-----------|
| `id` | INTEGER | - | PRIMARY KEY, AUTO_INCREMENT | Identificador único do produto |
| `nome` | VARCHAR | 100 | NOT NULL | Nome do cupcake |
| `descricao` | TEXT | - | NOT NULL | Descrição detalhada do produto |
| `preco` | DECIMAL | 10,2 | NOT NULL, CHECK (preco > 0) | Preço unitário do produto |
| `categoria` | VARCHAR | 50 | NOT NULL | Categoria/Sabor (ex: Chocolate, Morango, Baunilha) |
| `imagem_url` | VARCHAR | 500 | NULL | URL da imagem do produto |
| `estoque` | INTEGER | - | NOT NULL, DEFAULT 0, CHECK (estoque >= 0) | Quantidade disponível em estoque |
| `estoque_minimo` | INTEGER | - | NOT NULL, DEFAULT 5 | Quantidade mínima para alerta |
| `ativo` | BOOLEAN | - | NOT NULL, DEFAULT TRUE | Indica se o produto está ativo no catálogo |
| `data_cadastro` | TIMESTAMP | - | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Data e hora do cadastro |
| `data_atualizacao` | TIMESTAMP | - | NULL, ON UPDATE CURRENT_TIMESTAMP | Data e hora da última atualização |

**Índices:**
- `idx_produto_categoria` em `categoria` (para filtros)
- `idx_produto_ativo` em `ativo` (para listar apenas ativos)
- `idx_produto_nome` em `nome` (para buscas)

**Relacionamentos:**
- `produto` 1:N `pedido_item` (um produto pode estar em vários itens de pedido)
- `produto` 1:N `avaliacao` (um produto pode ter várias avaliações)

---

### 3. Tabela: `pedido`

Registra os pedidos realizados pelos clientes.

| Coluna | Tipo | Tamanho | Constraints | Descrição |
|--------|------|---------|-------------|-----------|
| `id` | INTEGER | - | PRIMARY KEY, AUTO_INCREMENT | Identificador único do pedido |
| `cliente_id` | INTEGER | - | NOT NULL, FOREIGN KEY | Referência ao cliente que fez o pedido |
| `cupom_id` | INTEGER | - | NULL, FOREIGN KEY | Referência ao cupom utilizado (se houver) |
| `data_pedido` | TIMESTAMP | - | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Data e hora do pedido |
| `status` | VARCHAR | 20 | NOT NULL, DEFAULT 'Pendente' | Status atual (Pendente, Preparando, Em Entrega, Entregue, Cancelado) |
| `valor_subtotal` | DECIMAL | 10,2 | NOT NULL, CHECK (valor_subtotal >= 0) | Soma dos itens antes do desconto |
| `valor_desconto` | DECIMAL | 10,2 | NOT NULL, DEFAULT 0, CHECK (valor_desconto >= 0) | Valor do desconto aplicado |
| `valor_total` | DECIMAL | 10,2 | NOT NULL, CHECK (valor_total >= 0) | Valor final do pedido |
| `endereco_entrega` | TEXT | - | NOT NULL | Endereço completo de entrega |
| `observacoes` | TEXT | - | NULL | Observações adicionais do cliente |
| `data_atualizacao` | TIMESTAMP | - | NULL, ON UPDATE CURRENT_TIMESTAMP | Data da última atualização de status |

**Índices:**
- `idx_pedido_cliente` em `cliente_id` (para histórico do cliente)
- `idx_pedido_status` em `status` (para filtros administrativos)
- `idx_pedido_data` em `data_pedido` (para relatórios por período)

**Relacionamentos:**
- `pedido` N:1 `cliente` (cada pedido pertence a um cliente)
- `pedido` N:1 `cupom` (cada pedido pode ter um cupom)
- `pedido` 1:N `pedido_item` (um pedido tem vários itens)
- `pedido` 1:1 `pagamento` (um pedido tem um pagamento)

**Constraints de Validação:**
```sql
CHECK (status IN ('Aguardando Pagamento', 'Em Preparo', 'Em Rota', 'Entregue', 'Cancelado'))
CHECK (valor_total = valor_subtotal - valor_desconto)
```

---

### 4. Tabela: `pedido_item`

Itens individuais de cada pedido (produtos e quantidades).

| Coluna | Tipo | Tamanho | Constraints | Descrição |
|--------|------|---------|-------------|-----------|
| `id` | INTEGER | - | PRIMARY KEY, AUTO_INCREMENT | Identificador único do item |
| `pedido_id` | INTEGER | - | NOT NULL, FOREIGN KEY | Referência ao pedido |
| `produto_id` | INTEGER | - | NOT NULL, FOREIGN KEY | Referência ao produto |
| `quantidade` | INTEGER | - | NOT NULL, CHECK (quantidade > 0) | Quantidade comprada |
| `preco_unitario` | DECIMAL | 10,2 | NOT NULL, CHECK (preco_unitario > 0) | Preço do produto no momento da compra |
| `subtotal` | DECIMAL | 10,2 | NOT NULL, CHECK (subtotal > 0) | Total do item (quantidade × preço_unitario) |

**Índices:**
- `idx_pedido_item_pedido` em `pedido_id` (para listar itens do pedido)
- `idx_pedido_item_produto` em `produto_id` (para análise de vendas)

**Relacionamentos:**
- `pedido_item` N:1 `pedido` (cada item pertence a um pedido)
- `pedido_item` N:1 `produto` (cada item referencia um produto)

**Constraints de Validação:**
```sql
CHECK (subtotal = quantidade * preco_unitario)
UNIQUE (pedido_id, produto_id) -- Um produto não pode aparecer duplicado no mesmo pedido
```

---

### 5. Tabela: `pagamento`

Registra as informações de pagamento dos pedidos.

| Coluna | Tipo | Tamanho | Constraints | Descrição |
|--------|------|---------|-------------|-----------|
| `id` | INTEGER | - | PRIMARY KEY, AUTO_INCREMENT | Identificador único do pagamento |
| `pedido_id` | INTEGER | - | NOT NULL, UNIQUE, FOREIGN KEY | Referência ao pedido (relação 1:1) |
| `metodo_pagamento` | VARCHAR | 30 | NOT NULL | Método escolhido (Pix, Cartão de Crédito, Boleto) |
| `status_pagamento` | VARCHAR | 20 | NOT NULL, DEFAULT 'Pendente' | Status (Pendente, Aprovado, Recusado) |
| `valor` | DECIMAL | 10,2 | NOT NULL, CHECK (valor > 0) | Valor do pagamento |
| `data_pagamento` | TIMESTAMP | - | NULL | Data e hora da confirmação do pagamento |
| `codigo_transacao` | VARCHAR | 100 | NULL | Código/ID da transação (simulado) |
| `data_criacao` | TIMESTAMP | - | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Data de criação do registro |

**Índices:**
- `idx_pagamento_pedido` em `pedido_id` (para consulta rápida)
- `idx_pagamento_status` em `status_pagamento` (para filtros)

**Relacionamentos:**
- `pagamento` 1:1 `pedido` (cada pagamento está ligado a um pedido)

**Constraints de Validação:**
```sql
CHECK (metodo_pagamento IN ('Pix', 'Cartão de Crédito', 'Boleto'))
CHECK (status_pagamento IN ('Pendente', 'Aprovado', 'Recusado'))
```

---

### 6. Tabela: `avaliacao`

Avaliações e comentários dos clientes sobre os produtos.

| Coluna | Tipo | Tamanho | Constraints | Descrição |
|--------|------|---------|-------------|-----------|
| `id` | INTEGER | - | PRIMARY KEY, AUTO_INCREMENT | Identificador único da avaliação |
| `produto_id` | INTEGER | - | NOT NULL, FOREIGN KEY | Referência ao produto avaliado |
| `cliente_id` | INTEGER | - | NOT NULL, FOREIGN KEY | Referência ao cliente que avaliou |
| `nota` | INTEGER | - | NOT NULL, CHECK (nota BETWEEN 1 AND 5) | Nota de 1 a 5 estrelas |
| `comentario` | TEXT | - | NULL | Comentário opcional do cliente |
| `data_avaliacao` | TIMESTAMP | - | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Data e hora da avaliação |

**Índices:**
- `idx_avaliacao_produto` em `produto_id` (para listar avaliações de um produto)
- `idx_avaliacao_cliente` em `cliente_id` (para histórico do cliente)

**Relacionamentos:**
- `avaliacao` N:1 `produto` (cada avaliação é de um produto)
- `avaliacao` N:1 `cliente` (cada avaliação é feita por um cliente)

**Constraints de Validação:**
```sql
UNIQUE (produto_id, cliente_id) -- Um cliente só pode avaliar cada produto uma vez
```

---

### 7. Tabela: `cupom`

Cupons de desconto criados pelos administradores.

| Coluna | Tipo | Tamanho | Constraints | Descrição |
|--------|------|---------|-------------|-----------|
| `id` | INTEGER | - | PRIMARY KEY, AUTO_INCREMENT | Identificador único do cupom |
| `codigo` | VARCHAR | 20 | NOT NULL, UNIQUE | Código do cupom (ex: CUPOM10, PRIMEIRACOMPRA) |
| `descricao` | VARCHAR | 200 | NOT NULL | Descrição do cupom |
| `tipo_desconto` | VARCHAR | 15 | NOT NULL | Tipo (Percentual ou Valor Fixo) |
| `valor_desconto` | DECIMAL | 10,2 | NOT NULL, CHECK (valor_desconto > 0) | Valor do desconto (% ou R$) |
| `valor_minimo_pedido` | DECIMAL | 10,2 | NOT NULL, DEFAULT 0 | Valor mínimo do pedido para usar o cupom |
| `data_inicio` | DATE | - | NOT NULL | Data de início da validade |
| `data_fim` | DATE | - | NOT NULL | Data de fim da validade |
| `quantidade_total` | INTEGER | - | NOT NULL, DEFAULT 0 | Quantidade total de usos disponíveis (0 = ilimitado) |
| `quantidade_usada` | INTEGER | - | NOT NULL, DEFAULT 0 | Quantidade de vezes que foi usado |
| `ativo` | BOOLEAN | - | NOT NULL, DEFAULT TRUE | Indica se o cupom está ativo |
| `data_criacao` | TIMESTAMP | - | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Data de criação do cupom |

**Índices:**
- `idx_cupom_codigo` em `codigo` (para validação rápida)
- `idx_cupom_ativo` em `ativo` (para listar cupons ativos)
- `idx_cupom_validade` em `data_inicio, data_fim` (para verificar validade)

**Relacionamentos:**
- `cupom` 1:N `pedido` (um cupom pode ser usado em vários pedidos)

**Constraints de Validação:**
```sql
CHECK (tipo_desconto IN ('Percentual', 'Valor Fixo'))
CHECK (data_fim >= data_inicio)
CHECK (quantidade_usada <= quantidade_total OR quantidade_total = 0)
```

---

## 🔗 Relacionamentos Detalhados

### Cardinalidades

| Relação | Cardinalidade | Descrição |
|---------|---------------|-----------|
| `cliente` → `pedido` | 1:N | Um cliente pode fazer vários pedidos |
| `pedido` → `pedido_item` | 1:N | Um pedido contém vários itens |
| `produto` → `pedido_item` | 1:N | Um produto pode estar em vários itens de pedido |
| `pedido` → `pagamento` | 1:1 | Cada pedido tem exatamente um pagamento |
| `cupom` → `pedido` | 1:N | Um cupom pode ser usado em vários pedidos |
| `produto` → `avaliacao` | 1:N | Um produto pode ter várias avaliações |
| `cliente` → `avaliacao` | 1:N | Um cliente pode fazer várias avaliações |

### Chaves Estrangeiras (Foreign Keys)

```sql
-- Tabela: pedido
ALTER TABLE pedido 
  ADD CONSTRAINT fk_pedido_cliente 
  FOREIGN KEY (cliente_id) REFERENCES cliente(id) ON DELETE RESTRICT;

ALTER TABLE pedido 
  ADD CONSTRAINT fk_pedido_cupom 
  FOREIGN KEY (cupom_id) REFERENCES cupom(id) ON DELETE SET NULL;

-- Tabela: pedido_item
ALTER TABLE pedido_item 
  ADD CONSTRAINT fk_pedido_item_pedido 
  FOREIGN KEY (pedido_id) REFERENCES pedido(id) ON DELETE CASCADE;

ALTER TABLE pedido_item 
  ADD CONSTRAINT fk_pedido_item_produto 
  FOREIGN KEY (produto_id) REFERENCES produto(id) ON DELETE RESTRICT;

-- Tabela: pagamento
ALTER TABLE pagamento 
  ADD CONSTRAINT fk_pagamento_pedido 
  FOREIGN KEY (pedido_id) REFERENCES pedido(id) ON DELETE CASCADE;

-- Tabela: avaliacao
ALTER TABLE avaliacao 
  ADD CONSTRAINT fk_avaliacao_produto 
  FOREIGN KEY (produto_id) REFERENCES produto(id) ON DELETE CASCADE;

ALTER TABLE avaliacao 
  ADD CONSTRAINT fk_avaliacao_cliente 
  FOREIGN KEY (cliente_id) REFERENCES cliente(id) ON DELETE CASCADE;
```

### Políticas de Exclusão

- **RESTRICT**: Impede a exclusão se houver registros relacionados
  - Usado em: `cliente`, `produto` (em pedidos/avaliações)
  
- **CASCADE**: Exclui automaticamente os registros relacionados
  - Usado em: `pedido` → `pedido_item`, `pedido` → `pagamento`
  
- **SET NULL**: Define como NULL se o registro pai for excluído
  - Usado em: `pedido` → `cupom`

---

## 📈 Estimativas de Volume de Dados

| Tabela | Crescimento | Estimativa (1 ano) |
|--------|-------------|-------------------|
| `cliente` | Moderado | 1.000 - 5.000 registros |
| `produto` | Baixo | 50 - 200 registros |
| `pedido` | Alto | 5.000 - 50.000 registros |
| `pedido_item` | Muito Alto | 15.000 - 150.000 registros |
| `pagamento` | Alto | 5.000 - 50.000 registros |
| `avaliacao` | Moderado | 2.000 - 20.000 registros |
| `cupom` | Baixo | 20 - 100 registros |

---

## 🔍 Queries Importantes

### 1. Listar Produtos Disponíveis no Catálogo

```sql
SELECT * FROM produto 
WHERE ativo = TRUE AND estoque > 0 
ORDER BY nome;
```

### 2. Histórico de Pedidos de um Cliente

```sql
SELECT p.*, pa.status_pagamento 
FROM pedido p
INNER JOIN pagamento pa ON p.id = pa.pedido_id
WHERE p.cliente_id = ? 
ORDER BY p.data_pedido DESC;
```

### 3. Itens de um Pedido Específico

```sql
SELECT pi.*, pr.nome, pr.imagem_url 
FROM pedido_item pi
INNER JOIN produto pr ON pi.produto_id = pr.id
WHERE pi.pedido_id = ?;
```

### 4. Produtos com Estoque Baixo

```sql
SELECT * FROM produto 
WHERE ativo = TRUE AND estoque <= estoque_minimo
ORDER BY estoque ASC;
```

### 5. Validar Cupom

```sql
SELECT * FROM cupom 
WHERE codigo = ? 
  AND ativo = TRUE 
  AND CURRENT_DATE BETWEEN data_inicio AND data_fim
  AND (quantidade_total = 0 OR quantidade_usada < quantidade_total);
```

### 6. Média de Avaliações de um Produto

```sql
SELECT AVG(nota) as media_nota, COUNT(*) as total_avaliacoes 
FROM avaliacao 
WHERE produto_id = ?;
```

### 7. Relatório de Vendas por Período

```sql
SELECT 
  DATE(p.data_pedido) as data,
  COUNT(p.id) as total_pedidos,
  SUM(p.valor_total) as total_vendas
FROM pedido p
WHERE p.data_pedido BETWEEN ? AND ?
  AND p.status != 'Cancelado'
GROUP BY DATE(p.data_pedido)
ORDER BY data DESC;
```

### 8. Produtos Mais Vendidos

```sql
SELECT 
  pr.id, pr.nome, pr.imagem_url,
  SUM(pi.quantidade) as total_vendido
FROM pedido_item pi
INNER JOIN produto pr ON pi.produto_id = pr.id
INNER JOIN pedido p ON pi.pedido_id = p.id
WHERE p.status != 'Cancelado'
GROUP BY pr.id
ORDER BY total_vendido DESC
LIMIT 10;
```

---

## 🛡️ Segurança e Integridade

### Validações Implementadas

1. **Integridade Referencial**: Todas as chaves estrangeiras garantem consistência
2. **Constraints de Domínio**: Verificações de valores válidos (ex: status, notas)
3. **Checks de Valores**: Garantia de valores positivos para preços e quantidades
4. **Unicidade**: Emails, e códigos de cupom únicos

### Triggers Recomendados (Base44)

1. **Atualizar Estoque**: Reduzir estoque automaticamente ao criar pedido
2. **Calcular Subtotal**: Calcular automaticamente o subtotal de pedido_item
3. **Atualizar Contador de Cupons**: Incrementar quantidade_usada ao usar cupom
4. **Validar Estoque**: Impedir pedido se estoque insuficiente

---

## 📊 Normalização

O banco de dados está na **3ª Forma Normal (3FN)**:

✅ **1FN**: Todos os atributos são atômicos  
✅ **2FN**: Não há dependências parciais  
✅ **3FN**: Não há dependências transitivas  

**Benefícios:**
- Minimização de redundância
- Facilidade de manutenção
- Integridade dos dados
- Performance otimizada para consultas

---

## 🎯 Conclusão

Esta modelagem de dados foi projetada para:

- **Suportar todas as funcionalidades** do App Cupcakes
- **Garantir integridade** e consistência dos dados
- **Facilitar consultas** e relatórios
- **Permitir escalabilidade** conforme crescimento do negócio
- **Manter performance** mesmo com grande volume de dados

A estrutura é robusta, normalizada e preparada para um sistema de e-commerce profissional.

---

**Modelagem de Dados - App Cupcakes**  
*Última atualização: Dezembro 2025*
