# Redux baby steps
O passo a passo para implementação do Redux em um projeto React.js

### Checklist do react-redux

**Antes de começarmos devemos ter bem definido o que queremos**:
- Como será o *formato* do seu estado global, ou seja, quais dados queremos salvar?
      `
      Pra ficar mais claro iremos começar nossa aplicação, tendo o caso a seguir como exemplo prático:
      Queremos registrar no estado global os dados de login, devemos registrar o 'name' e 'email' do 
      nosso 'user', tendo isso em mente podemos dar sequência.
      `
      <br />
      <br />
- pensar quais actions serão necessárias na sua aplicação: 
      `
       Com o contexto já bem definido no passo anterior, poderiamos criar uma action para o 'name' e outra 
       action para 'email', porém NÃO iremos fazer assim, vamos criar uma action apenas para 'user' que deve
       possuir os dados de 'name' e de 'email'.
      `

**Instalação**:
  <br />
  
`Criando uma aplicação React.js caso não tenha iniciado ainda:`
```
npx create-react-app NOME-DO-SEU-APP
```
  <br />
  <br />
  
`Instalação do Redux no React.js:`
```
npm install --save redux react-redux
```
  <br />
  <br />
  
`DevTools do Redux:`
```
npm install --save redux-devtools-extension
```
  <br />
  <br />
  
`ATENÇÃO!!! - Caso o projeto tenha chamada de API faça a instalação do Redux Thunk com o comando abaixo.`
```
npm install redux-thunk 
```
  <br />
  <br />
  
`Eu geralmente uso o npm install no final do comando pra dar um refresh, porém não é necessário:`
```
npm install
```

**Criar dentro do diretório 🗃 src**:
- Diretório/pasta 📂`redux` e dentro dessa pasta:
   -  Crie os diretórios 📂`actions`, 📂`reducers` e 📂`store`.

*Criar dentro do diretório 📂 actions:*
- arquivo 📄 `index.js`

**Criar dentro do diretório 📂 reducers:*
- arquivo 📄 `index.js`

**Criar dentro do diretório 📂 store:*
- arquivo 📄 `index.js`

#### A partir daqui devemos reforçar um fato importante: Alguns arquivos precisaram ser importados antes mesmo de serem implementados, para uma melhor compreensão do que vem a seguir. "Imagine que o Redux é uma casa em construção, porém existe uma peculiaridade nela, ela será construida de forma reversa, ou seja, primeiro iremos fazer o telhado, depois as paredes, (...) e por fim a base". Seguindo essa linha de racíocinio podemos seguir adiante.

**No arquivo App.js:**
*Essa implementação pode ser feita tanto no componente `<App />`, como no arquivo `src/index.js`, aqui iremos fazer no `index.js`,
mas se sinta livre pra escolher onde quer fazer.*
- Importe o Provider do react-redux: `import { Provider } from 'react-redux';`
- Importe o arquivo da pasta store: `import store from './redux/store/index.js';`
- Definir o Provider, `<Provider store={ store }>`, de maneira que ele englobe todo o componente, para fornecer os estados à todos os componentes encapsulados em `<App />`.

![Captura de tela de 2022-05-17 01-21-33](https://user-images.githubusercontent.com/83602931/168728504-d2e713e4-8a8f-4bff-877d-288823b4d921.png)

**No arquivo store/index.js:**
- Importar o `createStore`, como o próprio nome sugere, é uma função nativa que cria a `store`: 
    - `import { createStore } from 'redux';`
- Importar o `composeWithDevTools`, ele é fundamental para conseguir visualizar a extensão DevTools no Browser: 
    - `import { composeWithDevTools } from 'redux-devtools-extension';`
- Importar o `rootReducer` do arquivo index.js do diretório reducers:
    - import rootReducer from '../reducers/index.js';
- Configurar o [Redux DevTools](https://github.com/reduxjs/redux-devtools)

![Captura de tela de 2022-05-17 02-18-04](https://user-images.githubusercontent.com/83602931/168734725-66a5b69a-78f1-4219-a61e-385a6f557fa6.png)

**Na pasta reducers**:
- Criar os reducers necessários, no nosso caso iremos criar apenas um, caso não esteja lembrado definimos lá no início que iriamos salvar os dados do `user` onde ele nos disponibilizará o `name`  `email`, pois bem, vamos ao código:

- Importar um type do arquivo `actionTypes.js` do diretório action: 
   `import { DATA } from '../actions/actionsTypes';`

- Criar uma constante com as caracteristicas da estrutura que se deseja reseber e armazenar, daremos o nome de INITIAL_STATE, de fato será o estado inicial que irá receber os dados futuramente. 
```
const INITIAL_STATE = {
  user: {
    name: '',
    email: '',
  },
};
```
- Criar a função que atualiza o state e exporta-la, não irei me aprofundar em cada detalhe da função pra não ficar muito extenso, porém qualquer dúvida é só da uma "pesquisada básica" na internet.
```
function userReducer(state = INITIAL_STATE, action) {
  switch (action.type) {
    case DATA:
      return {
        ...state,
        user: action.payload,
      }    
    default:
      return state;
   }
}

export default userReducer;
```

![Captura de tela de 2022-05-17 02-41-55](https://user-images.githubusercontent.com/83602931/168737523-c87c2f15-8598-4d90-b805-11420f5af9d9.png)



- [ ] configurar os exports do arquivo index.js

**Na pasta actions**:
- [ ] criar os actionTypes, por exemplo: `export const DATA = 'DATA';`
- [ ] criar os actions creators necessários

**Nos componentes**:
- [ ] criar a função mapStateToProps
- [ ] criar a função mapDispatchToProps
- [ ] fazer o connect

**Se a sua aplicação não terá outras páginas, não é necessário configurar as rotas. Caso contrário**:
- [ ] npm install react-router-dom
