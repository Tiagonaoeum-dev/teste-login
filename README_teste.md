# Sistema GOV BR -- Portal de Autenticação com Testes Cypress

## Descrição do Projeto

Sistema web de autenticação que simula um portal governamental
brasileiro, com validações específicas (CPF, data de nascimento) e uma
suíte completa de testes automatizados utilizando Cypress.

## Funcionalidades Principais

### Sistema de Autenticação

-   Login por nome, CPF e senha
-   Cadastro completo com validação
-   Validações:
    -   CPF com dígitos verificadores
    -   Data de nascimento com idade mínima
    -   E-mail
    -   Força da senha
-   Armazenamento via localStorage
-   Interface responsiva com tema em cores do Brasil

### Testes Automatizados

-   7 suítes
-   23 casos de teste
-   Testes de responsividade
-   Cobertura completa dos fluxos do usuário

## Tecnologias Utilizadas

-   HTML5
-   CSS3
-   JavaScript ES6+
-   Cypress 13.6.0
-   Node.js 14+
-   LocalStorage

## Estrutura do Projeto

    projeto-gov-br/
    ├── index.html
    ├── homepage.html
    ├── app.js
    ├── styles.css
    ├── cypress/
    │   ├── e2e/
    │   │   └── login-cadastro.cy.js
    │   ├── support/
    │   │   ├── commands.js
    │   │   └── e2e.js
    │   └── fixtures/
    ├── cypress.config.js
    ├── package.json
    └── README.md

## Instalação e Configuração

### Pré-requisitos

-   Node.js 14+
-   NPM
-   Navegador moderno

### Passo 1 -- Clonar o Projeto

    git clone [url-do-repositorio]
    cd projeto-gov-br

Ou navegue até a pasta local:

    cd caminho/do/projeto

### Passo 2 -- Instalar Dependências

    npm install

### Passo 3 -- Iniciar o Servidor

    npm run serve

Alternativa:

    npx serve . -p 5500

### Passo 4 -- Acessar o Projeto

Acesse: http://localhost:5500

## Executando os Testes Cypress

### Método 1: Interface Gráfica

    npx cypress open

Passos: 1. Selecione E2E Testing 2. Escolha o navegador 3. Clique em
Start E2E Testing 4. Execute login-cadastro.cy.js

### Método 2: Terminal (Headless)

    npx cypress run

Opções:

    npx cypress run --spec "cypress/e2e/login-cadastro.cy.js"
    npx cypress run --browser chrome
    npx cypress run --browser firefox

## Suítes de Teste Implementadas

### 1. Carregamento da Página

-   Verifica elementos essenciais
-   Valida formulário ativo

### 2. Navegação entre Formulários

-   Alternância login ↔ cadastro

### 3. Validações de Login

-   Campos vazios
-   CPF inválido
-   Login com CPF par (sucesso)
-   Redirecionamento

### 4. Validações de Cadastro

-   Nome mínimo
-   CPF com 11 dígitos
-   E-mail válido
-   Senha 6--20
-   Confirmar senha
-   Aceite dos termos
-   Cadastro bem-sucedido

### 5. Fluxo Completo

Cadastro → Login → Dashboard

### 6. Testes da Homepage

-   Proteção de rota
-   Logout
-   Conteúdo da dashboard

### 7. Responsividade

-   Mobile
-   Tablet
-   Desktop

## Validações Implementadas

### Validação de CPF

-   11 dígitos
-   Máscara automática
-   Dígitos verificadores
-   CPF terminando em número par é considerado válido para testes

### Validação de Data

-   Formato YYYY-MM-DD
-   Impede datas futuras
-   Validação idade mínima 18 anos

### Validação de E-mail

Formato usuario@dominio.com

### Validação de Senha

-   6 a 20 caracteres
-   Força (fraca, média, forte)
-   Confirmação obrigatória

## Comandos Customizados do Cypress

    cy.login(nome, cpf, senha);
    cy.preencheCadastro(usuario);
    cy.limparLocalStorage();
    cy.alternarParaCadastro();
    cy.alternarParaLogin();
    cy.capturarScreenshot(nome);

## Scripts no package.json

    npm run serve
    npm test
    npm run test:open
    npm run test:chrome
    npm run test:firefox

## Dados de Teste

### CPFs válidos

-   12345678902
-   98765432104
-   11122233396

### CPFs inválidos

-   12345678901
-   98765432103
-   11122233395

### Usuário exemplo

    const usuarioTeste = {
      nome: 'Usuario Teste',
      cpf: '12345678902',
      dataNasc: '1990-01-01',
      email: 'teste@exemplo.com',
      senha: 'senha123'
    };

## Solução de Problemas Comuns

### Cypress não encontra servidor

    npx serve . -p 5500
    http://localhost:5500

### Erro: Cannot find module 'cypress'

    rm -rf node_modules package-lock.json
    npm install

### Timeout nos testes

Adicionar no cypress.config.js:

    defaultCommandTimeout: 10000

### LocalStorage não limpa entre testes

    beforeEach(() => {
      cy.limparLocalStorage();
      cy.visit('/');
    });

## Configuração do Cypress

    baseUrl: 'http://localhost:5500',
    viewportWidth: 1280,
    viewportHeight: 720,
    video: false,
    screenshotOnRunFailure: true,
    defaultCommandTimeout: 10000

## Personalização

### Alterar porta:

    baseUrl: 'http://localhost:3000'

    npx serve . -p 3000

### Criar novos testes:

    touch cypress/e2e/novos-testes.cy.js

### Modificar validações no app.js:

-   validarCPF()
-   validarDataNascimento()
-   validarSenha()

## Relatórios e Resultados

### Screenshots

Local: cypress/screenshots/

### Logs

-   Terminal
-   console.log() para depuração

## Considerações de Segurança

-   Não armazenar senhas reais em localStorage
-   Usar backend seguro
-   Hash com bcrypt/Argon2
-   HTTPS obrigatório
-   Validação no backend
-   JWT
-   Rate limiting
-   Auditoria

## Contribuição

    git checkout -b feature/nova-funcionalidade
    git commit -m 'Adiciona nova funcionalidade'
    git push origin feature/nova-funcionalidade

## Licença

MIT License.

## Autor

Seu Nome -- seu.email@dominio.com

## Nota Final

Projeto acadêmico. Ajustes recomendados para produção real.
