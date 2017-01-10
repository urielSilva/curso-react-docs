### Instalação do NodeJS ###

O primeiro passo é realizar a instalação do NodeJS e no NPM, que já vem junto com o Node por padrão. Esse link irá auxiliar na instalação:

[Instalar NodeJS](https://nodejs.org/en/download/package-manager/)

### Instalação do create-react-app ###

Durante o curso iremos utilizar uma ferramenta chamada *create-react-app*, criada com o intuito de facilitar a configuração inicial de um projeto React e todas as dependências necessárias (React, Webpack,  Babel, etc). O *create-react-app* está disponível como um pacote do NPM, e para instalá-lo iremos utilizar o seguinte comando:

    npm install -g create-react-app

Para quem tiver mais curiosidade sobre como ele facilita nossa vida, segue o link para o repo no github:

[create-react-app repo](https://github.com/facebookincubator/create-react-app)

### Criando o Projeto ###

Agora que já temos o *create-react-app* instalado, podemos finalmente criar o nosso projeto React. Fazer isso é bem fácil, basta executar os seguintes comandos no terminal:

    create-react-app nome_do_projeto
    cd nome_do_projeto
    npm start


### Conteúdo do Projeto ###

Nessa seção vamos cobrir os principais arquivos e pastas criados dentro do projeto.


    src/
    node_modules/
    public/
    package.json
    .gitignore
    README.md
   
 Pasta *src*: Contém o código propriamente dito da nossa aplicação. Todos os nossos componentes e outros arquivos necessários entrarão aqui.

Pasta *node_modules*: Contém as dependências do projeto que foram instaladas via *npm*. Não tivemos que instalar nada nós mesmos, mas o *create-react-app* instala várias bibliotecas necessárias para a execução do projeto.

Pasta *public*:  Contém o arquivo *index.html*, onde os nossos componentes serão inseridos durante a execução da aplicação. Também contém um *favicon*.

*package.json*:  Arquivo que registra todas as dependências do projeto que são gerenciadas pelo *npm*. Quando o comando *npm install* é executado, o *npm* busca nesse arquivo as dependências que precisar baixar.

Uma vez entendida a estrutura do projeto, podemos examinar melhor o código do arquivo *src/App.js*, onde está localizado o primeiro componente que iremos utilizar.

O código do componente é o seguinte:   

	

    import React, { Component } from 'react';
    import logo from './logo.svg';
    import './App.css';
    
        class App extends Component {
          render() {
            return (
              <div className="App">
                <div className="App-header">
                  <img src={logo} className="App-logo" alt="logo" />
                  <h2>Welcome to React</h2>
                </div>
                <p className="App-intro">
                  To get started, edit <code>src/App.js</code> and save to reload.
                </p>
              </div>
            );
          }
        }
        
        export default App;
	

Alguns pontos importantes desse código:

As linhas de *import* devem parecer um pouco estranhas para quem está acostumado com Javascript. Esse recurso é uma adição do ES6 (ou ES2015), que permite o *import/export* de classes ou módulos de arquivos externos. No momento em que se exporta uma classe, existe a opção de exportá-la como *default*. A diferença disso é que na hora de importar essa classe, não é necessário colocar seu nome entre chaves, como exemplificado na primeira linha do arquivo. A classe *React* foi exportada como *default*, mas a classe *Component* não, portanto devemos importar *Component* com as chaves em volta. O arquivo informado como destino do *import* pode ser um arquivo da nossa própria aplicação, devendo ser informado com o caminho relativo (*import './App.css'*), ou um arquivo de uma dependência externa, podendo ser informado apenas o namespace daquela biblioteca(*import React, { Component } from 'react'*). Lembrando que as bibliotecas estão na pasta *node_modules* e quem se encarrega de fazer essa associação é o Webpack.

Continuando, temos a declaração da classe *App*. Classes também são um novo recurso do ES6, mas é importante ressaltar que o conceito de OO em Javascript não mudou, por baixo dos panos o JS ainda lida com *Prototypal Inheritance*. Esse recurso é apenas uma sintaxe mais amigável para lidar com objetos. Ao informar que a classe *App* herda de *Component*, estamos declarando que essa classe será um componente React. Esse detalhe é muito importante e obrigatório para a criação de componentes. 

Um outro ponto muito importante e também obrigatório em um componente é a existência do método *render()*. Esse método é responsável por retornar o código "HTML" que corresponde ao template daquele componente, ou seja, o código que irá ser exibido na tela quando esse componente for renderizado. Na realidade esse código não é exatamente HTML, mas sim JSX, uma extensão da sintaxe do Javascript que facilita o uso de Javascript junto com o que seria o HTML. Deixo aqui o link da documentação que fala sobre o JSX.


[Leia mais sobre JSX](https://facebook.github.io/react/docs/introducing-jsx.html) 




	