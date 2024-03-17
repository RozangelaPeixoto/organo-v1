# Organo - Descrição do Projeto
O Organo foi um projeto do curso "React: desenvolvendo com JavaScript" da Alura que visa criar um ambiente para organizar as pessoas de acordo com as escolas de tecnologia em que elas trabalham, [aqui está o layout do projeto](https://github.com/RozangelaPeixoto/organo/assets/140510936/70f26290-dc2b-4808-8d9d-8bf53de0e108). Esse foi meu primeiro projeto em React e fiz uma documentação bem completa sobre o que fiz e as coisas que aprendi durante o curso.

## 💻Documentando o conhecimento

**O QUE É E ONDE SURGIU O REACT**
O React surgiu em 2011 e foi criado por engenheiros de software do Facebook. A primeira implementação do React foi na timeline do próprio Facebook no mesmo ano.

Em resumo o React é uma biblioteca reativa, baseada em componentes para criar interfaces de usuário. A maior vantagem do react, e o motivo pelo qual ele foi criado, é que ele reage aos eventos e mudanças de estado, interagindo com outros componentes e atualizando o que for necessário, tudo isso em uma única página.

**CRIAÇÃO E ORGANIZAÇÃO DO PROJETO**
1) Antes de começar precisamos instalar o node.js, ele que vai criar nosso ambiente de execução e gerenciar nossos pacotes, através dos comandos npm (locais) e npx (remotos)
2) Para criar o projeto base usamos o comando `npm create react app`
3) Com o projeto criado podemos iniciar o servidor `npm start`
4) O projeto base já vem com um código padrão que não é necessário para o nosso projeto, então nesse passo precisamos apagar ou limpar todos os arquivos que não vamos utilizar, em sua grande maioria css e imagens

---
Antes de seguir adiante precisamos entender a integração entre 3 arquivos importantes, são eles: 
=> index.html (public)
Esse é o arquivo mostrado ao usuário, nele está a estrutura padrão do html, o que precisamos alterar nesse arquivo é apenas algumas informações no head para quando formos fazer o deploy do projeto, já o body não precisa ser alterado, nele existe apenas uma div vazia com uma id `<div id="root"></div>` e vamos entender o porque disse no próximo arquivo.

=> index.js (src)
Existem alguns imports nesse arquivo, mas o que deve ser abstraído aqui é que o elemento com o id root está sendo usado para criar a base do projeto e dentro dessa base ele está renderizando o nosso componente principal que é o App.js
```
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```
* React.StrictMode é um recurso para ser usado no desenvolvimento, ele tem muitas vantagens uma das melhores são as mensagens de erro amigáveis.

=> App.js (src)
Esse é o componente principal da aplicação, onde vamos escrever a lógica do nosso projeto.
---

**CRIANDO O COMPONENTE BANNER**
Chegou o momento de criar nosso primeiro componente, mas antes vamos aprender um pouco de boas práticas na organização das pastas.

---
* A pasta `public` é onde nossos arquivos externos ficam, arquivos ou recursos que podem ser acessados por uma url e que serão visíveis pelo usuário. Então dentro dessa pasta vamos criar nossa pasta `imagens`.

* Já na pasta `src` é onde ficam os arquivos que compoem nossa aplicação e que não são acessíveis pelo usuário. Nela vamos adicionar nossos componentes e páginas. Sendo assim podemos criar a pasta `components` e `pages` para organizar nossa árvore.

* A organização do componente pode ser feitas de algumas formas, nesse projeto vamos criar uma pasta para o componente `Componente` e dentro dela vamos criar dois arquivos, um index.js e um Componenete.css
---

Voltando a criação do componente...

1) Vamos criar um pasta `Banner` dentro da pasta `components` e dentro dela vamos criar os arquivos: index.js e Banner.css
2) Dentro do arquivo index.js vamos escrever o código base para a criação de um componente
  * Lembrando que o return só retorna uma única tag, independente do que tem dentro dessa tag
```
function Banner() {
  return(
    <header>...</header>
  )
}
export default Banner
```

2) Adicionar a tag Banner ao App.js e importar o componente
```
import Banner from '/.components/Banner';
function App() {
    return (
        <div>
            <Banner />
        </div>
    )
}
export default App;
```
3) Agora vamos importar o css no Banner.js
  * Como class é um nome reservado no Javascript o atributo que vamos utilizar para estilizar será o className
```
import './Banner.css'
function Banner() {
  return(
    <header className="cabecalho"></header>
  )
}
export default Banner
```

**COMPONENTE CAMPOTEXTO E AS PROPS**
1) A organização desse componente é igual ao anterior, uma pasta `CampoTexto` e dois arquivos `index.js` e `CampoTexto.css` 

2) Dessa vez vamos usar const e arrow function para criar o componente
```
import './CampoTexto.css'
const CampoTexto = () => {
  return(...)
}
export default CampoTexto
```
3) E então adicionar a tag CampoTexto ao App.js e importar o componente

> Props é uma forma reduzida de dizer propriedades. Elas são usadas para passar dados entre componentes.
Inicialmente vamos usar as props para personalizar os componentes, depois vamos ver outros usos.
4) Primeiro, recebemos as props como parâmetro da função
5) Depois podemos substituir os locais estáticos pelos valores que vamos receber nas props
```
const CampoTexto = (props) => {
  return(
    <div className="campo-texto">
      <label>{props.label}</label>
      <input placeholder={props.placeholder}/>
    </div>
  )
}
```
6) Voltando ao App.js onde chamamos nossa tag de CampoTexto vamos criar essas props
`<CampoTexto label="Nome" placeholder="Digite seu nome"/>`

**COMPONENTE FORMULARIO**
Vamos criar mais um componente, ele será intitulado Formulario e o objetivo dele é receber os componentes que irão compor nosso formulário, no caso só temos o CampoTexto, mas precisamos chamar esse componente três vezes.

A criação desse componente segue o padrão que já foi mostrado.

Com o componente criado vamos remover o CampoTexto do App.js e adicionar no Formulario, dessa forma:
* Nunca esqueça de importar o componente
```
<section className='formulario'>
  <form>
    <h2>Preencha os dados para criar o colaborador</h2>
      <CampoTexto label="Nome" placeholder="Digite seu nome"/>
      <CampoTexto label="Cargo" placeholder="Digite seu cargo"/>
      <CampoTexto label="Imagem" placeholder="Digite a url da imagem"/>
  </form>
</section>
```

**COMPONENTE LISTASUSPENSA E O MÉTODO MAP**
1) Vamos criar mais um componente, esse terá o nome de ListaSuspensa.
2) ListaSuspensa é um select que lista os times, para isso vamos usar o método map, que recebe um array para ser alterado e então exibido.
```
<div className='lista-suspensa'>
  <label>Time</label>
  <select>
    {props.times.map(time => <option key={time}>{time}</option>)}
  </select>
</div>
```
* O método map é muito útil no React, pois todo elemento iterável pode ser retornado pelo map já integrado ao html.
* A chave única (key) é importante para o react ter controle sobre as renderização daquele item.

3) Adicionar o componente de ListaSuspensa ao Formulario e assim criar nossos parâmetros pela tag.
`<ListaSuspensa times={times} />`

4) Criar um array times que será enviado pela props
```
const times = [
  "Programação",
  "Frontend",
  "..."
]
```

**COMPONENTE BOTAO E A PROPS.CHILDREN**
1) Criação padrão de componente
2) Adicionar o Botao no Formulario, aqui vai a primeira diferença desse componente, pois vamos abrir a tag e escrever o conteúdo dentro dela
`<Botao>Criar card</Botao>`
3) E dentro do componente Botao vamos receber as informações através do `props.children`, que são os filhos do componente, ou seja, qualquer coisa que foi adicionada dentro da tag e não nas propriedades da tag.


**AJUSTANDO O FORMULARIO**
Agora que temos um botão no formulário vamos endenter o funcionamento dele. Todo botão sem tipo definido dentro de um formulário por padrão é um submit, sendo assim ele vai dar um post na mesma página passando as informações pela url. A principal diferença entre escutar o click ou o submit de um formulário é que no submit o navegador faz uma validação padrão usando as próprias propriedades dos campos, já no click seria preciso fazer isso na mão.

Com isso em mente vamos adicionar um escutador na tag do form `<form onSubmit={aoSalvar}>` juntamente com a função que será executada.
```
const aoSalvar = (evento) => { 
  evento.preventDefault()
}
```

* Todo escutador de evento passa o evento como parâmetro, com ele podemos acessar uma gama de informações e funções. No código usamos o `preventDefault()` que é o método que previne o comportamente padrão do submit.

Outra coisa que também podemos fazer é criar parâmetros para personalisar as propriedades dos campos, aqui vamos usar as props para dizer que o campo é ou não obrigatório(required) passando o parâmetro `obrigatorio={true}` e recebendo no campo `required={props.obrigatorio}` 


**APRENDENDO SOBRE USESTATE**
* Para receber os campos do formulário precisamos atribuir o que o usuário está digitando a uma variável, ela também vai controlar o estado do componente. Para isso o React utiliza um hook chamado useState, ele é responsável pela criação de variáveis que irão ajudar a controlar a atualização do componente.

* Para utilizar o useState precisamos importar a classe e usar o seguinte padrão na criação da variável:
 `const [variavel, setVariavel] = useState('') ` onde variavel é o nome que vamos usar para ler o valor, setVariavel é o método que será usado sempre que for preciso atualizar o valor da variável e useState('') é onde abribuimos o valor inicial da variável, que no exemplo é uma string vazia. 

 * Os componentes CampoTexto e ListaSuspensa irão receber informações do usuário e essas informações devem ser repassadas para o componente pai que é o Formulario, então para que isso funcione precisamos "elevar o estado do componente" que significa que o useState que o componente filho vai alterar será passado para o pai através das props.

 **ELEVAÇÃO DO ESTADO**
 1) No componente filho vamos pegar duas informações pela props, valor e aoAlterado, onde esse último é uma função que passa o valor digitado pelo usuário para o método set da variável correspondente.
```
const aoDigitado = (evento) => {
    props.aoAlterado(evento.target.value)
}
...
<input value={props.valor} onChange={aoDigitado} ... />
```

2) No componente pai vamos recuperar essa informação e alterar o valor das variáveis.
```
const [nome, setNome] = useState('')
const [cargo, setCargo] = useState('')
const [imagem, setImagem] = useState('')
const [time, setTime] = useState('')
...
<CampoTexto valor={nome} aoAlterado={valor => setNome(valor)} ... />
<CampoTexto valor={cargo} aoAlterado={valor => setCargo(valor)} ... />
<CampoTexto valor={imagem} aoAlterado={valor => setImagem(valor)} ... />
<ListaSuspensa valor={time} aoAlterado={valor => setTime(valor)} ... />
```

**CADASTRAR O COLABORADOR**
*No App.js*
1) Criar a variável com useState, do tipo array, que vai receber os colaboradores
2) Criar a função que adiciona o colaborador no array de colaboradores
3) Criar a props no Formulario que chama a função passando o colaborador
```
const [colaboradores, setColaboradores] = useState([])

const aoNovoColaboradorAdicionado = (colaborador) => {
  setColaboradores([...colaboradores, colaborador])
}
...
<Formulario aoColaboradorCadastrado={colaborador => aoNovoColaboradorAdicionado(colaborador)}/>
...
```
* Spread Operator são os três pontos antes do array `...` ele permite espalhar os elementos do array em locais que se esperam mais de um elemento, no código acima para modificar o array de colaboradores ele está espalhando os já cadastrados e adicionando um novo ao final.

*No Formulario.js*
4) Voltando na função aoSalvar vamos chamar a props que eleva o colaborador para o App.js passando as informações do colaborador 
```
props.aoColaboradorCadastrado({
  projeto,
  nome,
  imagem,
  time
})
```
* Para criar esse objeto usamos uma forma abreviada onde se a chave terá o mesmo nome que a variável podemos omitir o nome da váriavel.

**COMPONENTE TIME E CSS INLINE**
Para montar a listagem dos times é preciso criar um novo componente.
1) Criar um componente chamado Time, nele vamos precisar de três informações: nome do time, cor primária e cor secundária, então vamos preparar o código para receber essas propriedades.
```
const Time = {props} => {
    const css = { backgroundColor: props.corSecundaria }
    return (
        <section className='time' style={css}>
            <h3>style={{borderColor:  props.corPrimaria}}>{props.nome}</h3>
        </section>
    )
}
```
* Para usar o css inline precisamos criar um objeto, onde chamamos as propriedades usando camelCase, perceba que tanto faz criar uma variável ou chamar na própria tag sempre vai haver duas {{}} a primeira vai sinalizar que vamos usar uma variável e a segunda para criar o objeto.

2) Adicionar o componente Time ao App.js e criar um array de objetos pra armazenar as informações que o componente vai precisar.

3) Para mostrar os 7 times vamos usar o map para percorrer o objeto de times retornando a chamada do componente passando as props adequadas.
```
const times = [{
  nome: 'Programação',
  corPrimaria: '#57C278',
  corSecundaria: '#D9F7E9',
},
...]
...
{times.map{time => <Time key={time.nome} nome={time.nome} corPrimaria={time.corPrimaria} corSecundaria={time.corSecundaria} />}}
```

**REFATORANDO**
Como temos dois componentes precisando usar uma lista de times não é viável, ou melhor, não é manutenível manter a mesma lista em dois lugares diferentes, por isso elevamos o estado do componente Time e agora vamos elevar novamente o estado do componente ListaSuspensa, sendo assim vamos excluir a lista de times de dentro do Formulario e fazer o Formulario receber essa lista pelo App.js

1) Fazer o Formulario receber apenas o nome dos times `<Formulario times={times.map(time => time.nome)} .../>`

2) Onde ListaSuspensa recebia a variável times agora vai receber de props `<ListaSuspensa times={props.times} .../>`

**COMPONENTE COLABORADOR E O MÉTODO FILTER**
Nesse ponto vamos criar o card do colaborador, ou seja, mostrar as informações que foram coletadas pelo formulário.
1) Criar o componente Colaborador, ele receberá pela props: nome, cargo, imagem e a cor do card (que ele vai pegar de acordo com o time)
`const Colaborador = ({ nome, cargo, imagem, corDeFundo }) => {...}`
* Outra forma de passar a props é desestruturar o objeto passando apenas o nome das chaves.

2) Antes de adicionar o componente Colaborador ao Time precisamos passar as informações do colaborador para o Time. Voltamos ao App.js e na chamada do Time passamos os colaboradores `times.map{time => <Time colaboradores={colaboradores} corPrimaria={time.corPrimaria} .../>`

3) Por fim, adicionamos o Colaborador ao Time passando a props.colaboradores, usando o map para que ele crie um card para cada colaborador ` {props.colaboradores.map( colaborador => <Colaborador nome={colaborador.nome} cargo={colaborador.cargo} imagem={colaborador.imagem} corDeFundo={props.corPrimaria})}`

4) Existe um problema, pois o mesmo colaborador aparece em todos os times. Para consertar vamos fazer um pequeno ajuste no ponto 2, na chamada do Time adicionamos um filtro, assim ele só vai passar para o Time os colaboradores que tiverem o mesmo time.
`<Time colaboradores={colaboradores.filter(colaborador => colaborador.time === time.nome)} .../>`

**RENDERIZAÇÃO CONDICIONAL**
Aqui vamos arrumar alguns detalhes para deixar o projeto mais funcional: 1º Esconder os times que ainda não tem colaboradores e 2º Resetar os campos do formulário.

Para resolver o primeiro problema vamos voltar ao componente Time, onde teremos usar duas lógicas:
1) Usando o &&, onde o React avalia a primeira condição (ou mais condições) do if e se for verdade ele renderiza o restante do código.
```
props.colaboradores.lenght > 0 && <section className='time' style={css}
    <h3> style={{ borderColor: props.corPrimaria }}>{props.nome}</h3>
    <div className='colaboradores'>
        {props.colaboradores.map( colaborador => <Colaborador nome={colaborador.nome} cargo={colaborador.cargo} imagem={colaborador.imagem} corDeFundo={props.corPrimaria})}
    </div>
</section>
```
2) Usando operador ternário, onde ele teria duas opções de renderização uma caso true e outra caso false.
```
props.colaboradores.lenght > 0 ? <section className='time' style={css}
    <h3> style={{ borderColor: props.corPrimaria }}>{props.nome}</h3>
    <div className='colaboradores'>
        {props.colaboradores.map( colaborador => <Colaborador nome={colaborador.nome} cargo={colaborador.cargo} imagem={colaborador.imagem} corDeFundo={props.corPrimaria})}
    </div>
</section>
: ""
```
Os dois códigos possuem o mesmo resultado nessa situação, mas em algumas ocasiões o segundo será a melhor opção. Isso porque o segundo código oferece a possibilidade de renderizar um outro código caso a condição não seja atendida.

Para aplicar a 2ª melhoria é muito simples, só precisamos resetar as variável que criamos dentro do Formulario. Dentro do método aoSalvar, logo após enviar as informações via props vamos adicionar o seguinte código:
```
setNome('')
setCargo('')
setImagem('')
setTime('')
```

**COMPONENTE RODAPE**
Esse componente encerra o projeto e ele é muito simples, pois só precisamos reproduzir o layout criando o html e css e então adicionar a tag `<Rodape/>` no final do App.js

**CONTEÚDO EXTRA**
Uma forma de debugar a aplicação através do navegador é adicionar a palavra `debugger` ao código, no ponto que deseja analisar, assim quando você rodar a aplicação no chrome com a ferramenta do desenvolvedor aberta, a execução será pausada e uma nova aba de opções surgirá para ajudar na analise do código.  