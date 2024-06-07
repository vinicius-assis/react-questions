## Componentes e JSX

---

> O que é JSX e por que é usado no React?

- **JSX significa JavaScript XML. Ele é utilizado porque permite escrever tags HTML dentro do JavaScript, facilitando a criação e visualização da estrutura da interface de usuário diretamente no código JavaScript.**

> Qual a diferença entre componentes funcionais e de classe?

- **Componentes funcionais são definidos como funções e utilizam hooks para manipular estados e efeitos, como useState e useEffect. Componentes de classe são definidos através de classes e utilizam métodos de ciclo de vida, como componentDidMount e componentWillUnmount, para manipular estados e efeitos.**

> Como você pode passar dados para um componente filho?

- **Podemos passar dados para um componente filho utilizando props. Também podemos utilizar o Context API para compartilhar dados, estados e ações entre componentes.**

> O que são props e como elas são utilizadas?

- **Props são atributos recebidos pelo componente via parâmetros. Elas são utilizadas para passar dados e funções de um componente pai para um componente filho, permitindo que os componentes sejam reutilizáveis e dinâmicos.**

## Estado e Ciclo de Vida

---

> Qual é a diferença entre estado (state) e props?

- **State é um objeto gerenciado internamente pelo componente e pode ser alterado ao longo do tempo para refletir mudanças na interface do usuário. Props são dados passados de um componente pai para um componente filho e são imutáveis no contexto do componente filho.**

> Explique o ciclo de vida de um componente de classe.

- **O ciclo de vida de um componente de classe no React pode ser dividido em três fases principais:**

  - **_Montagem (Mounting): Ocorre quando o componente é criado e inserido no DOM. Métodos principais: constructor(), static getDerivedStateFromProps(), render(), componentDidMount()._**
  - **_Atualização (Updating): Ocorre quando as props ou o estado do componente mudam. Métodos principais: static getDerivedStateFromProps(), shouldComponentUpdate(), render(), getSnapshotBeforeUpdate(), componentDidUpdate()._**
  - **_Desmontagem (Unmounting): Ocorre quando o componente é removido do DOM. Método principal: componentWillUnmount()._**

> O que é o hook useState e como ele é usado?

- **O hook useState é uma função que permite adicionar estado a componentes funcionais no React. Ele retorna um array com dois elementos: o estado atual e uma função que permite atualizar esse estado.**

#### Exemplo de uso:

```jsx
import React, { useState } from "react";

function Contador() {
  const [contagem, setContagem] = useState(0);

  return (
    <div>
      <p>Você clicou {contagem} vezes</p>
      <button onClick={() => setContagem(contagem + 1)}>Clique aqui</button>
    </div>
  );
}
```

> Como você gerencia estado em componentes funcionais?

- **Em componentes funcionais, o estado é gerenciado principalmente através dos hooks do React, como useState e useReducer.**

#### Exemplo com useState:

```jsx
import React, { useState } from "react";

function ExemploUseState() {
  const [nome, setNome] = useState("João");

  return (
    <div>
      <p>Nome: {nome}</p>
      <button onClick={() => setNome("Maria")}>Mudar Nome</button>
    </div>
  );
}
```

#### Exemplo com useReducer:

```jsx
import React, { useReducer } from "react";

const initialState = { contagem: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "incrementar":
      return { contagem: state.contagem + 1 };
    case "decrementar":
      return { contagem: state.contagem - 1 };
    default:
      throw new Error();
  }
}

function Contador() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Contagem: {state.contagem}</p>
      <button onClick={() => dispatch({ type: "incrementar" })}>+</button>
      <button onClick={() => dispatch({ type: "decrementar" })}>-</button>
    </div>
  );
}
```

## Hooks

---

> O que são hooks no React?

- **Hooks são funções que permitem usar estado e outros recursos do React em componentes funcionais. Eles foram introduzidos no React 16.8 para facilitar a reutilização de lógica de estado e efeitos colaterais em componentes funcionais.**

> Explique o hook useEffect e forneça um exemplo de uso.

- **O hook useEffect permite executar efeitos colaterais em componentes funcionais. Ele pode ser usado para operações como buscar dados, assinar serviços, ou manipular o DOM.**

#### Exemplo de uso:

```jsx
import React, { useState, useEffect } from "react";

function ExemploUseEffect() {
  const [dados, setDados] = useState([]);

  useEffect(() => {
    fetch("https://api.example.com/dados")
      .then((response) => response.json())
      .then((data) => setDados(data));
  }, []);

  return (
    <div>
      <ul>
        {dados.map((item) => (
          <li key={item.id}>{item.name}</li>
        ))}
      </ul>
    </div>
  );
}
```

> Qual a diferença entre useMemo e useCallback?

- **useMemo memoiza o valor de uma expressão para evitar cálculos desnecessários em renderizações subsequentes. useCallback memoiza uma função para evitar que funções sejam recriadas em cada renderização, útil para evitar re-renderizações desnecessárias de componentes filhos.**

> Quando você usaria o hook useReducer?

- **useReducer é usado quando o estado é mais complexo e envolve múltiplas subvalores ou quando a lógica de atualização é complexa. É uma alternativa ao useState que é mais semelhante ao Redux.**

## Contexto e Gerenciamento de Estado

> O que é o Context API e quando você deve usá-lo?

- **O Context API permite compartilhar valores entre componentes sem a necessidade de passar props manualmente em cada nível da árvore de componentes. Deve ser usado quando múltiplos componentes precisam acessar os mesmos dados ou funções.**

> Explique como usar o useContext para compartilhar dados entre componentes.

- **useContext é um hook que permite acessar o valor de um contexto diretamente. Primeiro, você cria um contexto com React.createContext(), depois você fornece o valor desse contexto usando o componente <Context.Provider> e, finalmente, você acessa esse valor em qualquer componente usando useContext.**

#### Exemplo:

```jsx
import React, { createContext, useContext, useState } from "react";

const MeuContexto = createContext();

function Provedor({ children }) {
  const [valor, setValor] = useState("Olá Mundo");

  return <MeuContexto.Provider value={valor}>{children}</MeuContexto.Provider>;
}

function ComponenteFilho() {
  const valor = useContext(MeuContexto);

  return <div>{valor}</div>;
}

function App() {
  return (
    <Provedor>
      <ComponenteFilho />
    </Provedor>
  );
}
```

> Compare o uso do Context API com o Redux.

- **O Context API é útil para compartilhar dados entre componentes sem a necessidade de passar props manualmente, mas é mais limitado em comparação com o Redux, que é uma biblioteca de gerenciamento de estado mais robusta. O Redux oferece um fluxo de dados unidirecional, ferramentas de depuração avançadas, middleware, e é adequado para aplicações com estados complexos e ações assíncronas.**

> Quais são os principais conceitos do Redux?

- **Store: O objeto que armazena todo o estado da aplicação.**
- **Actions: Objetos que descrevem o que aconteceu na aplicação.**
- **Reducers: Funções que determinam como o estado muda em resposta às actions.**
- **Dispatch: A função usada para enviar actions ao store.**
- **Selectors: Funções que selecionam e retornam uma parte específica do estado.**

## Roteamento

---

> O que é React Router?

- **React Router é uma biblioteca para gerenciar a navegação e os roteamentos em uma aplicação React. Ela permite definir rotas e associar componentes a essas rotas.**

> Como você pode criar rotas dinâmicas no React Router?

- **Você pode criar rotas dinâmicas usando parâmetros de rota. Os parâmetros de rota são definidos com dois pontos : antes do nome do parâmetro na definição da rota.**

#### Exemplo:

```jsx
import { BrowserRouter as Router, Route, Switch } from "react-router-dom";

function App() {
  return (
    <Router>
      <Switch>
        <Route path="/usuario/:id" component={Usuario} />
      </Switch>
    </Router>
  );
}
```

> Explique a diferença entre BrowserRouter e HashRouter.

- **BrowserRouter usa a API de histórico do HTML5 para manipular as URLs de forma limpa e amigável, sem o # na URL. HashRouter usa o hash fragmento na URL (a parte após #) e é mais compatível com navegadores mais antigos.**

> Como você pode proteger rotas em uma aplicação React?

- **Você pode proteger rotas usando componentes de ordem superior (HOC) ou hooks para verificar a autenticação antes de renderizar o componente de destino. Um exemplo comum é criar um componente PrivateRoute que verifica a autenticação e, se o usuário não estiver autenticado, redireciona para a página de login.**

#### Exemplo:

```jsx
import { Route, Redirect } from "react-router-dom";

function PrivateRoute({ component: Component, ...rest }) {
  const isAuthenticated = {}; // lógica de autenticação

  return (
    <Route
      {...rest}
      render={(props) =>
        isAuthenticated ? <Component {...props} /> : <Redirect to="/login" />
      }
    />
  );
}
```

## Desempenho

---

> Quais são algumas técnicas para otimizar o desempenho de uma aplicação React?

- **Usar React.memo para evitar re-renderizações desnecessárias.**
- **Usar hooks como useMemo e useCallback para memorização.**
- **Dividir o código em partes menores usando o lazy loading com React.lazy e Suspense.**
- **Evitar mutações diretas do estado.**
- **Utilizar a virtualização de listas para renderizar apenas os itens visíveis com bibliotecas como react-window.**

> O que é memoização e como ela pode ser implementada no React?

- **Memoização é uma técnica de otimização que armazena o resultado de funções caras para evitar cálculos repetidos. No React, pode ser implementada usando o hook useMemo para valores e useCallback para funções.**

#### Exemplo com useMemo:

```jsx
import React, { useMemo } from "react";

function Componente({ valor }) {
  const valorMemoizado = useMemo(() => {
    return valor * 2;
  }, [valor]);

  return <div>{valorMemoizado}</div>;
}
```

> Como você pode evitar re-renderizações desnecessárias?

- **Usar React.memo para componentes que não precisam re-renderizar frequentemente.**
- **Usar useMemo e useCallback para memorização de valores e funções.**
- **Garantir que as props e estados passados para componentes não mudem desnecessariamente.**
- **Utilizar a virtualização de listas para renderizar apenas os itens visíveis.**

> O que é o Virtual DOM e como ele melhora o desempenho do React?

- **O Virtual DOM é uma representação leve da árvore do DOM na memória. Quando o estado de um componente muda, o React cria um novo Virtual DOM e o compara com o Virtual DOM anterior. Apenas as mudanças reais são aplicadas ao DOM real, minimizando operações de manipulação de DOM e melhorando o desempenho.**

## Teste

---

> Quais são as ferramentas mais comuns para testar aplicações React?

- **Jest: Um framework de testes JavaScript com funcionalidades integradas.**
- **React Testing Library: Uma biblioteca que facilita o teste de componentes React de maneira que reflita como eles são usados por usuários reais.**
- **Enzyme: Uma biblioteca para testar componentes React (menos recomendada atualmente em favor do React Testing Library).**
- **Cypress: Uma ferramenta de teste de ponta a ponta para aplicações web.**

> Como você escreveria um teste para um componente React?

#### Exemplo com React Testing Library:

```jsx
import { render, screen } from "@testing-library/react";
import "@testing-library/jest-dom/extend-expect";
import MeuComponente from "./MeuComponente";

test("renderiza MeuComponente com o texto correto", () => {
  render(<MeuComponente />);
  const elemento = screen.getByText(/Olá Mundo/i);
  expect(elemento).toBeInTheDocument();
});
```

> Explique a diferença entre testes unitários e testes de integração.

- **Testes Unitários: Testam partes isoladas do código, como funções ou componentes individuais, para garantir que funcionam conforme esperado.**
- **Testes de Integração: Testam como diferentes partes do sistema funcionam juntas, verificando a interação entre componentes e módulos.**

> O que é o React Testing Library e como ele difere do Enzyme?

- **React Testing Library é uma biblioteca que facilita o teste de componentes React focando em testes que refletem o uso real dos componentes pelos usuários. Ele encoraja boas práticas de teste, como evitar teste de implementações internas. Enzyme, por outro lado, permite o acesso a detalhes internos dos componentes, o que pode levar a testes menos robustos e mais acoplados à implementação.**

## Estilização

---

> Quais são as diferentes maneiras de estilizar componentes no React?

- **CSS tradicional: Usar arquivos CSS separados.**
- **CSS Modules: Usar arquivos CSS que são escopados localmente por padrão.**
- **CSS-in-JS: Usar bibliotecas como styled-components ou Emotion para escrever estilos diretamente dentro do JavaScript.**
- **Frameworks de CSS: Usar frameworks como Bootstrap ou Tailwind CSS.**

> Como você pode usar CSS Modules em uma aplicação React?

#### Exemplo:

```jsx

// MeuComponente.module.css
.botao {
background-color: blue;
color: white;
}

// MeuComponente.jsx
import React from 'react';
import styles from './MeuComponente.module.css';

function MeuComponente() {
  return <button className={styles.botao}>Clique aqui</button>;
}

export default MeuComponente;
```

> O que é CSS-in-JS e quais são suas vantagens?

- **CSS-in-JS é uma técnica onde os estilos são definidos diretamente no JavaScript. Vantagens incluem:**

  - **_Escopo local por padrão, evitando conflitos de nomes._**
  - **_Capacidade de usar lógica JavaScript para estilos dinâmicos._**
  - **_Fácil remoção de estilos não utilizados, melhorando o desempenho._**

> Como você pode integrar frameworks de CSS, como Bootstrap, com React?

- **Você pode integrar frameworks de CSS como Bootstrap importando os arquivos CSS diretamente no seu projeto React.**

#### Exemplo:

```jsx
// No arquivo de entrada, como index.js ou App.js
import "bootstrap/dist/css/bootstrap.min.css";

function App() {
  return (
    <div className="container">
      <button className="btn btn-primary">Clique aqui</button>
    </div>
  );
}

export default App;
```

## Acessibilidade

---

> Quais são algumas práticas recomendadas para garantir a acessibilidade em uma aplicação React?

- **Usar semântica HTML adequada (tags como `<header>`, `<main>`, `<footer>`, etc.).**
- **Garantir que todos os elementos interativos (botões, links) sejam acessíveis via teclado.**
- **Usar atributos ARIA para melhorar a acessibilidade quando necessário.**
- **Testar a aplicação com ferramentas de acessibilidade como screen readers.**

> Como você pode usar o React para melhorar a acessibilidade de formulários?

- **Usar labels para todos os campos de formulário.**
- **Garantir que os elementos de formulário tenham atributos id e for correspondentes.**
- **Usar atributos ARIA para fornecer informações adicionais aos usuários de tecnologias assistivas.**

> O que são ARIA roles e como eles são utilizados no React?

- **ARIA roles são atributos que definem funções específicas para elementos da interface de usuário, melhorando a acessibilidade. Eles são usados para informar a tecnologia assistiva sobre o propósito de um elemento.**

#### Exemplo:

```jsx
<div role="alert">Mensagem de alerta</div>
```

> Como você pode testar a acessibilidade de uma aplicação React?

- **Usar ferramentas de análise de acessibilidade, como a extensão Lighthouse do Google Chrome.**
- **Testar com screen readers, como NVDA ou JAWS.**
- **Usar bibliotecas de testes de acessibilidade automatizados, como jest-axe.**

## Boas Práticas

> Quais são as melhores práticas para organizar o código de uma aplicação React?

- **Estruturar o projeto de forma clara e consistente, por exemplo, agrupando componentes por funcionalidade.**
- **Usar nomes de arquivos e pastas descritivos.**
- **Manter os componentes pequenos e focados em uma única responsabilidade.**
- **Separar a lógica de negócio da lógica de apresentação.**

> Como você pode dividir uma aplicação React em componentes reutilizáveis?

- **Identificar partes da UI que se repetem ou que podem ser independentes.**
- **Criar componentes para essas partes, passando dados e ações como props.**
- **Garantir que os componentes sejam genéricos e configuráveis através de props.**

> O que são Higher-Order Components (HOCs) e quando você deve usá-los?

- **Higher-Order Components (HOCs) são funções que recebem um componente e retornam um novo componente com funcionalidades adicionais. Eles são usados para reutilizar lógica entre componentes.**

#### Exemplo:

```jsx
function withLoading(Component) {
  return function WithLoadingComponent({ isLoading, ...props }) {
    if (!isLoading) return <Component {...props} />;
    return <p>Loading...</p>;
  };
}
```

> Como você pode lidar com erros em uma aplicação React?

- **Usar componentes de erro para capturar e exibir erros.**
- **Implementar o método componentDidCatch em componentes de classe ou usar o hook useErrorBoundary em componentes funcionais.**
- **Usar bibliotecas de monitoramento de erros, como Sentry, para capturar e relatar erros em produção.**

#### Exemplo:

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // Envie o erro para um serviço de log
  }

  render() {
    if (this.state.hasError) {
      return <h1>Algo deu errado.</h1>;
    }

    return this.props.children;
  }
}
```
