# ReactJS

## Requisistos básicos:
  
- Noções de:
  - [Javascript](https://github.com/rochamauricio/e6/blob/master/javascript/js.md)
  - [CSS](https://github.com/rochamauricio/e6/blob/master/css/css.md)
  - [HTML](https://github.com/rochamauricio/e6/blob/master/html/html.md)
- Intalar:
  - npm (Gerenciador de dependências do JavaScript)
  - node (vem com npx)
  - Obs.: para exemplos básicos não precisa instalar!

## Conceitos

- React é uma biblioteca JavaScript para criar interfaces de usuário.
- React não é um framework.
- React é baseada em componentes.
- Tudo em React são componentes.
- Foi criada em 2011 por Jordan Walke no Facebook.
- Em 2015 surge React Native (para aplicações mobile).

- No React utilizamos a palavra className (e não class) para atribuir um valor a uma propriedade class de uma tag HTML pois a palavra class é uma palavra reservada no Javascript.
- *One-way data flow*: O React trabalha com um fluxo único de direção de passagem de valor: só conseguimos propagar informações dos componentes de mais alto nível para os de mais baixo nível.

### JSX

- É uma linguagem de marcação criada para utilizar tags html junto com javascript.
- Não é HTML e nem string
- Otimiza a renderização do código.
- Precisa ser instalado pois não existe naturalmente no Javascript.
- Precisa instalar o babel (é para versao de desenvolvimento e nao para a producao)
- O babel transforma o codigo JSX em código react e facilita as coisas!

Exemplo de jsx:

~~~javascript
const element = <h1> Hello, Wordld! </h1>;
~~~

## Exemplos básicos

- Os exemplos básicos têm fins didáticos e não utilizam o NPM. 
- Para todos exemplos básicos:
  - Criar um diretório para o projeto e dentro dele um arquivo index.html
  - Obs.: para visualizar o resultado abra o arquivo index.html em um navegador web.

### Exemplo 1

- Exemplo que cria uma div com o texto "Olá Mundo".

Arquivo **index.html**:

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Exemplo - React JS</title>
</head>
<body>
  <div id="app"></div>

  <!-- Adiciona o react -->
  <script src="https://unpkg.com/react@17/umd/react.development.js" crossorigin></script>

  <!-- Adiciona o reactdom: para injetar componentes na página -->
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js" crossorigin></script>

  <script>
    // Cria um componente
    function MeuComponente() {
      return React.createElement('div', null, 'Olá mundo') // parametros: componente, propriedades, filho
    }

    // RactDOM é uma var global do React
    ReactDOM.render(
      React.createElement(MeuComponente),
      document.getElementById('app')
    )
  </script>
</body>
</html>
~~~

### Exemplo 2

- Exemplo que cria diversas divs encadeadas, inserindo classes e um id. Na div final há um parágrafo com o texto "Olá Mundo".

Arquivo **index.html**:

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Exemplo 1 - React JS</title>
</head>
<body>
  <div id="app"></div>
  <script src="https://unpkg.com/react@17/umd/react.development.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js" crossorigin></script>
  <script>
    function MeuComponente1() {
      return (
        React.createElement('div', { className: 'componente-1' },
          React.createElement(MeuComponente2)
        )
      )
    }

    function MeuComponente2() {
      return (
        React.createElement('div', { className: 'componente-2' },
          React.createElement(MeuComponente3)
        )
      )
    }

    function MeuComponente3() {
      return (
        React.createElement('div', { className: 'componente-3' },
          React.createElement(MeuComponente4)
        )
      )
    }

    function MeuComponente4() {
      return (
        React.createElement('div', { className: 'componente-4' },
          React.createElement('p', null, 'Olá Mundo!')
        )
      )
    }

    function MeuComponente() {
      return React.createElement('div', { id: 'componentes' },
        React.createElement(MeuComponente1));
    }

    ReactDOM.render(
      React.createElement(MeuComponente),
      document.getElementById('app')
    )
  </script>
</body>
</html>
~~~

### Exemplo 3

- Exemplo que passa propriedades de um componente pai (MeuComponente1) para o componente filho (MeuComponente2).

~~~html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Exemplo 1 - React JS</title>
</head>

<body>
  <div id="app"></div>
  <script src="https://unpkg.com/react@17/umd/react.development.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js" crossorigin></script>
  <script>
    function MeuComponente1() {
      const meuNome = "Mauricio";
      return (
        React.createElement('div', { className: 'componente-1' },
          React.createElement(MeuComponente2, { nome: meuNome, idade: 110 }) // passando propriedades para o componente 4
        )
      )
    }

    function MeuComponente2(props) { // recebe o objeto { nome: meuNome, idade: 29 } como parametro, usamos o nome props por convenção
      return (
        React.createElement('div', { className: 'componente-2' },
          React.createElement('p', null, "Bem vindo " + props.nome + ", sua idade é: " + props.idade + " anos!")
        )
      )
    }

    function MeuComponente() {
      return React.createElement('div', { id: 'componentes' },
        React.createElement(MeuComponente1));
    }

    ReactDOM.render(
      React.createElement(MeuComponente),
      document.getElementById('app')
    )
  </script>
</body>

</html>
~~~

### Exemplo 4

- Exemplo que usa context provider e consumer para passar informações de qualquer componente pai DIRETAMENTE para qualquer componente filho, neto, bisneto, ...

~~~html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Exemplo 1 - React JS</title>
</head>

<body>
  <div id="app"></div>
  <script src="https://unpkg.com/react@17/umd/react.development.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js" crossorigin></script>
  <script>

    // propagando informacao para qualquer componente filho, neto, bisneto
    const NomeContext = React.createContext('nome');

    function MeuComponente1() {
      const meuNome = "Mauricio Barbosa da Rocha";
      return (
        // propaga a informação
        React.createElement(NomeContext.Provider, { value: meuNome }, // chave precisa ser value
          React.createElement('div', { className: 'componente-1' },
            React.createElement(MeuComponente2)
          )
        )
      )
    }

    function MeuComponente2() {
      return (
        React.createElement('div', { className: 'componente-2' },
          React.createElement(MeuComponente3)
        )
      )
    }

    function MeuComponente3() {
      return (
        React.createElement('div', { className: 'componente-3' },
          React.createElement(MeuComponente4)
        )
      )
    }

    // recebendo a informacao
    function MeuComponente4() {
      return (
        React.createElement(NomeContext.Consumer, null,
          (NomeContext) => (
            React.createElement('div', { className: 'componente-4' },
              React.createElement('p', null, NomeContext)
            )
          )
        )
      )
    }

    function MeuComponente() {
      return React.createElement('div', { id: 'componentes' },
        React.createElement(MeuComponente1));
    }

    ReactDOM.render(
      React.createElement(MeuComponente),
      document.getElementById('app')
    )
  </script>
</body>

</html>
~~~

## Links

- [Tutorial youtube - Prog a bordo](https://www.youtube.com/watch?v=Ws9WVHhNq5M)

## Continua

- [React Tutorial - W3schools](https://www.w3schools.com/react/default.asp)
- Hooks
