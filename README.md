# laracasts_ES2015_Crash_Course

## To Var, Let, or Const

Para declarar variáveis pode se usar let e const

let para elas existirem apenas no escopo em que voce definiu
const para elas nao poderem ser sobrepostas

##  Arrows

Pode se usar => para definir as closures no lugar de function.
Ex:

``` js
let names = ['taylor', 'jeffrey' 'adam' ];

names = names.map((name) => {
name + 'is coll';
});
```

Em que:
Pode nao se usar {} quando a funcao tem apenas uma linha
Esta implicito o return quando possui apenas uma linha


## Default Parameters

Pode se no es6 aceitar parametros com valor defaut

## Rest and Spread

O operador rest, funciona na declaracao de parametroes de funções.
Se usar '...' para indicar que todos os parametros passados do ponto para frente, serão formados em um array.

``` js
function sum(...numbers) {
	return numbers.reduce(function(prev, current){
		return prev + current;
	})
}

console.log(sum(1,2,3));
```

O operador spread tem efeito contrario, em que na chamada ele separa o array em valores fora, para serem utilizados como parametros

``` js
function sum(x, y) {
		return x + y;
}

let nums = [1,2];
console.log(sum(...nums));
```

## Template Strings

Pode se usar a sintxa ${} para concatenar strings

``` js
let name = 'Bar';

let template = ` 
<div class="Alert">
	<p>${name}</p>
</div>	
`;
 console.log(template);
```

## Awesome Object Enhancements

Atalho para atribtos em objetos, quando quer se usar a declaracao de um objeto como name: name, (em que a variavel name já é existente) pode se resumir utilizando apenas name.

Para metodos pode resumir removendo a clasula function e deixando o nome do metodo com  () na frente

``` js
function getPerson() {
	let name = 'John';
	let age = 23;

	return {
		name,
		age,
		greet() {
			return `Hello, ${this.name}`;
		}
	};
}

alert(getPerson().greet());
```

Desustruturação de objetos:  podemos estrair em variaveis atributos de objetos, facilitando o uso apenas dos atributos desejados:

``` js
let data = {
	name: 'Karen',
	age: 32,
	results: ['foo', 'bar'],
	count: 30
};

let {results, count} = data;

console.log(results, count);
```

Sendo que funciona tambem com parametros de uma função:

``` js
function greet({name, age}) {
	console.log(`Hello, ${name}. You are ${age}.`);
}

let data = {
	name: 'Karen',
	age: 32,
	results: ['foo', 'bar'],
	count: 30
}; // Recebido de um  request AJAX

greet(data);
```

## Classes

Nova sintaxe mais limpa para classes, junto com algumas funcionalidades

``` js
class User {
	constructor(username, email){
		this.username = username;
		this.email = email;
	}

	changeEmail(newEmail){
		this.email = newEmail;
	}

	static register(username, email){
		return new User(username, email);
	}

	get foo(){
		return 'foo';
	}

}

let user = new User('Jeffrey','support@laracasts.com');

user.changeEmail('foo@example.com');

console.dir(user);

let user2 = new User.register('Jeffrey111','suppor111t@laracasts.com');

console.dir(user2);
```

- Possivel criar metodos staticos usando a static antes dos metodos.
- Possivel criar getter and setter, utilzando get ou set antes dos metodos
- Possivel utilizar heranca, utilizando Class Foo extends Bar


## Modules 

Modulos são na sua essência arquivos.
Em que separamos os arquivos com funcionalidades em que importamos uma a uma

Exemplo arquivo 'TaskColletion.js' utilizando 'export' para disponibilizar:

``` js
export class TaskCollection {
	constructor(tasks = []){
		this.tasks = tasks;
	}

	dump(){
		console.log(this.tasks);
	}
}
```

Em que é importado com a clausula import {TaskCollection}  selecionando um ou mais itens para importar.
``` js
import {TaskCollection} from './TaskCollection';

new TaskCollection([
	'Go to the Store',
	'Eat Cake',
	'Finish screencast'
]).dump();
```

Podemos incluir mais exportações no arquivo 'TaskCollection.js'


``` js
export let foo = 'bar';
export myfunc = function () {};
```

E importar incluindo variaveis em import
``` js
import {TaskCollection, foo, myfunc} from './TaskCollection';
```

É possivel definir uma importacao default no arquivo como:
``` js
export default class TaskCollection {
	constructor(tasks = []){
		this.tasks = tasks;
	}
```

e importar como:
``` js
import TaskCollection from './TaskCollection';
```

## Promisses

Promisses são funcões em que reservamos para ações que ainda nao foram executadas.
Que quando executadas, são feitas de modo assincrono.

Várias blibliotecas utilizam as promisses, tendo como exemplo as funções que requisições AJAX, que levam algum tempo.

``` js
let timer = new Promise(function(resolve, reject){
	console.log('Init Promisse');
	setTimeout(function () {
		console.log('Timeout done');
		resolve(); 
	}, 4000);

});

timer.then(function () {
	console.log('Proceed now that timer has concluded');
});
```

No exemplo, definimos uma promise chamada timer.
Quando a ação deseja na declaração da proxima for finalizada, devemos executar 'resolve()'. Que será o instante em que o o 'then' será chamado. 
Caso desejado podemos tambem usar 'reject()' para quando ocorrer erro, e disparar com 'catch' ou entao o segundo parametro do 'then'