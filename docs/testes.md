# 🧪 Testes do Sistema - App Cupcakes

## 📋 Visão Geral

Este documento registra os testes manuais realizados no sistema **App Cupcakes**, os bugs encontrados durante o desenvolvimento e as correções aplicadas.

> Os testes foram **manuais**, executados pelo próprio desenvolvedor, sem automação e sem avaliação de terceiros. Os dados usados (nomes, e-mails, CPF) são fictícios.

---

## 🎯 Objetivos dos Testes

- Validar as funcionalidades principais do sistema
- Identificar e corrigir bugs antes da publicação
- Verificar o comportamento em diferentes tamanhos de tela
- Conferir a separação de acesso entre Cliente e Administrador

---

## 📝 Metodologia

1. **Testes funcionais manuais**: fluxos completos de uso e regras de negócio (carrinho, checkout, cupons, pedidos)
2. **Testes de validação**: campos obrigatórios e formatos (e-mail, CPF, telefone)
3. **Testes de responsividade**: verificação visual em desktop, tablet e celular
4. **Testes de acesso**: conferência de que o cliente não acessa o painel administrativo

O pagamento é **simulado** (apenas Pix), então o fluxo de pagamento real não foi testado.

---

## 📊 Modelo de Caso de Teste

| Campo | Descrição |
|-------|-----------|
| **ID** | Identificador único do teste |
| **Módulo** | Área do sistema testada |
| **Caso de Teste** | O que será testado |
| **Pré-condições** | Requisitos antes do teste |
| **Passos** | Ações para executar o teste |
| **Resultado Esperado** | Comportamento esperado |
| **Resultado Obtido** | Comportamento observado |
| **Status** | ✅ Passou / ❌ Falhou |

---

## 🧪 Casos de Teste Documentados

### TC-001: Cadastro de Novo Cliente

| Campo | Conteúdo |
|-------|----------|
| **Módulo** | Autenticação - Cadastro |
| **Caso de Teste** | Cadastro de novo cliente com dados válidos |
| **Pré-condições** | Usuário não está logado; acesso à página de cadastro |
| **Passos** | 1. Acessar a página de cadastro<br>2. Preencher nome, e-mail, CPF e telefone (dados fictícios)<br>3. Preencher e confirmar a senha<br>4. Preencher o endereço<br>5. Clicar em "Cadastrar" |
| **Resultado Esperado** | Sistema valida os dados, cria a conta e redireciona para o catálogo ou login |
| **Resultado Obtido** | Conta criada com sucesso; usuário redirecionado ao catálogo já autenticado |
| **Status** | ✅ **PASSOU** |

---

### TC-002: Adicionar Produto ao Carrinho

| Campo | Conteúdo |
|-------|----------|
| **Módulo** | Cliente - Carrinho |
| **Caso de Teste** | Adicionar produto disponível ao carrinho |
| **Pré-condições** | Cliente logado; produto com estoque |
| **Passos** | 1. Acessar o catálogo<br>2. Clicar em "Adicionar ao Carrinho" em um produto com estoque<br>3. Verificar o contador do carrinho<br>4. Abrir o carrinho |
| **Resultado Esperado** | Produto adicionado com quantidade 1; contador incrementa; carrinho mostra nome, preço e quantidade |
| **Resultado Obtido** | Produto adicionado corretamente; contador e carrinho atualizados |
| **Status** | ✅ **PASSOU** |

---

### TC-003: Aplicar Cupom de Desconto

| Campo | Conteúdo |
|-------|----------|
| **Módulo** | Cliente - Checkout / Cupom |
| **Caso de Teste** | Aplicar cupom percentual válido |
| **Pré-condições** | Cliente logado; carrinho com subtotal de R$ 50,00; cupom de 10% ativo e dentro da validade |
| **Passos** | 1. Ir para o checkout<br>2. Informar o código do cupom<br>3. Clicar em "Aplicar"<br>4. Conferir desconto e total |
| **Resultado Esperado** | Mensagem de sucesso; desconto de R$ 5,00; total de R$ 45,00 |
| **Resultado Obtido** | Cupom validado; desconto de R$ 5,00; total de R$ 45,00 |
| **Status** | ✅ **PASSOU** |

---

### TC-004: Finalizar Pedido (Fluxo Completo)

| Campo | Conteúdo |
|-------|----------|
| **Módulo** | Cliente - Checkout / Pedido |
| **Caso de Teste** | Compra completa do início ao fim com pagamento simulado |
| **Pré-condições** | Cliente logado; produtos com estoque |
| **Passos** | 1. Adicionar 2 produtos ao carrinho<br>2. Ir para o checkout e confirmar dados e endereço<br>3. Escolher Pix (simulado)<br>4. Aceitar os termos<br>5. Finalizar o pedido |
| **Resultado Esperado** | Pedido criado; estoque atualizado; carrinho esvaziado; status "Aguardando Pagamento"; número do pedido exibido |
| **Resultado Obtido** | Pedido criado com sucesso; estoque atualizado; carrinho esvaziado; confirmação exibida |
| **Status** | ✅ **PASSOU** |

---

### TC-005: Admin - Atualizar Status do Pedido

| Campo | Conteúdo |
|-------|----------|
| **Módulo** | Admin - Gerenciamento de Pedidos |
| **Caso de Teste** | Alterar o status de "Aguardando Pagamento" para "Em Preparo" |
| **Pré-condições** | Admin logado; pedido existente |
| **Passos** | 1. Abrir "Gerenciamento de Pedidos"<br>2. Abrir os detalhes de um pedido<br>3. Selecionar o novo status<br>4. Clicar em "Atualizar Status" |
| **Resultado Esperado** | Status atualizado e histórico registrado com data/hora |
| **Resultado Obtido** | Status atualizado; histórico registrado; cliente vê o novo status ao atualizar a página |
| **Status** | ✅ **PASSOU** |

---

## 🐛 Bugs Encontrados Durante o Desenvolvimento

### Bug #01: CPF aceito sem formatação
**Severidade**: 🟡 Média | **Status**: ✅ Corrigido

O cadastro aceitava CPF sem pontos e traço, enquanto outras telas exibiam o formato com máscara, gerando inconsistência.
**Correção**: máscara automática de CPF nos formulários.

### Bug #02: Total do carrinho não atualizava
**Severidade**: 🔴 Alta | **Status**: ✅ Corrigido

Ao alterar a quantidade com os botões +/-, o subtotal e o total só atualizavam após recarregar a página.
**Correção**: recálculo imediato ao alterar a quantidade.

### Bug #03: Cupom expirado era aceito
**Severidade**: 🔴 Alta | **Status**: ✅ Corrigido

Cupons fora do período de validade ainda podiam ser aplicados.
**Correção**: validação de data de início e fim ao aplicar o cupom, com a mensagem "Cupom expirado".

### Bug #04: Estoque podia ficar negativo
**Severidade**: 🔴 Alta | **Status**: ✅ Corrigido

Pedidos feitos ao mesmo tempo podiam deixar o estoque negativo.
**Correção**: verificação de estoque no momento da finalização do pedido, rejeitando com "Estoque insuficiente".

### Bug #05: Filtro de preço retornava produtos fora da faixa
**Severidade**: 🟡 Média | **Status**: ✅ Corrigido

O filtro por faixa de preço exibia produtos fora do intervalo.
**Correção**: condição do filtro ajustada para respeitar mínimo **e** máximo.

### Resumo

| Bug | Descrição | Severidade | Status |
|-----|-----------|------------|--------|
| #01 | CPF sem formatação aceito | 🟡 Média | ✅ Corrigido |
| #02 | Total do carrinho não atualiza | 🔴 Alta | ✅ Corrigido |
| #03 | Cupom expirado aceito | 🔴 Alta | ✅ Corrigido |
| #04 | Estoque negativo | 🔴 Alta | ✅ Corrigido |
| #05 | Filtro de preço incorreto | 🟡 Média | ✅ Corrigido |

---

## 🧪 Responsividade

O layout foi verificado visualmente em desktop (1920x1080 e 1366x768), tablet (768x1024) e celulares de tela pequena e média.

---

## 🔒 Controle de Acesso

- Cliente não acessa o painel administrativo
- Rotas protegidas redirecionam para o login
- Cliente não visualiza pedidos de outros clientes

---

## ⚠️ Limitações dos Testes

- Não há testes automatizados (o código não é exportável da Base44)
- Não foram feitos testes de carga, de desempenho medido nem auditoria de segurança
- Pagamento simulado: não há teste com gateway real
- Funcionalidades marcadas como "Não Implementado" em [funcionalidades.md](./funcionalidades.md) não foram testadas

---

## 🎯 Próximos Passos

- Registrar os casos de teste restantes no mesmo modelo
- Testes automatizados E2E (Cypress/Playwright) caso o sistema seja reconstruído com código acessível
- Testes de carga e de segurança antes de qualquer uso comercial real
- Testes de usabilidade com usuários reais

---

**Documento de Testes - App Cupcakes**  
*Última atualização: Novembro 2026*
