Na segunda aula, desenvolvemos um componente simples que era responsável por listar os cursos disponíveis na tela. Para isso, foi necessário aprender um pouco do State e de outros aspectos de um componente React. A seguir, vou fazer um resumo do que foi explicado na aula.

### Primeiros passos ###

A primeira coisa que precisamos fazer é criar um novo arquivo, que chamaremos de *CourseList.js*. Entretanto, para fins de organização, sugere-se que esse arquivo fique dentro de uma pasta *components* que irá guardar os arquivos referentes aos nossos componentes. Dessa forma a estrutura do nosso projeto está assim:

	

node_modules/
public/
src/components/CourseList.js
App.js
index.js
...
		
Uma vez criado o arquivo, devemos criar uma nova classe com o nome de *CourseList*, e como essa classe será um componente React, devemos herdar da classe *Component*, como explicado na aula anterior. Não podemos esquecer de importar a classe *React* e *Component* do pacote '*react*'. Uma versão inicial do componente ficou assim:

    import React, { Component } from 'react';
    class CourseList extends Component {
    
      render() {
        return (
            <div>
            </div>
        );
      }
    }
    export default CourseList;


### Armazenando valores com State ###

Nosso componente irá mostrar informações para o usuário, mais especificamente os cursos disponíveis na plataforma. Uma primeira pergunta é: Como iremos buscar os dados que precisamos da nossa API? 

Como dito anteriormente, o React se propõe a resolver apenas um problema específico do desenvolvimento front end, portanto a parte de chamada à API não faz parte do core do React. Podemos utilizar o que quisermos para realizar essa ação, e por motivos de familiaridade iremos usar o bom e velho *jQuery*.

Para usar o *jQuery* em nosso projeto, basta instalá-lo usando o *npm* e importá-lo dentro do arquivo em que for necessário. Para instalar, precisamos executar o seguinte comando no terminal(lembrete: executar no diretório raiz do projeto):

    npm install jquery --save

E para fazer o import, colocamos a seguinte linha no nosso arquivo:


	

    import $ from 'jquery';


Agora que possuímos o *jQuery*, podemos fazer a chamada à nossa API e buscar os nossos cursos. Uma segunda pergunta que surge é: Onde iremos armazenar os dados que retornarão da nossa chamada Ajax? 

Para resolver o problema de armazenar dados em um componente, existe o conceito de *State* dentro do *React*. O *State* nada mais é do que um Objeto Javascript (JSON) feito para guardar os dados (estado) relevantes para nosso componente. Para podermos utilizá-lo, precisamos inicializá-lo dentro do método construtor do nosso componente.

    constructor() {
        super();
        this.state = {courses: []};
      }

Acessamos o *State* com um *this.state* e atribuímos à propriedade *courses* um array vazio, já que eventualmente iremos armazenar o array de cursos nesse campo. Um detalhe importante é que tirando nesse momento de inicialização, iremos alterar o valor do *state* por meio do método *setState()*. Isso é extremamente importante, pois o método *setState()* causa a re-renderização do nosso componente, o que torna o nosso componente algo "reativo", refletindo na tela as mudanças causadas em seu estado.

Agora que já inicializamos o *state*, iremos realizar a nossa chamada à API para popular os dados. Iremos colocar essa chamada dentro de um método do ciclo de vida de um componente React, chamado *componentWillMount()*. Esse método é chamado antes do componente ser renderizado, e é o momento ideal para consultarmos uma fonte de dados externa.


[Mais sobre State e Ciclo de Vida](https://facebook.github.io/react/docs/state-and-lifecycle.html)

Nossa chamada ficará assim:

	

    componentWillMount() {
        $.ajax({
          url: 'https://api- goodle.herokuapp.com/courses.json',
          dataType: 'json',
          success: (data) => {
            this.setState({courses: data});
          }
        })
      }



Agora que já temos nossos cursos no devido lugar, podemos acessá-los e retornar o template com a listagem completa.

### Processando arrays com Map ###

Agora que já temos nossos cursos, iremos voltar nossa atenção para o método *render*, e criaremos o template que irá ser retornado pelo componente. Iremos criar um template simples que mostra o nome a descrição de cada curso. Para isso, iremos utilizar a função *map*, que itera por um array e retorna um novo array após aplicar uma função qualquer em cada elemento, sendo essa função definida por nós. O *map* é um recurso que vem da programação funcional, e várias linguagens, incluindo o Javascript, possuem esse recurso que facilita bastante o processamento de listas e arrays.

O código ficará assim:


    render() {
        return (
            <div>
              <h1>Cursos Disponíveis</h1>
              {this.state.courses.map((course) => {
                return (
                  <div key={course.id}
                   <h2>{course.name}</h2>
				   <p>{course.description}</p>
                  </div>
                );
              })}
            </div>
        );
      }


Como dito, aplicamos a função *map* ao nosso array de cursos, disponível em *this.state.courses*, e dentro da função que o *map* aplica aos elementos, criamos um trecho de JSX que contém as informações de um único curso, e ao final da execução cada trecho referente a um curso será inserido no template final do componente.

Para quem estiver se perguntando o que é aquele atributo *key={course.id}*, essa dúvida fica como dever de casa pra vocês. Esse link ajuda a responder:

[Mais sobre listas e keys](https://facebook.github.io/react/docs/lists-and-keys.html)

Agora que temos nosso componente pronto, precisamos adicioná-lo no componente *App* para que algo seja mostrado na tela. Para isso, basta adicionar:

    import CourseList from './components/CourseList';


E adicionar a tag do componente dentro do *render* do componente *App*:
	

    render() {
        return (
          <div className="App">
            <CourseList />
          </div>
        );
      }

Com isso fechamos a aula 2, até mais.
PS: Parem de não aparecer na aula porque dá muito trabalho escrever isso tudo.