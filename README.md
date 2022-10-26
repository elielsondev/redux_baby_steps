# Redux in React.js baby steps
O passo a passo para implementação do Redux em projeto React.js

Usaremos um exemplo simples para entendermos o Redux, porém o Redux é excelente para operações complexas:
![image](https://user-images.githubusercontent.com/83602931/195695806-21d4a05a-9140-4168-a80b-c94b211895da.png)


A imagem acima mostra o problema que queremos resolver com ajuda do Redux:
- A esquerda temos a tela de login do usuário que tem que digitar o `nome` e `email`.
- Após clicar no botão de login queremos que o `nome` e `email` sejam 'recuperados' e exibidos junto com a mensagem, como mostra a nossa imagem a direita.

***!!! É ai que o nosso Redux entra em cena. !!!***

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

**Criar dentro do diretório 📂 actions:**
- arquivo 📄 `index.js`

**Criar dentro do diretório 📂 reducers:**
- arquivo 📄 `index.js`

**Criar dentro do diretório 📂 store:**
- arquivo 📄 `index.js`

##### A partir daqui devemos reforçar um fato importante: Alguns arquivos precisaram ser importados antes mesmo de serem implementados, para uma melhor compreensão do que vem a seguir. "Imagine que o Redux é uma casa em construção, porém existe uma peculiaridade nela, ela será construida de forma reversa, ou seja, primeiro iremos fazer o telhado, depois as paredes, (...) e por fim a base". Seguindo essa linha de racíocinio podemos seguir adiante.

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


- Agora implementar nosso arquivo index.js, ainda no diretório reducers:
  - Importar o `combineReducers` do redux, com ele é possível 'consumir' um ou mais reducers:
  `import { combineReducers } from 'redux';`
  
  - Importar os reducers que nós criamos, nesse caso será apenas o `userReducer`, porém se existissem mais deveriamos importa-los também:
  `import userReducer from './userReducer';`
  
  - Criar a constante `rootReducer` que recebe o `combineReducer` com os reducers existentes e exportar:
  ```
  const rootReducer = combineReducers({
    userReducer,
  });

  export default rootReducer;
  ```
  
![Captura de tela de 2022-05-17 02-56-56](https://user-images.githubusercontent.com/83602931/168739372-1327d14d-0fc2-405c-ae90-a1b204165e99.png)

**Na pasta actions**:
- Criar as actionTypes necessárias: `export const DATA = 'DATA';`

![Captura de tela de 2022-05-17 03-03-28](https://user-images.githubusercontent.com/83602931/168740163-f693a066-8e41-434b-95b0-8e6dce0057af.png)

- Importar as `actionTypes` necessárias: `import { DATA } from './actionsTypes';`

- Criar os actions creators necessários:
```
export const actionData = (payload) => (
  {
    type: DATA,
    payload,
  }
);
```

![Captura de tela de 2022-05-17 03-10-47](https://user-images.githubusercontent.com/83602931/168741128-1ea301f0-b495-4a10-beeb-fe02b3ddcc80.png)


**Nos componentes**:
> Aguarde!!! Em breve concluirei os tópicos abaixo.
- fazer o connect: Devemos importar o connect `import { connect } from 'react-redux'` no componente que iremos usar o `mapStateToProps`, `mapDispatchToProps` ou ambos.
```
export default connect(mapStateToPros, mapDispatchToProps)(App)
```
 **OBS: Caso não use um dos dois no componente substitua-o no connect por `null`**

- criar a função mapDispatchToProps: Essa função é responsável por disparar as informações (dados) que você quer enviar para o reducer.
```
const mapDispatchToProps = (dispatch) => (
  {
    infoInput: (state) => dispatch(actionData(state)),    
  }
);
```
**OBS: Devemos importar a action que queremos persistir a informação.**

- criar a função mapStateToProps: Essa função resgata os dados salvos no reducer como props;
```
const mapStateToProps = (state) => (
  {
    infoSave: state.userReducer.user,
  }
);
```

![image](https://user-images.githubusercontent.com/83602931/195689268-b29c8498-80ad-4ae4-97ce-bf33e3d64c7e.png)

**Se a sua aplicação não terá outras páginas, não é necessário configurar as rotas. Caso contrário**:
 `npm install react-router-dom`
