API Raízes do Nordeste

Projeto desenvolvido para a disciplina de Projeto Multidisciplinar (Trilha Back-End) do curso de Análise e Desenvolvimento de Sistemas da UNINTER.

A ideia aqui foi construir uma API REST para o sistema de uma rede de lanchonetes (Raízes do Nordeste). O sistema precisa lidar com pedidos vindo de vários lugares (App, Totem, Balcão, Web) e centralizar tudo.

Tecnologias 

Node.js com TypeScript

Express para criar o servidor e as rotas

PostgreSQL como banco de dados

Prisma como ORM pra facilitar a vida com o banco

JWT pra fazer a autenticação (login)

Swagger pra documentar a API

Como rodar o projeto na sua máquina

Se quiser testar o projeto, segue o passo a passo:

1. Clona o repositório

git clone https://github.com/andrezampar1-ops/Raizes-do-nordeste---back--end
cd raizes-do-nordeste-backend


2. Instala as paradas

npm install


3. Configura as variáveis de ambiente

Tem um arquivo chamado .env.example na raiz do projeto.

Copia ele e muda o nome pra .env.

Troca o valor do DATABASE_URL pra string de conexão do seu banco de dados Postgres (precisa ter um rodando).

Coloca uma senha no JWT_SECRET.

4. Cria o banco de dados

Com o Postgres rodando certinho e o .env configurado, roda esse comando pra criar as tabelas:

npx prisma migrate dev


5. Inicia o servidor

Pra rodar em modo de desenvolvimento:

npm run dev


Se tudo der certo, a API vai rodar em http://localhost:3000.

Documentação (Swagger)

A documentação das rotas, com o que precisa mandar e o que ela devolve, tá toda no Swagger.
Com a API rodando, é só acessar:
 http://localhost:3000/api-docs

Como testar (Postman)

Deixei a minha collection do Postman na raiz do projeto com os testes que fiz pra disciplina. O arquivo é o Postman_Collection_Raizes_Nordeste.json.

Abre o Postman.

Importa esse arquivo .json.

Dá uma olhada nas pastas.

Dica: Roda primeiro a rota de Login (POST /auth/login) pra pegar o token. Depois copia esse token e coloca na aba "Authorization -> Bearer Token" nas outras rotas pra conseguir testar (como a de criar pedido).

O fluxo que implementei

Foquei na parte principal que o roteiro pedia:

Tem que estar logado. Aí você manda a requisição pra criar o pedido e precisa informar de onde ele tá vindo (ex: APP ou BALCAO).

A API pega isso, valida e cria o pedido no banco com status de AGUARDANDO_PAGAMENTO.

Aí eu fiz um serviço falso (PagamentoMockService) que simula a maquininha aprovando ou não.

Se ele aprovar, o status do pedido muda pra PAGO.
