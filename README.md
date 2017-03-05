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
