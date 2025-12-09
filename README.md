# 🧁 App Cupcakes

[![Base44 No-Code](https://img.shields.io/badge/Built%20with-Base44-blue)](https://base44.com)
[![Status](https://img.shields.io/badge/Status-Em%20Produção-success)]()
[![Documentation](https://img.shields.io/badge/Docs-Completa-brightgreen)](./docs)

![Home] (./docs/prints/home.png)

## 📱 Sobre o Projeto

O **App Cupcakes** é uma plataforma completa de e-commerce especializada na venda de cupcakes artesanais, desenvolvida inteiramente na plataforma No-Code **Base44**. O sistema oferece uma experiência moderna e intuitiva tanto para clientes quanto para administradores.

### 🔗 Sistema Publicado

> **Link da Aplicação (Produção):** `https://cupcake-delight-ebdbb888.base44.app`

---

## ✨ Funcionalidades Principais

### 👥 Área do Cliente

- **Catálogo de Produtos**: Visualização completa dos cupcakes disponíveis com fotos e descrições
- **Busca e Filtros**: Sistema de busca inteligente com filtros por categoria, preço e sabor
- **Carrinho de Compras**: Adição, remoção e ajuste de quantidades
- **Checkout Simplificado**: Processo de compra rápido e intuitivo
- **Pagamento Simulado**: Sistema de pagamento para demonstração (Pix, Cartão, Boleto)
- **Histórico de Pedidos**: Acompanhamento completo de todas as compras
- **Status em Tempo Real**: Rastreamento do pedido (Aguardando Pagamento → Em Preparo → Em Rota → Entregue)
- **Sistema de Avaliações**: Avaliação de produtos e experiência de compra
- **Perfil do Usuário**: Gerenciamento de dados pessoais e endereços

### 🔧 Área Administrativa

- **Dashboard Analítico**: Visão geral de vendas, pedidos e performance
- **Gráficos e Métricas**: Análise visual de vendas por período, produtos mais vendidos
- **CRUD de Produtos**: Cadastro completo de cupcakes (nome, descrição, preço, imagem, categoria)
- **Gestão de Estoque**: Controle de quantidade disponível e alertas de estoque baixo
- **Gerenciamento de Pedidos**: Visualização e atualização de status dos pedidos
- **Sistema de Cupons**: Criação e gestão de cupons de desconto
- **Relatórios**: Exportação de dados de vendas e pedidos nos formatos CSV e JSON

---

## 🏗️ Arquitetura

O App Cupcakes utiliza a arquitetura serverless e a infraestrutura No-Code da Base44, permitindo desenvolvimento rápido, escalabilidade automática e deploy sem necessidade de configuração de servidores.

- **Frontend**: Interface responsiva gerada automaticamente pela Base44
- **Backend**: API REST serverless com lógica de negócios configurada visualmente
- **Banco de Dados**: PostgreSQL gerenciado (relacional)
- **Autenticação**: Sistema de login e controle de acesso nativo da Base44
- **Deploy**: Publicação automática e hospedagem em infraestrutura cloud

> 📖 Para detalhes completos da arquitetura, consulte: [docs/arquitetura.md](./docs/arquitetura.md)

---

## 📂 Estrutura do Repositório

```
app-cupcakes/
│
├─ README.md                          # Este arquivo
│
├─ docs/                              # Documentação completa do projeto
│  ├─ AVISO.md                        # Informações sobre código-fonte
│  ├─ arquitetura.md                  # Arquitetura detalhada do sistema
│  ├─ modelagem-de-dados.md           # Esquema do banco de dados
│  ├─ funcionalidades.md              # Documentação de todas as funcionalidades
│  ├─ testes.md                       # Casos de teste e resultados
│  ├─ laudo-de-qualidade.md           # Relatório de qualidade do sistema
│  └─ prints/                         # Capturas de tela
│      ├─ cliente/                    # Telas da área do cliente
│      └─ admin/                      # Telas da área administrativa
│
└─ pit/                               # Documentos do PIT (Projeto Integrador)
   ├─ PIT_respostas.md                # Respostas completas do PIT
   └─ video_roteiro.md                # Roteiro para vídeo de apresentação
```

---

## 📚 Documentação

Toda a documentação técnica e funcional do projeto está organizada na pasta [`/docs`](./docs):

- **[AVISO.md](./docs/AVISO.md)**: Informações importantes sobre a natureza No-Code do projeto
- **[arquitetura.md](./docs/arquitetura.md)**: Descrição técnica da arquitetura e infraestrutura
- **[modelagem-de-dados.md](./docs/modelagem-de-dados.md)**: Modelo completo do banco de dados
- **[funcionalidades.md](./docs/funcionalidades.md)**: Documentação detalhada de todas as features
- **[testes.md](./docs/testes.md)**: Plano de testes, casos de teste e resultados
- **[laudo-de-qualidade.md](./docs/laudo-de-qualidade.md)**: Avaliação da qualidade do sistema

---

## 🔴 Importante: Código-Fonte

> ⚠️ **Este repositório contém apenas DOCUMENTAÇÃO**

A plataforma **Base44** é uma ferramenta No-Code que não permite a exportação de código-fonte. Todo o desenvolvimento foi realizado através de interface visual, com configurações e lógica de negócios definidas diretamente na plataforma.

**O que você encontrará aqui:**
- ✅ Documentação completa do projeto
- ✅ Modelagem de dados e arquitetura
- ✅ Descrição de funcionalidades
- ✅ Casos de teste e laudos de qualidade
- ✅ Roteiros e materiais do PIT

**O que NÃO está neste repositório:**
- ❌ Código-fonte (não exportável da Base44)
- ❌ Arquivos de configuração de build
- ❌ Dependências de pacotes

Para mais informações, leia: [docs/AVISO.md](./docs/AVISO.md)

---

## 📋 PIT - Projeto Integrador de Tecnologia

Os arquivos relacionados ao Projeto Integrador estão na pasta [`/pit`](./pit):

- **[PIT_respostas.md](./pit/PIT_respostas.md)**: Respostas completas para todas as questões do PIT
- **[video_roteiro.md](./pit/video_roteiro.md)**: Roteiro estruturado para o vídeo de apresentação

---

## 🚀 Como Visualizar o Sistema

O sistema está publicado e acessível através da plataforma Base44. Utilize o link fornecido acima para acessar a aplicação em produção.

### Credenciais para Teste (Cliente)
O avaliador pode também criar sua própria conta via interface de cadastro.

A plataforma Base44 utiliza verificação por e-mail (código de autenticação).
Por esse motivo, contas de demonstração não são fornecidas, já que não seria possível
receber o código de verificação em e-mails fictícios.

### Credenciais de Administrador
A autenticação administrativa é gerenciada pela Base44.
Apenas o Owner possui permissões de administrador.
As funcionalidades do painel admin serão demonstradas no vídeo do PIT.

---

## 👨‍💻 Desenvolvimento

**Plataforma**: Base44 No-Code Platform  
**Tipo de Projeto**: E-commerce de Cupcakes  
**Modelo**: B2C (Business to Consumer)  
**Ambiente**: Cloud (Serverless)

---

## 📞 Contato

Desenvolvedor: Elias Gonçalves Sulzek  

RGM: 30152267

E-mail para contato acadêmico: elias.sulzek@cs.up.edu.br

Linkedin: https://www.linkedin.com/in/elias-sulzek-26b259233/

GitHub: https://github.com/eliassulzek

---

## 📄 Licença

Este repositório é destinado exclusivamente para fins acadêmicos.
Não possui fins comerciais e não inclui código-fonte exportável.

---

**Desenvolvido por Elias Gonçalves Sulzek usando Base44 No-Code Platform**