Raízes do Nordeste - API Back-End

Este repositório contém o código-fonte da API REST desenvolvida para a rede de lanchonetes Raízes do Nordeste. O projeto foi elaborado como requisito de avaliação da disciplina de Projeto Multidisciplinar (Trilha Back-End) do curso de Análise e Desenvolvimento de Sistemas da UNINTER.

O objetivo principal desta API é centralizar o fluxo operacional da rede, garantindo suporte multicanal (App, Totem, Balcão, Web), controle de pedidos, gestão de stock, simulação de pagamentos e segurança (autenticação JWT).

  Tecnologias Utilizadas

Linguagem: Node.js com TypeScript

Framework Web: Express

Banco de Dados: PostgreSQL

ORM: Prisma

Segurança: JSON Web Token (JWT) e BCrypt (Hash de senhas)

Documentação: Swagger (OpenAPI)

  Pré-requisitos

Para executar este projeto localmente, vais precisar de ter instalado na tua máquina:

Node.js (versão 18 ou superior)

PostgreSQL (ou um container Docker com o Postgres)

Git

  Passo a Passo para Configuração e Execução

1. Clonar o repositório

git clone (https://github.com/andrezampar1-ops/Raizes-do-nordeste---back--end)
cd raizes-do-nordeste-backend


2. Instalar as dependências

npm install


3. Configurar Variáveis de Ambiente

Na raiz do projeto, existe um ficheiro chamado .env.example.

Cria uma cópia desse ficheiro e renomeia para .env.

Altera a variável DATABASE_URL com as tuas credenciais do PostgreSQL.

Define um "segredo" para a geração dos tokens JWT.

Exemplo do .env:

DATABASE_URL="postgresql://usuario:senha@localhost:5432/raizes_nordeste?schema=public"
JWT_SECRET="minha_chave_super_secreta_para_desenvolvimento"
PORT=3000


4. Criar o Banco de Dados e Rodar as Migrations

Com o PostgreSQL a rodar, executa o comando abaixo para que o Prisma crie as tabelas automaticamente no teu banco de dados:

npx prisma migrate dev --name init


(Opcional: Se tiveres um ficheiro de seed configurado para criar utilizadores ou produtos iniciais, roda npx prisma db seed)

5. Iniciar a API

Para iniciar o servidor em ambiente de desenvolvimento, executa:

npm run dev


A API estará disponível em: http://localhost:3000

📖 Documentação da API (Swagger)

Toda a documentação dos endpoints, incluindo contratos de request/response e status codes esperados, está disponível através do Swagger.

Com a API a rodar, acede no teu navegador:
👉 http://localhost:3000/api-docs

🧪 Como Rodar os Testes (Postman)

Os cenários de teste exigidos no projeto (fluxo principal, erros de autenticação, validações, etc.) foram exportados e encontram-se na pasta raiz do repositório no ficheiro:
📄 Postman_Collection_Raizes_Nordeste.json

Passo a passo para testar:

Abre o Postman.

Clica em Import (canto superior esquerdo) e seleciona o ficheiro .json mencionado acima.

A coleção inclui pastas divididas por recursos (Auth, Pedidos, Produtos).

Ordem sugerida:

Executa primeiro o POST /auth/login para obteres um token válido.

Copia o accessToken retornado e coloca-o no separador Authorization (Bearer Token) das rotas protegidas, como o POST /pedidos.

📌 Fluxo Principal Implementado (MVP)

O projeto foca no seguinte fluxo crítico exigido pela atividade:

Cliente autenticado (JWT) envia a criação de um pedido, informando obrigatoriamente o canal de origem (ex: APP, TOTEM).

A API valida a requisição e cria o pedido com o status AGUARDANDO_PAGAMENTO.

O serviço PagamentoMockService é acionado internamente.

Caso aprovado, o status do pedido é atualizado automaticamente para PAGO.

🤖 Declaração de Uso de Inteligência Artificial

Para a elaboração deste projeto e documentação, foram utilizadas ferramentas de Inteligência Artificial (modelos de linguagem) exclusivamente como apoio para:

Revisão ortográfica e gramatical.

Sugestões de formatação para Markdown e Swagger.

Auxílio na estruturação de exemplos de código boilerplate (configurações do Express).
