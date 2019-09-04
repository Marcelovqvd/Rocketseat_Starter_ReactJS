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

#### estilizando o componente Header

criar src/components/Header/style.css

Com React não vamos criar um link no HTML para pegar o CSS. Vamo sutilizar tudo dentro da pasta src e tudo vai passar pelo Javascript. Então deve-=se fazer o import do CSS no Header/index.js ---> import './styles.css';

#### criando estilo global

criar src/styles.css e importá-lo no App.js

## Buscando produtos da API

Buscar produtos da API e exibí-los em tela

Para poder acessar informações de uma API Rest vamos usar a biblioteca axios

## Axios

    $ yarn add axios

criar src/services/api.js

const api = axios.create({baseURL:''}) --> baseURL da qual todas as requisições vão partir

importar api em App.js

A aplicação vai ter algumas páginas. Então a listagem de produtos vai ficar em:

src/pages/main/index.js

Este index.js vai ser componente em formato de classe

Agora é preciso buscar as informações que estão na rota da api seguida de products --> baseURL/products

#### Métodos de ciclo de vida

Métodos que executam automaticamente baseados no ciclo de vida do componente.

componentDidMount() --> este método é executado quando o componente for mostrado em tela. Se precisar de uma ação logo que o componente for exibido em tela, utilizamos este método.

Aqui ele vai retornar a função loadProducts na forma de arrow function para ter acesso ao escopo do this.

Executar a api com o get --> api.get('/products');

Com isso tem acesso ao objeto que tem a resposta da chamada em 'data'. Dentro de 'data ficam os docs onde estão os produtos que se quer mostrar na tela.

# Armazenando no state

No React, quando se quer armazenar informações puxadas de uma api, isso não se faz da forma tradicional, armazenando em uma variável. Para isso se usa o state.

#### state

O state é uma variável que armazena um objeto. É nele que vamos armazenar as informações buscadas em uma api. Aqui, o objeto do state vai ter a propriedade 'products' que é um array vazio que vai ser preenchido.

É preciso armazenar em um state, e não em uma variável qualquer porque assim é possível fazer com que o método render() dependa do state, escute as alterações ocorridas no state. Assim, o render() vai executar automaticamente quando houver alterações no state.

Aqui, vamos mostrar no render a contagem de quantos produtos se tem na api.

Considerando que o state seja:

      state = { products: [] }

temos

     return <h1>Contagem de produtos: {this.state.products.length}</h1>

Para preencher a variável products usamos o método setState(). Então:

    this.setState({ products: response.data.docs });

Agora o render vai imprimir automaticamente na page a mensagem:

    Contagem de produtos: 10

Isso é possível porque o render 'ouviu' a alteração no state e executou o return.

#### imprimir na tela uma lista com o título de cada produto buscado na api

render() {

return ...

    this.state.products.map(product => (
    <h2 key={product_id}>{product.title}</h2>
    ))}

### key

No React é necessário usar uma 'key' com um valor para cada informação. Aqui utilizamos uma key com um valor único para cada produto da api.
