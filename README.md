# Admin — Explicações dos Códigos

Este diretório explica, de forma simples, **o que cada arquivo faz**.

## 1) `Códigos/index.html`
- **O que é:** Página principal da aplicação (Single Page Application).
- **O que faz:** Carrega a estrutura de navegação e a `<section id="view">` onde as telas aparecem.
- **Como liga os códigos:** Faz os imports de `styles.css` e `app.js` (no mesmo diretório).
- **Rotas (hash):**
  - `#/` – Início
  - `#/register` – Cadastro de usuário
  - `#/login` – Login
  - `#/dashboard` – Área autenticada do usuário comum
  - `#/admin/users` – Lista de usuários (apenas ADMIN)
  - `#/admin/users/edit?id=<ID>` – Edição de nome (apenas ADMIN)

## 2) `Códigos/styles.css`
- **O que é:** Folha de estilos (CSS).
- **O que faz:** Define o visual (cores, botões, cards, tabelas) e uma aparência moderna.
- **Por que está separado:** Facilita ajustes visuais sem alterar HTML/JS.

## 3) `Códigos/app.js`
- **O que é:** Lógica da aplicação (JavaScript).
- **Principais responsabilidades:**
  - **Roteamento por hash** (SPA): escolhe a view com base na URL (#/rota).
  - **Autenticação**: login e logout; guarda sessão no `localStorage`.
  - **Autorização (RBAC)**: bloqueia rotas de admin para não-admin.
  - **Cadastro**: valida campos; aplica **regras de senha** (8+ com maiúscula, minúscula, número, símbolo).
  - **ViaCEP**: ao preencher CEP, busca **UF** e **Cidade** automaticamente.
  - **Armazenamento**: usa `localStorage` como "banco de dados" local.
  - **Criptografia de senha**: usa `SHA-256` (SubtleCrypto) para salvar **hash**, não a senha em texto puro.
  - **Admin**: um usuário administrador é **criado automaticamente** se não existir:
    - E-mail: `admin@admin.com`
    - Senha: `Admin@123456` (você pode editar em `app.js`)
  - **Telas (views)**: início, cadastro, login, dashboard, lista admin, edição admin.

## Como funciona o fluxo
1. Ao abrir `index.html`, o app inicializa e cria o admin se for a primeira execução.
2. Você pode **Cadastrar** usuários (rota `#/register`).
3. Faça **Login** (rota `#/login`).
4. Acesse **Dashboard** (rota `#/dashboard`) para ver **seus dados** (apenas do usuário logado).
5. Se for **ADMIN**, acesse `#/admin/users` para **listar/editar/excluir** usuários.

## O que foi atendido do desafio
- Cadastro público (nome, e-mail, senha; opcional CEP/estado/cidade preenchidos por ViaCEP).
- Login público (e-mail/senha).
- Área autenticada (mensagem de boas-vindas e dados do próprio usuário).
- **Admin inicial** pré-configurado.
- Área de admin para **listar**, **editar nome** e **excluir** usuários.
- **Validações de formulário** no frontend + **regras de senha**.
- **Integração com API pública de CEP** (ViaCEP).
