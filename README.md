# Huntweb - Projeto Starter da Rocketseat

Este Readme consiste em um passo a passo das aulas do curso Starter ReactJs da Rocketseat. Cada commit é referente a uma aula.

## ReactJs

    É biblioteca que nãoi faz mais que o Javascript puro. Porém, o faz de forma mais organizada. Serve para manipular a DOM. É muito utilizado para construção de SPA.

    Com o uso do React o back end não vai retornar os dados já formatados. Vai retorná-los em formato de JSON. Estrutura de dados que seja legível para ser utilizada em formnato de API Rest. então o back end da aplicação vai estar totalmente separado do front end. O front end vai consumir os dados do back end para conseguir montar a interface e mostrar as informações para o usuário.

    Isso traz muita flexibilidade para trabalharmos com a parte interativa da aplicação, como por exemplo permitir que o usuário carregue algo na tela. Além de deixar o front end bastante organizado, pois utiliza a componentização.

    #### sintaxe

    Conforme é mostrado na documentação oficial do React, quase todos os componentes vão ser em formato de classe. A classe vai extender o Component que tem na classe React.

    Tem o método obrigatório render() que renderiza um arquivo JSX.

    O JSX tem a sintaxe parecida com o HTML mas permite mostrar variáveis e incluir código Javascript dentro do HTML.

    A função ReactDom.render() vai renderizar o componente

## Criando Projeto

Instalar NodeJs e yarn (usar yarn em vez de mpn).

Instalar o pacote create-react-app com yarn

    $ yarn global add create-react-app

O create-react-app já vem com a parte de transpilação configurada. Então não precisa configurar Webpack e Babel.

Criar o projeto:

\$ create-react-app nomedoProjeto

Para rodar o servidor:

    $ yarn start

    O create-react-app já vem com a parte de transpilação configurada. Então não precisa configurar Webpack e Babel.

    Criar o projeto:

    $ create-react-app nomedoProjeto

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

#### Axios

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

# Página anterior/próxima

Criar funcionalidades de passar e voltar páginas

Criar buttons em src/pages/main/index.js

os buttons devem ter a disabled property;

Para chamar método sempre que o usário clicar em algum button, em javascript puro seria onclick.

No React deve ser onClik (camel case)

então os buttons ficariam com o seguinte código:

     <button disabled={page === 1}onClick={this.prevPage}>Anterior</button>

     <button disabled={page === productInfo.pages}onClick={this.nextPage}>Próxima</button>

this.nextPage e this.prevPage são os métodos a serem chamados ao clique

É preciso usar as informações de paginação da api. Então devemos armazená-los no state.
Para isso, criamos a propriedade productInfo no state.

Em loadProducts criar const { docs, ... productInfo} usando 'rest operator'. Aqui, a variável docs tem os produtos e a variável productInfo tem o resto das informações.

Agora tem que passar estas variáveis para o this.setState()

Voltabdo às funções:

nextPage() -> buscar a página atual e o productInfo;

    const {page, productInfo} = this.state;

verificar em qual página está

    if(page === productInfo.pages)

Se já esiver na última página -> return (não faz nada);

Se não estiver na última página

    const pageNumber = page + 1;

    this.loadProducts(pageNumber)

prevPage() ->

    const pageNumber = page -1;

Então

    loadProducts = async (page = 1) => {
      const response = await api.get(`/products?page=${page}`);
      const { docs, ...productInfo } = response.data;
      this.setState({ products: docs, productInfo, page });
    };

# Configurando navegação

Biblioteca para navegação

    $ yarn add react-router-dom

Criar src/routes.js

Importar componentes do react-router-dom

    import { BrowserRouter, Switch, Route } from 'react-router-dom';

- BrowserRouter: define que utilizamos as rotas através de um browser
- Switch: permite que apenas uma rota seja chamada por vez. Então um componente só vai ser exibido quando uma rota for acessada. Aqui, apenas uma página vai ser exibida por rota.
- Route: rotas.

  import Main from './pages/main';

Criar componente (forma de função)

const Routes = () => ( código )

A primeira rota vai ser acessada em localhost:3000

    <Route path="/" component={Main} />

O componente Main vai ser mostrado

importar rotas em App.js

em const App = () => (
mostrar <Routes/> em vez de <Main/>

Agora o roteamento já está configrado

Criar src/pages/product/index.js

Em index.js criar classe Product

Criar nova rota em routes.js

    <Route path="/products/:id" component={Product} />

Mas aqui o React considera que o produto começa com "/" então, mesmo que fizer localhost:3000/products/:id, ele vai parar na 1ª rota (path="/")
Então é preciso adicionar a propriedade exact:

    < Route exact path="/" component= {Main} />

Agora é preciso redirecionar o usuário para a segunda rota

Em src/main/index.js

    import { Link } from 'react-router-dom';

Link é um componente do 'react-router-dom'.

Substituir a tag <a> do render() className="product-list" por Link e o href por 'to';

    <Link to={`/products/${product.id}`}>Acessar</Link>

    # Navegando pro Detalhe

Buscar os dados dos produtos na API e exibi-los em tela, dentro da src/pages/produtc/index.js

- Buscando os dados do produto:
  criar variável product no state;
  preencher o

  product{} -> método componentDidMount()

        api.get('product/${id}')

- Preencher os dados do produto

  this.setState({ product: response.data});

- Mostrar os dados no render

  const { product } = this.state;

  return

  product.title, product.description,

  e

      URL: <a href={product.URL}>{product.URL}</a>

- Estilizar

## Princípios básicos do React neste curso

- Componentização;

- Roteamento com react-router;

- Ciclos de vida 'componentDidMount()';

- Utilização de API;

- Utilização do state;

- Utilização de propriedades.
