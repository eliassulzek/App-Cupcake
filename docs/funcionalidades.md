# ✨ Funcionalidades do Sistema - App Cupcakes

## 📋 Visão Geral

O **App Cupcakes** oferece um conjunto completo de funcionalidades para clientes e administradores, proporcionando uma experiência de e-commerce moderna e eficiente.

---

## 👥 FUNCIONALIDADES DA ÁREA DO CLIENTE

### 1. 🏠 Página Inicial / Catálogo de Produtos

**Descrição**: Exibição visual de todos os cupcakes disponíveis para compra.

**Funcionalidades:**
- Visualização em grid responsivo (adapta-se a diferentes tamanhos de tela)
- Cards de produtos contendo:
  - Imagem do cupcake
  - Nome do produto
  - Preço unitário
  - Botão "Adicionar ao Carrinho"
- Paginação automática (exibe N produtos por página)
- Indicador visual de produtos sem estoque
- Destaque para produtos em destaque ou promoções

**Fluxo de Uso:**
```
1. Cliente acessa a página inicial
2. Sistema carrega produtos ativos com estoque disponível
3. Cliente visualiza o catálogo
4. Cliente pode clicar em um produto para ver detalhes
5. Cliente pode adicionar diretamente ao carrinho
```

---

### 2. 🔍 Busca e Filtros

**Descrição**: Sistema inteligente de busca e filtros para facilitar a localização de produtos.

#### 2.1 Busca Textual

**Funcionalidades:**
- Campo de busca visível no topo da página
- Busca por nome do produto
- Busca por palavras na descrição
- Resultados em tempo real (ou ao pressionar Enter)
- Destaque dos termos buscados nos resultados
- Mensagem quando nenhum resultado é encontrado

#### 2.2 Filtros

**Categorias/Sabores:**
- Chocolate
- Morango
- Baunilha
- Red Velvet
- Limão
- Outros sabores

**Faixa de Preço:**
- Menor preço primeiro
- Maior preço primeiro
- Preço personalizado (de R$ X até R$ Y)

**Disponibilidade:**
- Apenas produtos em estoque
- Todos os produtos

**Ordenação:**
- Mais relevantes
- Menor preço
- Maior preço
- Nome (A-Z)
- Mais recentes
- Mais vendidos

**Fluxo de Uso:**
```
1. Cliente digita termo de busca OU seleciona filtros
2. Sistema aplica filtros em tempo real
3. Catálogo é atualizado com produtos correspondentes
4. Cliente pode combinar múltiplos filtros
5. Cliente pode limpar filtros e retornar à visualização completa
```

---

### 3. 🛒 Carrinho de Compras

**Descrição**: Gerenciamento de produtos selecionados antes da finalização da compra.

**Funcionalidades:**

#### 3.1 Adicionar ao Carrinho
- Botão "Adicionar ao Carrinho" em cada produto
- Seleção de quantidade antes de adicionar
- Feedback visual quando produto é adicionado
- Ícone do carrinho atualiza com contador de itens
- Verificação automática de estoque disponível

#### 3.2 Visualizar Carrinho
- Lista completa de produtos adicionados
- Para cada item:
  - Imagem miniatura
  - Nome do produto
  - Preço unitário
  - Quantidade
  - Subtotal (preço × quantidade)
- **Total geral** em destaque

#### 3.3 Gerenciar Itens
- **Alterar Quantidade**: 
  - Botões de incremento (+) e decremento (-)
  - Campo editável de quantidade
  - Recálculo automático do subtotal
  - Validação de estoque disponível
  
- **Remover Item**:
  - Botão "Remover" ou ícone de lixeira
  - Atualização automática do total

#### 3.4 Informações Adicionais
- Mensagem se carrinho estiver vazio
- Botão "Continuar Comprando" (volta ao catálogo)
- Botão "Finalizar Compra" (vai para checkout)
- Salvar carrinho na sessão (persiste ao navegar)

**Fluxo de Uso:**
```
1. Cliente adiciona produtos ao carrinho
2. Contador do carrinho é atualizado
3. Cliente pode continuar comprando ou ir para o carrinho
4. No carrinho, cliente revisa itens
5. Cliente ajusta quantidades se necessário
6. Cliente remove itens indesejados
7. Cliente visualiza total e prossegue para checkout
```

---

### 4. 💳 Checkout e Finalização de Pedido

**Descrição**: Processo completo de finalização da compra.

#### 4.1 Etapa 1: Revisão do Pedido
- Listagem de todos os itens do carrinho
- Quantidades e preços
- Subtotal dos produtos

#### 4.2 Etapa 2: Dados Pessoais
- **Campos:**
  - Nome completo (preenchido automaticamente se logado)
  - Email
  - Telefone
- **Validações:**
  - Formato de email válido
  - Telefone no formato correto
  - Todos os campos obrigatórios preenchidos

#### 4.3 Etapa 3: Endereço de Entrega
- **Opção 1**: Usar endereço cadastrado
  - Lista de endereços salvos
  - Seleção do endereço desejado
  
- **Opção 2**: Informar novo endereço
  - CEP (com busca automática via API)
  - Logradouro
  - Número
  - Complemento
  - Bairro
  - Cidade
  - Estado

#### 4.4 Etapa 4: Cupom de Desconto
- Campo para inserir código do cupom
- Botão "Aplicar"
- Validações:
  - Cupom existe e está ativo
  - Cupom está dentro da validade
  - Cupom não atingiu limite de usos
  - Pedido atende valor mínimo
- Feedback visual:
  - ✅ Cupom aplicado com sucesso (mostra desconto)
  - ❌ Cupom inválido (mostra motivo)
- Cálculo automático:
  - Subtotal
  - Desconto (-)
  - **Total Final**

#### 4.5 Etapa 5: Método de Pagamento
- **Opções disponíveis:**
  - 💰 Pix (QR Code simulado)
  - 💳 Cartão de Crédito (dados simulados)
  - 📄 Boleto (código de barras simulado)
  - **Apenas a simulação do pagamento por pix está disponível.**

- **Cartão de Crédito:** (Não Implementado)
  - Número do cartão
  - Nome do titular
  - Data de validade
  - CVV
  - Número de parcelas

#### 4.6 Etapa 6: Confirmação
- Está disponível apenas para o pagamento por pix "Simular Pagamento Aprovado" 
- Resumo completo do pedido
- Termos e condições (checkbox obrigatório)
- Botão "Finalizar Pedido"

#### 4.7 Pós-Confirmação
- Mensagem de sucesso
- Número do pedido gerado
- Resumo do pagamento
- Botão "Acompanhar Pedido"
- Botão "Voltar à Loja"

**Fluxo de Uso:**
```
1. Cliente clica em "Finalizar Compra" no carrinho
2. Sistema valida se há itens no carrinho
3. Cliente preenche/confirma dados pessoais
4. Cliente seleciona/informa endereço de entrega
5. Cliente opcionalmente aplica cupom de desconto
6. Sistema valida cupom e aplica desconto
7. Cliente escolhe método de pagamento
8. Cliente preenche dados do pagamento
9. Cliente revisa resumo final
10. Cliente aceita termos e finaliza pedido
11. Sistema:
    - Cria registro do pedido
    - Cria itens do pedido
    - Atualiza estoque dos produtos
    - Cria registro de pagamento
    - Incrementa uso do cupom (se aplicável)
12. Cliente recebe confirmação com número do pedido
13. Carrinho é esvaziado
```

---

### 5. 📦 Histórico de Pedidos

**Descrição**: Visualização de todos os pedidos realizados pelo cliente.

**Funcionalidades:**
- Listagem de pedidos em ordem cronológica (mais recentes primeiro)
- Para cada pedido:
  - Número do pedido
  - Data e hora
  - Status atual (com ícone colorido)
  - Valor total
  - Método de pagamento
  - Botão "Ver Detalhes"

- **Filtros:**
  - Por status (Todos, Pendente, Em Andamento, Entregue, Cancelado)
  - Por data (Última semana, Último mês, Último ano)

- **Detalhes do Pedido:**
  - Todos os itens comprados (nome, quantidade, preço)
  - Endereço de entrega
  - Histórico de mudanças de status (timeline)

**Fluxo de Uso:**
```
1. Cliente acessa "Meus Pedidos"
2. Sistema lista todos os pedidos do cliente
3. Cliente pode filtrar por status ou data (Não Implementado)
4. Cliente clica em "Ver Detalhes" de um pedido
5. Sistema exibe informações completas do pedido
6. Cliente pode acompanhar status ou fazer nova compra
```

---

### 6. 📍 Rastreamento de Pedido

**Descrição**: Acompanhamento em tempo real do status do pedido.

**Status Disponíveis:**

1. **🔵 Aguardando Pagamento**
   - Pedido registrado no sistema
   - Pagamento aguardando confirmação

2. **🟡 Em Preparo**
   - Pagamento confirmado
   - Pedido em preparação na cozinha

3. **🟠 Em Rota**
   - Pedido despachado
   - A caminho do endereço do cliente

4. **🟢 Entregue**
   - Pedido entregue ao cliente
   - Finalizado com sucesso

5. **🔴 Cancelado** 
   - Existe o Status mas não tem botão para o cliente cancelar o pedido
   - Pedido cancelado
   - Motivo do cancelamento

**Interface:**
- **Progress Bar / Timeline Visual**
  - Representação gráfica do progresso
  - Status atual destacado
  - Status anteriores marcados como concluídos
  - Status futuros em cinza

- **Informações Adicionais:**
  - Data e hora de cada mudança de status
  - Previsão de entrega (Não Implementado)
  - Código de rastreamento (Não Implementado)

**Fluxo de Uso:**
```
1. Cliente acessa "Meus Pedidos"
2. Cliente clica no pedido desejado
3. Sistema exibe status atual e histórico
4. Cliente pode atualizar a página para ver mudanças
5. Cliente recebe notificação visual de mudanças (Não Implementado)
```

---

### 7. ⭐ Sistema de Avaliações

**Descrição**: Permite que clientes avaliem produtos comprados.

**Funcionalidades:**

#### 7.1 Visualizar Avaliações
- Exibição na página de detalhes do produto
- Para cada avaliação:
  - Nome do cliente
  - Nota (1 a 5 estrelas)
  - Comentário
  - Data da avaliação
- Média geral de avaliações (ex: 4.5/5)
- Total de avaliações recebidas
- Ordenação (mais recentes, mais úteis, maior nota)

#### 7.2 Criar Avaliação
- Disponível apenas para produtos já comprados
- Um cliente só pode avaliar cada produto uma vez
- **Formulário:**
  - Seleção de nota (1 a 5 estrelas)
  - Campo de comentário (opcional)
  - Botão "Enviar Avaliação"
- Confirmação após envio
- Avaliação aparece imediatamente no produto

**Fluxo de Uso:**
```
1. Cliente acessa histórico de pedidos
2. Cliente clica em "Avaliar" em um produto comprado
3. Sistema abre modal/página de avaliação
4. Cliente seleciona nota (estrelas)
5. Cliente escreve comentário (opcional)
6. Cliente envia avaliação
7. Sistema valida (se já não avaliou antes)
8. Sistema salva avaliação
9. Cliente recebe confirmação
10. Avaliação aparece na página do produto
```

---

### 8. 👤 Perfil do Usuário

**Descrição**: Gerenciamento completo dos dados pessoais do cliente.

**Funcionalidades:**

#### 8.1 Informações Pessoais
- Visualização de dados cadastrados:
  - Nome completo
  - Email
  - CPF
  - Telefone
  - Data de nascimento
- Botão "Editar Dados"
- Formulário de edição com validações
- Botão "Salvar Alterações"

#### 8.2 Endereços
- Lista de endereços cadastrados (Não Implementado)
- Para cada endereço:
  - Identificação (Casa, Trabalho, etc.) (Não Implementado)
  - Endereço completo
  - Opção de marcar como padrão (Não Implementado)
  - Botões "Editar" e "Excluir" (Não Implementado)
- Botão "Adicionar Novo Endereço" (Não Implementado)

#### 8.3 Segurança
- **Alterar Senha:**
  - Senha atual
  - Nova senha
  - Confirmar nova senha
  - Validação de complexidade
  
- **Logout:**
  - Botão para sair da conta
  - Confirmação opcional

#### 8.4 Histórico de Atividades (Não Implementado)
- Últimos pedidos realizados
- Últimas avaliações feitas
- Data do último login
- Estatísticas:
  - Total de pedidos
  - Total gasto
  - Produto favorito

**Fluxo de Uso:**
```
1. Cliente acessa "Meu Perfil"
2. Sistema exibe dados atuais do cliente
3. Cliente pode editar informações pessoais
4. Cliente pode gerenciar endereços
5. Cliente pode alterar senha
6. Cliente salva alterações
7. Sistema valida e atualiza dados
8. Cliente recebe confirmação
```

---

## 🔧 FUNCIONALIDADES DA ÁREA ADMINISTRATIVA

### 9. 📊 Dashboard Analítico

**Descrição**: Painel principal com visão geral do negócio.

**Métricas Principais (Cards):**

1. **Total de Vendas (Hoje)**
   - Valor total em R$

2. **Total de Pedidos (Hoje)**
   - Quantidade de pedidos
   - Quantidade de pedidos Pendentes

3. **Produtos**
   - Quantidade total de produtos
   - Alerta para produtos com estoque baixo

**Gráficos:**

1. **Vendas ao Longo do Tempo**
   - Gráfico de linha
   - Definição da quantidade de dias
   - Valor total por dia/mês

2. **Pedidos por Status**
   - Gráfico de pizza ou donut
   - Distribuição: Aguardando Pagamento, Em Preparo, Em Rota, Entregue

3. **Produtos Mais Vendidos**
   - Gráfico de barras horizontal
   - Top 10 produtos
   - Quantidade vendida

4. **Categorias Mais Vendidas**
   - Gráfico de barras
   - Vendas por sabor/categoria

**Tabelas:**

1. **Últimos Pedidos**
   - 10 pedidos mais recentes
   - Número, cliente, valor, status

2. **Produtos com Estoque Baixo**
   - Produtos abaixo do estoque mínimo
   - Alerta visual

**Fluxo de Uso:**
```
1. Admin faz login
2. Sistema redireciona para Dashboard
3. Admin visualiza métricas em tempo real
4. Admin pode filtrar por período
5. Admin identifica tendências e problemas
6. Admin toma ações (ex: repor estoque)
```

---

### 10. 📦 CRUD de Produtos

**Descrição**: Gerenciamento completo do catálogo de cupcakes.

#### 10.1 Listar Produtos

**Funcionalidades:**
- Tabela com todos os produtos
- Colunas:
  - Imagem (miniatura)
  - ID
  - Nome
  - Categoria
  - Preço
  - Estoque
  - Status (Ativo/Inativo)
  - Ações (Editar, Excluir, Ver)
  
- **Filtros:**
  - Por categoria
  - Por status (Ativo/Inativo)
  - Por faixa de estoque
  
- **Busca:**
  - Por nome
  - Por ID

- **Ordenação:**
  - Por nome, preço, estoque, data de cadastro

- **Paginação:**
  - X produtos por página
  - Navegação entre páginas

- **Ações em Lote:**
  - Ativar/Desativar múltiplos produtos
  - Exportar lista (CSV/Excel)

#### 10.2 Criar Produto

**Formulário:**
- **Nome do Produto** (obrigatório)
  - Texto, máx 100 caracteres
  
- **Descrição** (obrigatório)
  - Texto longo, até 500 caracteres
  
- **Preço** (obrigatório)
  - Número decimal, formato R$ 0,00
  - Validação: deve ser maior que 0
  
- **Categoria/Sabor** (obrigatório)
  - Seleção única: Chocolate, Morango, Baunilha, etc.
  
- **Quantidade em Estoque** (obrigatório)
  - Número inteiro, mínimo 0
  
- **Estoque Mínimo** (obrigatório)
  - Número inteiro, para alertas
  
- **Imagem do Produto** (obrigatório)
  - Upload de arquivo
  - Formatos aceitos: JPG, PNG
  - Tamanho máximo: 2MB
  - Preview antes de salvar
  
- **Status** (obrigatório)
  - Checkbox: Ativo/Inativo
  - Padrão: Ativo

**Botões:**
- "Salvar e Adicionar Outro"
- "Salvar e Voltar para Lista"
- "Cancelar"

**Validações:**
- Todos os campos obrigatórios preenchidos
- Preço válido e positivo
- Imagem no formato correto
- Nome único (sem duplicatas)

#### 10.3 Editar Produto

**Funcionalidades:**
- Formulário preenchido com dados atuais
- Mesmo layout do formulário de criação
- Possibilidade de alterar imagem (upload nova ou manter atual)
- Botão "Salvar Alterações"
- Botão "Cancelar"
- Histórico de alterações (quem editou, quando)

#### 10.4 Excluir Produto

**Funcionalidades:**
- Confirmação obrigatória antes de excluir
- Mensagem de aviso se produto tem pedidos vinculados
- Opção de desativar ao invés de excluir
- Exclusão lógica (produto fica no banco, mas inativo)

**Fluxo de Uso:**
```
1. Admin acessa "Produtos"
2. Sistema lista todos os produtos
3. Admin pode:
   a. Criar novo produto → Preenche formulário → Salva
   b. Editar produto → Altera dados → Salva
   c. Excluir produto → Confirma → Produto removido/desativado
   d. Filtrar/Buscar produtos → Visualiza resultados
4. Sistema valida e processa ação
5. Admin recebe confirmação
6. Lista é atualizada
```

---

### 11. 📦 Gestão de Estoque

**Descrição**: Controle e atualização de quantidades disponíveis.

**Funcionalidades:**

#### 11.1 Visualização de Estoque
- Listagem de produtos com foco no estoque
- Colunas:
  - Nome do produto
  - Categoria
  - Quantidade atual
  - Estoque mínimo
  - Status (indicador visual)
- Cores/ícones:
  - Sem alteração se tiver estoque
  - Ícone de Aviso com pouco estoque

#### 11.2 Atualização Rápida
- Campo editável inline na tabela
- Botão "Salvar Alterações"

#### 11.3 Entrada de Estoque
- Formulário dedicado:
  - Nome
  - Descrição
  - Sabor
  - Preço
  - Estoque
  - Imagem

**Fluxo de Uso:**
```
1. Admin acessa "Produtos"
2. Sistema lista produtos com status "Ativo" ou "Inativo"
3. Admin identifica produtos com estoque baixo
4. Admin registra entrada de estoque:
   - Seleciona produto
   - Informa quantidade recebida
   - Salva
5. Sistema atualiza quantidade disponível
6. Admin visualiza estoque atualizado
```

---

### 12. 📋 Gerenciamento de Pedidos

**Descrição**: Controle completo de todos os pedidos do sistema.

**Funcionalidades:**

#### 12.1 Listagem de Pedidos

**Visualização:**
- Tabela com todos os pedidos
- Colunas:
  - Número do pedido
  - Data/hora
  - Cliente (nome)
  - Valor total
  - Status (com cor)
  - Ações

**Filtros:**
- Por status (Todos, Aguardando, Preparo, Em Rota, Entregue, Cancelado)

**Ordenação:**
- Mais recentes primeiro (padrão)
- Por status

**Paginação:**
- X pedidos por página
- Total de pedidos exibido

#### 12.2 Detalhes do Pedido

**Informações Exibidas:**

1. **Dados do Pedido:**
   - Número do pedido
   - Data e hora
   - Status atual

2. **Dados do Cliente:**
   - Nome
   - Telefone

3. **Endereço de Entrega:**
   - Endereço completo
   - CEP

4. **Itens do Pedido:**
   - Tabela com produtos
   - Quantidade de cada item
   - Preço unitário
   - Subtotal

5. **Resumo Financeiro:**
   - Subtotal dos produtos
   - Desconto (se houver cupom)
   - **Total Final**

6. **Informações de Pagamento:** (Não Implementado)
   - Método escolhido
   - Status do pagamento
   - Data de confirmação (se aplicável)
   - Código da transação

7. **Histórico de Status:**
   - Timeline com todas as mudanças
   - Data/hora de cada mudança

#### 12.3 Atualização de Status

**Interface:**
- Dropdown/select com opções de status
- Botão "Atualizar Status"
- Confirmação visual após atualização
- Registro automático no histórico

**Opções de Status:**
1. **Aguardando Pagamento** → **Em Preparo**
2. **Em Preparo** → **Em Rota**
3. **Entregue** → **Cancelado**
4. Qualquer status → **Cancelado**

**Regras:** (Não Implementado)
- Status deve seguir fluxo lógico
- Não é possível voltar status (exceto para Cancelado)
- Cancelamento requer confirmação e motivo
- Ao marcar como Entregue, pedido é finalizado

#### 12.4 Ações Adicionais (Não Implementado)

- **Imprimir Pedido:**
  - Gera versão para impressão
  - Formato de recibo/nota de pedido
  
- **Enviar Email ao Cliente:**
  - Notificação de atualização de status
  - Confirmação de entrega
  
- **Reembolsar/Cancelar:**
  - Cancela pedido
  - Opção de reembolso (simulado)
  - Devolve produtos ao estoque

- **Ver Cliente:**
  - Acesso rápido ao perfil do cliente
  - Histórico de pedidos do cliente

**Fluxo de Uso:**
```
1. Admin acessa "Gerenciamento de Pedidos"
2. Sistema lista pedidos (por padrão, pendentes primeiro)
3. Admin pode filtrar por status/data
4. Admin clica em um pedido para ver detalhes
5. Admin atualiza status conforme preparação/entrega:
   - Pedido Recebido → marca como "Preparando"
   - Pedido Pronto → marca como "Em Entrega"
   - Pedido Entregue → marca como "Entregue"
6. Sistema registra mudança e notifica cliente (opcional)
7. Admin pode imprimir pedido ou enviar comunicação
```

---

### 13. 🎟️ Sistema de Cupons

**Descrição**: Criação e gestão de cupons de desconto promocionais.

**Funcionalidades:**

#### 13.1 Listar Cupons

**Visualização:**
- Tabela com todos os cupons
- Colunas:
  - Código
  - Tipo (Percentual/Valor Fixo)
  - Valor do Desconto
  - Validade (Data início - Data fim)
  - Usos (Usado/Total)
  - Status (Ativo/Inativo)
  - Ações (Remover)

#### 13.2 Criar Cupom

**Formulário:**

1. **Código do Cupom** (obrigatório)
   - Texto, ex: BEMVINDO10, NATAL25
   - Sem espaços, maiúsculas
   - Único no sistema

2. **Tipo de Desconto** (obrigatório)
   - Radio button:
     - ( ) Percentual (%)
     - ( ) Valor Fixo (R$)

3. **Valor do Desconto** (obrigatório)
   - Se Percentual: 1 a 100
   - Se Valor Fixo: R$ 0,01 ou mais

4. **Período de Validade** (obrigatório)
   - Data de início
   - Data de fim
   - Validação: data fim >= data início

5. **Quantidade de Usos** 
   - Número máximo de vezes que pode ser usado
   - 0 = ilimitado
   - Padrão: 0

6. **Status** (obrigatório)
   - Checkbox: Ativo/Inativo
   - Padrão: Ativo

**Botões:**
- "Novo Cupom"
- "Criar"
- "Cancelar"

**Validações:**
- Código único (não pode existir outro igual)
- Período de validade válido
- Valor de desconto dentro dos limites
- Percentual não pode ser maior que 100%

#### 13.3 Editar Cupom

**Funcionalidades:**
- Formulário preenchido com dados atuais
- Todas as configurações editáveis
- Botão "Salvar Alterações"
- **Atenção:** Alterar cupom não afeta pedidos já realizados

#### 13.4 Desativar/Excluir Cupom

**Funcionalidades:**
- **Desativar:** Cupom permanece no sistema mas não pode ser usado
- **Excluir:** Remove cupom (só se não foi usado em nenhum pedido)
- Confirmação obrigatória

#### 13.5 Estatísticas de Cupom

**Métricas:**
- Total de vezes usado
- Total de desconto concedido (R$)

**Fluxo de Uso:**
```
1. Admin acessa "Cupons"
2. Sistema lista cupons existentes
3. Admin clica em "Criar Novo Cupom"
4. Admin preenche formulário:
   - Define código (ex: NATAL25)
   - Escolhe tipo (25% de desconto)
   - Define validade (01/12 a 31/12)
   - Define limite (100 usos)
5. Admin salva cupom
6. Sistema valida e cria cupom
7. Cupom fica disponível para uso pelos clientes
8. Admin pode acompanhar uso na listagem
```

---

### 14. 📊 Relatórios

**Descrição**: Geração de relatórios analíticos para tomada de decisão.

**Tipos de Relatórios:**

#### 14.1 Relatório de Vendas

**Filtros:**
- Período (data início e fim)
- Status do pedido
- Método de pagamento

**Dados Exibidos:**
- Total de vendas (R$)
- Quantidade de pedidos
- Ticket médio

**Exportação:**
- JSON
- CSV

#### 14.2 Relatório de Produtos

**Filtros:**
- Categoria
- Período
- Ordenação (mais vendidos, menos vendidos)

**Dados Exibidos:**
- Lista de produtos
- Quantidade vendida de cada
- Participação no faturamento (%)
- Produtos mais vendidos (top 10)

---

## 🔐 Controle de Acesso

### Níveis de Permissão

#### Cliente (Usuário Final)
✅ **Permitido:**
- Acessar catálogo
- Buscar e filtrar produtos
- Adicionar ao carrinho
- Finalizar compra
- Ver histórico de pedidos
- Rastrear pedidos
- Avaliar produtos
- Editar próprio perfil

❌ **Negado:**
- Acessar painel administrativo
- Ver pedidos de outros clientes
- Alterar preços ou produtos
- Gerenciar estoque

#### Administrador
✅ **Permitido:**
- **Todas as funcionalidades do cliente, MAIS:**
- Acessar dashboard administrativo
- CRUD completo de produtos
- Gerenciar estoque
- Ver e gerenciar todos os pedidos
- Atualizar status de pedidos
- Criar e gerenciar cupons
- Gerar relatórios
- Ver dados de todos os clientes (Não Implementado)

❌ **Negado:**
- Excluir pedidos finalizados (apenas cancelar)
- Alterar dados de pagamento de pedidos concluídos

---

## 🎯 Resumo de Funcionalidades

### Cliente (9 módulos principais)
1. ✅ Catálogo de Produtos
2. ✅ Busca e Filtros
3. ✅ Carrinho de Compras
4. ✅ Checkout Completo
5. ✅ Histórico de Pedidos
6. ✅ Rastreamento
7. ✅ Avaliações
8. ✅ Perfil
9. ✅ Autenticação (Login/Logout)

### Administrador (6 módulos principais)
1. ✅ Dashboard Analítico
2. ✅ CRUD de Produtos
3. ✅ Gestão de Estoque
4. ✅ Gerenciamento de Pedidos
5. ✅ Sistema de Cupons
6. ✅ Relatórios

---

**Total: 15 módulos funcionais completos**

---

## 🚀 Diferenciais do Sistema

- 💻 **Interface Responsiva**: Funciona em desktop, tablet e mobile
- ⚡ **Performance**: Carregamento rápido e operações ágeis
- 🔒 **Segurança**: Autenticação e validações em todas as operações
- 📊 **Relatórios Completos**: Dados para tomada de decisão
- 🎨 **Design Moderno**: Interface intuitiva e agradável
- 🔄 **Atualizações em Tempo Real**: Status e métricas sempre atualizados

---

**Documentação de Funcionalidades - App Cupcakes**  
*Última atualização: Dezembro 2025*
