# ✨ Funcionalidades do Sistema - App Cupcakes

## 📋 Visão Geral

Este documento descreve **o que o App Cupcakes faz na versão publicada**, desenvolvido na plataforma no-code Base44. O texto foi conferido navegando no próprio app.

> O pagamento é **simulado** (nenhuma cobrança real) e não há integração com serviços de entrega, e-mail ou notificações. Itens que o app **não possui** estão listados na seção [Fora do Escopo](#-fora-do-escopo-não-implementado).

Estrutura do app: **Área do Cliente** (Home, Produto, Carrinho, Checkout, Meus Pedidos, Perfil) e **Painel Administrativo** (Dashboard, Produtos, Pedidos, Cupons, Relatórios).

---

## 👥 ÁREA DO CLIENTE

### 1. 🏠 Página Inicial / Catálogo

- Cabeçalho com logo, ícone do carrinho (com contador de itens) e menu do usuário
- Banner com campo de busca e botão de filtros
- **Sugestão do Dia**: destaque de um produto, com botão "Experimentar Hoje". O produto sugerido muda entre os acessos
- Seção "Nossos Cupcakes" com contador de produtos e grid de cards
- Cada card mostra: imagem, etiqueta do sabor, nome, descrição, preço e botão "Adicionar". Quando há avaliações, mostra a nota média e a quantidade
- Rodapé com links rápidos (Produtos, Meus Pedidos, Minha Conta) e contato

### 2. 🔍 Busca e Filtros

- **Busca**: campo "Buscar cupcakes..." na página inicial
- **Painel de filtros** (botão ao lado da busca), com:
  - **Sabor**: Todos, Chocolate, Baunilha, Red Velvet, Morango, Oreo, Limão
  - **Faixa de Preço**: controle deslizante (R$ 0 a R$ 50)
  - **Limpar Filtros**

### 3. 🧁 Detalhe do Produto

- Imagem, etiqueta do sabor, nome, nota média e total de avaliações, preço e descrição
- **Disponibilidade**: mostra "Em estoque (N unidades)"
- Seletor de quantidade e botão "Adicionar ao Carrinho - R$ X"
- Lista de avaliações do produto (nome do cliente, estrelas, comentário e data)

### 4. 🛒 Carrinho

- Abre como **painel lateral** ("Meu Carrinho"), pelo ícone do cabeçalho
- Lista de itens com imagem, preço, controles de quantidade (+/−) e botão de remover
- Subtotal e botão "Finalizar Pedido"

### 5. 💳 Checkout

- **Dados de Entrega**: nome completo, telefone, CEP, endereço (rua, número e complemento em um campo), cidade e estado. Os campos são preenchidos com os dados do perfil quando já cadastrados
- **Forma de Pagamento**: **PIX** (pagamento instantâneo), **Cartão de Crédito** (parcele em até 12x) e **Boleto** (vencimento em 3 dias)
- **Cupom**: campo "Código do cupom" para aplicar desconto
- **Resumo do Pedido**: itens, subtotal, entrega (**Grátis**) e total
- Botão "Ir para Pagamento", que leva à etapa de pagamento. **O pagamento é simulado**: nenhuma cobrança real é processada
- O pedido é criado com status **Aguardando Pagamento** e, após a confirmação simulada, passa para **Em Preparo** (histórico: "Pedido criado" e "Pagamento confirmado")
- O desconto do cupom e o código usado ficam gravados no pedido

### 6. 📦 Meus Pedidos e Rastreamento

- Lista dos pedidos do cliente, com número, data, valor e status
- Detalhe do pedido: itens, valores, endereço de entrega e **linha de progresso** do status
- Status do pedido: **Aguardando Pagamento → Em Preparo → Em Rota → Entregue**, além de **Cancelado**
- A atualização do status exige recarregar a página (não há atualização automática nem notificação)
- O cliente **não** possui botão para cancelar o pedido

### 7. ⭐ Avaliações

- As avaliações aparecem na página do produto e nos cards (nota média e quantidade)
- Os dados existentes foram cadastrados como exemplo; o app não exibe formulário para o cliente criar uma avaliação

### 8. 👤 Meu Perfil

- Campos editáveis: **telefone, CEP, endereço, cidade e estado**
- Botão "Salvar Alterações", botão "Voltar à Loja" e botão "Sair"

### 9. 🔐 Acesso

- Menu do usuário com: **Meus Pedidos, Meu Perfil, Painel Admin** (somente administradores) e **Sair**
- Login e cadastro gerenciados pela autenticação da plataforma Base44

---

## 🔧 PAINEL ADMINISTRATIVO

### 10. 📊 Dashboard

- **Cards**: Total Faturado, Pedidos Hoje, Produtos (com quantidade de itens em estoque baixo) e Pedidos Pendentes
- **Gráfico**: Produtos Mais Vendidos
- **Gráfico**: Pedidos por Status (Aguardando, Em Preparo, Em Rota, Entregue)
- **Lista**: Pedidos Recentes (número, cliente, data, valor e status) com link "Ver Todos"

### 11. 📦 Produtos

- Lista de produtos cadastrados, com criação, edição e remoção
- Campos do produto: nome, descrição, preço, sabor, estoque, **URL da imagem** e status ativo/inativo
- O estoque é um número por produto e é exibido ao cliente na página do produto
- Não há campo de "estoque mínimo": o alerta de estoque baixo no Dashboard usa um critério interno do app

### 12. 📋 Pedidos

- Lista de todos os pedidos, com filtros por status: **Todos, Aguardando, Em Preparo, Em Rota, Entregue**
- Detalhe do pedido: cliente, telefone, endereço, itens e valores
- **Atualização de status**: Aguardando Pagamento → Em Preparo → Em Rota → Entregue
- Não há aba de filtro para pedidos **Cancelado**, embora o status exista

### 13. 🎟️ Cupons

- Lista, criação e remoção de cupons
- Campos: código, tipo (percentual ou valor fixo), valor do desconto, **data de validade (única)**, limite de usos e status ativo/inativo
- Não existem data de início nem valor mínimo de pedido

### 14. 📈 Relatórios

- Relatórios de vendas e de produtos, com filtro de período
- Indicadores: total de vendas, quantidade de pedidos e ticket médio
- Exportação de dados

---

## 🔐 Controle de Acesso

| Perfil | Acesso |
|---|---|
| **Cliente** | Catálogo, busca e filtros, carrinho, checkout, Meus Pedidos, rastreamento, Meu Perfil |
| **Administrador** | Tudo do cliente, mais o Painel Administrativo (Dashboard, Produtos, Pedidos, Cupons, Relatórios) |

---

## 🚫 Fora do Escopo (Não Implementado)

- Pagamento real (gateway) e confirmação automática de pagamento
- Cálculo de frete (a entrega é sempre "Grátis"), previsão de entrega e código de rastreamento
- Notificações (e-mail, SMS, push) e atualização automática do status
- Cancelamento de pedido pelo cliente e filtro de cancelados no painel
- Múltiplos endereços por cliente, CPF e data de nascimento no perfil
- Alteração de senha dentro do app (a conta é gerenciada pela Base44)
- Upload de imagem do produto (usa URL), estoque mínimo configurável e exclusão lógica
- Ordenação do catálogo, filtro de disponibilidade e paginação
- Cupom com data de início ou valor mínimo de pedido
- Impressão de pedido, reembolso e histórico de alterações

---

## 🎯 Resumo

- **Cliente**: Catálogo, Busca e Filtros, Detalhe do Produto, Carrinho, Checkout (simulado), Meus Pedidos e Rastreamento, Avaliações (visualização), Perfil
- **Administrador**: Dashboard, Produtos, Pedidos, Cupons, Relatórios

---

**Documentação de Funcionalidades - App Cupcakes**  
*Última atualização: Novembro 2026*
