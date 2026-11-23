# 💾 Modelagem de Dados - App Cupcakes

## 📋 Visão Geral

Este documento descreve as **entidades reais** do App Cupcakes na Base44, conforme os esquemas do app publicado. A Base44 gerencia o banco internamente: cada entidade tem os campos abaixo, mais os campos automáticos `id`, `created_date`, `updated_date` e `created_by`.

O modelo é **simples e desnormalizado**: não existe entidade de cliente nem de item de pedido. Os clientes são os usuários da plataforma (`User`) e os itens ficam dentro do próprio pedido.

---

## 🗄️ Entidades e Relacionamentos

```
User (telefone, endereço...)
   │  identificado pelo e-mail
   ▼
Pedido ───────────────► Pagamento   (Pagamento.pedido_id → Pedido.id)
  │  itens[] embutidos
  │  cupom_usado (código) ──► Cupom (consulta pelo código)
  ▼
Produto ◄──────────── Avaliacao     (Avaliacao.produto_id → Produto.id)
```

Os vínculos são feitos por **id ou e-mail guardado como texto**, sem chave estrangeira nem integridade referencial no banco.

---

## 📊 Entidades

### 1. `Produto`

| Campo | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `nome` | texto | ✅ | Nome do cupcake |
| `descricao` | texto | | Descrição detalhada |
| `sabor` | enum | ✅ | Chocolate, Baunilha, Red Velvet, Morango, Oreo, Limão |
| `preco` | número | ✅ | Preço unitário |
| `estoque` | inteiro | ✅ | Quantidade em estoque |
| `imagem_url` | texto | | URL da imagem |
| `ativo` | booleano | | Padrão: verdadeiro |

### 2. `Pedido`

| Campo | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `cliente_email` | texto | ✅ | E-mail do cliente (vínculo com o usuário) |
| `cliente_nome` | texto | | Nome do cliente |
| `telefone` | texto | | Telefone informado no checkout |
| `endereco_entrega` | texto | | Endereço de entrega em um único campo |
| `itens` | lista | ✅ | Itens embutidos: `produto_id`, `produto_nome`, `quantidade`, `preco_unit` |
| `subtotal` | número | | Soma dos itens antes do desconto |
| `desconto` | número | | Padrão: 0 |
| `cupom_usado` | texto | | Código do cupom aplicado |
| `total` | número | ✅ | Valor final |
| `status` | enum | ✅ | AGUARDANDO_PAGAMENTO (padrão), EM_PREPARO, EM_ROTA, ENTREGUE, CANCELADO |
| `historico_status` | lista | | Cada mudança de status: `status`, `data`, `observacao` |

O `historico_status` é gravado pelo app (ex.: "Pedido criado" e "Pagamento confirmado").

### 3. `Pagamento`

| Campo | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `pedido_id` | texto | ✅ | Id do pedido |
| `metodo` | enum | ✅ | PIX, CARTAO_CREDITO, CARTAO_DEBITO, BOLETO |
| `status` | enum | | PENDENTE (padrão), APROVADO, RECUSADO |
| `transacao_id` | texto | | Código da transação (gerado pelo app, simulado) |
| `valor` | número | ✅ | Valor do pagamento |

### 4. `Avaliacao`

| Campo | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `cliente_email` | texto | ✅ | E-mail do cliente |
| `cliente_nome` | texto | | Nome exibido |
| `produto_id` | texto | ✅ | Id do produto avaliado |
| `pedido_id` | texto | | Id do pedido relacionado (opcional) |
| `nota` | inteiro | ✅ | De 1 a 5 |
| `comentario` | texto | | Comentário |

### 5. `Cupom`

| Campo | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `codigo` | texto | ✅ | Código do cupom |
| `tipo` | enum | ✅ | PERCENTUAL ou VALOR_FIXO |
| `valor` | número | ✅ | Desconto (% ou R$) |
| `validade` | data | ✅ | Data de validade (única) |
| `ativo` | booleano | | Padrão: verdadeiro |
| `uso_maximo` | inteiro | | Limite de usos |
| `uso_atual` | inteiro | | Padrão: 0 |

### 6. `User` (usuário da plataforma)

Além dos campos nativos (nome, e-mail, perfil/role), o app adiciona:

| Campo | Tipo | Descrição |
|---|---|---|
| `telefone` | texto | Telefone |
| `endereco` | texto | Endereço completo |
| `cidade` | texto | Cidade |
| `estado` | texto | Estado |
| `cep` | texto | CEP |

---

## 🔄 Fluxo dos Dados na Compra

1. O checkout cria o **Pedido** com status `AGUARDANDO_PAGAMENTO` e a observação "Pedido criado"
2. O pagamento simulado cria o **Pagamento** (ex.: PIX, `APROVADO`, com `transacao_id` gerado)
3. O pedido passa para `EM_PREPARO`, com a observação "Pagamento confirmado" no histórico
4. Se houver cupom, o pedido guarda `cupom_usado` e o `desconto`
5. O administrador avança o status: `EM_ROTA` e depois `ENTREGUE` (ou `CANCELADO`)

---

## ⚖️ Limitações do Modelo

- **Sem integridade referencial**: os vínculos são texto (id ou e-mail)
- **Itens dentro do pedido**: facilita a leitura, mas dificulta consultas como "quantos de um produto foram vendidos" sem processar todos os pedidos
- **Desnormalização**: nome do cliente, nome do produto e preço ficam copiados no pedido (mantém o histórico, mas duplica dados)
- **Sem restrição de unicidade** no código do cupom nem de uma avaliação por cliente/produto no nível do banco
- **Sem acesso SQL**: consultas são feitas pelas ferramentas da plataforma

---

## 🎯 Melhorias Futuras

- Separar `ItemPedido` em entidade própria para facilitar relatórios
- Entidade de endereços (vários por cliente)
- Banco relacional com chaves estrangeiras e constraints, caso o sistema seja reconstruído com código próprio

---

**Documentação de Modelagem de Dados - App Cupcakes**  
*Última atualização: Novembro 2026*
