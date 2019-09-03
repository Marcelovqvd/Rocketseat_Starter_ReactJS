# Huntweb - Projeto Starter da Rocketseat

    $ yarn global add create-react-app

    $ create-react-app

O create-react-app vem com a transpilação configurada. Então não é preciso se preocupar em configurar Babel e Webpack.

Para rodar o servidor:

    $ yarn start

## O que são componentes

Neste projeto, é a prtir do index.js que se inicia toda a aplicação. Nele está se importando o React para poder usar a linguagem JSX. Também se importa o ReactDOM para fazer o ReactDOM.render().

#### ReactDOM.render()

É uma função que vai ser utilizada apenas uma vez. Ela vai renderizar o primeiro componente -> App.js

O App.js é uma classe que extende o Componente do React então por isso, o App.js é um componente.

Componente é um conjunto de parte estrutural (HTML), parte funcional (Javascript) e parte de estilização (CSS). Este 3 pontos estão encapsulados em um trecho de código.

#### render()

Todo componente tem um método obrigatório que é o render(). O render precisa retornar o contepudo JSX. Deve-se usar 'className' pq class é uma palavra reservada Javascript.

## Criando Header

Criar src/components/Header/index.js

Importar React. Não precisa do Component pq vai ser em formato de função -> Stateless Component
