---
id: FunctionClass
title: Function
---

Um objeto **`4D.Function`** contém um trecho de código que pode ser executado a partir de um objeto, usando o operador `()`, ou usando as funções [`apply()`](#apply) e [`call()`](#call). 4D propõe três tipos de objetos `Function`:

- **as funções nativas**, ou seja, funções incorporadas de várias classes 4D, como `collection.sort()` ou `file.copyTo()`.
- **as funções usuário**, criadas nas [classes usuário](Concepts/classes.md) usando a palavra-chave [Function](Concepts/classes.md#function).
- **funções de fórmula**, ou seja, funções que podem executar qualquer fórmula 4D.

### Objetos de formulários

Os comandos [Formula](../commands/formula.md) e [Formula from string](../commands/formula-from-string.md) permitem que você crie [objetos`4D.Function`](#formula-objects) para executar qualquer expressão ou código 4D expresso como texto.

Objetos formulário podem ser encapsulados em propriedades objeto:

```4d
 var $f : 4D. Function
 $f:=New object
 $f.message:=Formula(ALERT("Hello world"))
```

Essa propriedade é uma "função objeto" ou seja uma função que é restrita a seu objeto pai. Para executar uma função armazenada em uma propriedade objeto, use o operador **()** depois do nome propriedade, tal como:

```4d
 $f.message() //exibe "Hello world"
```

Também se admite a sintaxe com parênteses:

```4d
 $f["message"]() //exibe "Hello world"
```

Note que mesmo se não tiver parênteses (ver abaixo), uma função objeto a ser executada deve ser chamda com () parênteses. Chamar só a propriedade de objeto devolverá uma nova referência à fórmula (e não a executará):

```4d
 $o:=$f.message //devolve o objeto fórmula em $o
```

Você também pode executar uma função usando as funções [`apply()`](#apply) e [`call()`](#call):

```4d
 $f.message.apply() //exibe "Hello world"
```

#### Utilização de parâmetros

Você pode passar parâmetros para suas fórmulas usando uma sintaxe de parâmetro sequencial baseada em $1, $2...$n. Por exemplo, pode escrever:

```4d
 var $f : Object
 $f:=New object
 $f.message:=Formula(ALERT("Hello "+$1))
 $f.message("John") //exibe "Hello John"
```

Ou usando a função [.call()](#call):

```4d
 var $f : Object
 $f:=Formula($1+" "+$2)
 $text:=$f.call(Null;"Hello";"World") //retorna "Hello World"
 $text:=$f.call(Null;"Welcome to";String(Year of(Current date))) //retorna "Welcome to 2019" (por exemplo)
```

#### Parâmetros a um único método

Para mais conveniência, quando a fórmula é feita de um único método de projeto, parâmetros podem ser omitidos na inicialização do objeto fórmula. Pode ser passado quando a fórmula for chamada. Por exemplo:

```4d
 var $f : 4D.Function

 $f:=Formula(myMethod)
  //Escrevendo Formula(myMethod($1;$2)) não é necessário
 $text:=$f.call(Null;"Hello";"World") //retorna "Hello World"
 $text:=$f.call() //retorna "How are you?"

  //myMethod
 #DECLARE ($param1 : Text; $param2 : Text)->$return : Text
 If(Count parameters=2)
    $return:=$param1+" "+$param2
 Else
    $return:="How are you?"
 End if
```

Parâmetros são recebidos dentro do método, na ordem que são especificados na chamada.

### Resumo

|                                                                                                              |
| ------------------------------------------------------------------------------------------------------------ |
| [<!-- INCLUDE #FunctionClass.apply().Syntax -->](#apply)<br/><!-- INCLUDE #FunctionClass.apply().Summary --> |
| [<!-- INCLUDE #FunctionClass.call().Syntax -->](#call)<br/><!-- INCLUDE #FunctionClass.call().Summary -->    |
| [<!-- INCLUDE #FunctionClass.source.Syntax -->](#source)<br/><!-- INCLUDE #FunctionClass.source.Summary -->  |

<!-- REF FunctionClass.apply().Desc -->

## .apply()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 17 R3   | Adicionado |

</details>

<!-- REF #FunctionClass.apply().Syntax -->**.apply**() : any<br/>**.apply**( *thisObj* : Object { ; *formulaParams* : Collection } ) : any<!-- END REF -->

<!-- REF #FunctionClass.apply().Params -->

| Parâmetro     | Tipo       |                             | Descrição                                                                                                                       |
| ------------- | ---------- | :-------------------------: | ------------------------------------------------------------------------------------------------------------------------------- |
| thisObj       | Object     |              ->             | Objeto a ser retornado pelo comando This na fórmula                                                                             |
| formulaParams | Collection |              ->             | Coleção de valores a serem passados como $1...$n quando `formula` for executado |
| Resultados    | any        | <- | Valores de execução de fórmula                                                                                                  |

<!-- END REF -->

#### Descrição

A função `.apply()` <!-- REF #FunctionClass.apply().Summary -->executa o objeto `formula` ao qual ele é aplicado e retorna o valor resultante<!-- END REF -->. O objeto fórmula pode ser criado usando os comandos `Formula` ou `Formula from string`.

No parâmetro *thisObj* pode passar uma referência ao objeto a ser usada como `This` na fórmula.

Também pode passar uma coleção a ser usada como parâmetros $1...$n na fórmula usando o parâmetro opcional *formulaParams*.

Note que `.apply()` é similar a [`.call()`](#call) exceto que os parâmetros são passados como coleção. Isso pode ser útil para passar resultados calculados. Isso pode ser útil para passar resultados calculados.

#### Exemplo 1

```4d
 var $f : 4D. Function
 $f:=Formula($1+$2+$3)

 $c:=New collection(10;20;30)
 $result:=$f.apply(Null;$c) // retorna 60
```

#### Exemplo 2

```4d
 var $calc : 4D. Function
 var $feta; $robot : Object
 $robot:=New object("name";"Robot";"price";543;"quantity";2)
 $feta:=New object("name";"Feta";"price";12.5;"quantity";5)

 $calc:=Formula(This.total:=This.price*This.quantity)

 $calc.apply($feta) // $feta={name:Feta,price:12.5,quantity:5,total:62.5}
 $calc.apply($robot) // $robot={name:Robot,price:543,quantity:2,total:1086}
```

<!-- END REF -->

<!-- REF FunctionClass.call().Desc -->

## .call()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 17 R3   | Adicionado |

</details>

<!-- REF #FunctionClass.call().Syntax -->**.call**() : any<br/>**.call**( *thisObj* : Object { ; ...*params* : any } ) : any<!-- END REF -->

<!-- REF #FunctionClass.call().Params -->

| Parâmetro  | Tipo   |                             | Descrição                                                                                                            |
| ---------- | ------ | --------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| thisObj    | Object | ->                          | Objeto a ser retornado pelo comando This na fórmula                                                                  |
| params     | any    | ->                          | Valores a serem passados como $1...$n quando a fórmula for executada |
| Resultados | any    | <- | Valores de execução de fórmula                                                                                       |

<!-- END REF -->

#### Descrição

A função `.call()` <!-- REF #FunctionClass.call().Summary -->executa o objeto `formula` ao qual ele está aplicado e retorna o valor resultante<!-- END REF -->. O objeto fórmula pode ser criado usando os comandos `Formula` ou `Formula from string`.

No parâmetro *thisObj* pode passar uma referência ao objeto a ser usada como `This` na fórmula.

Você também pode passar valores para serem usados como parâmetros *$1...$n* na fórmula usando os parâmetros *params* opcionais.

Observe que `.call()` é semelhante a [`.apply()`](#apply), exceto pelo fato de que os parâmetros são passados diretamente.

#### Exemplo 1

```4d
 var $f : 4D. Function
 $f:=Formula(Uppercase($1))
 $result:=$f.call(Null;"hello") // retorna "HELLO"
```

#### Exemplo 2

```4d
 $o:=New object("value";50)
 $f:=Formula(This.value*2)
 $result:=$f.call($o) // devolve 100
```

<!-- END REF -->

<!-- REF FunctionClass.source.Desc -->

## .source

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 18 R2   | Adicionado |

</details>

<!-- REF #FunctionClass.source.Syntax -->**.source** : Text <!-- END REF -->

#### Descrição

A propriedade `.source` <!-- REF #FunctionClass.source.Summary -->contém a expressão de origem da `fórmula` como texto<!-- END REF -->.

Essa propriedade é **somente leitura**.

#### Exemplo

```4d
 var $of : 4D.Function
 var $tf : Text
 $of:=Formula(String(Current time;HH MM AM PM))
 $tf:=$of.source //"String(Current time;HH MM AM PM)"
```

<!-- END REF -->
