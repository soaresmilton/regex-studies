Repositório destinado aos meus estudos em expressões regulares. 

## Regular Expressions (Regex)

Expressões regulares ou **regex** são usadas nas linguagens de programação para encontrar determinadas partes de texto (string), através da criação de padrões específicos.

Por exemplo, para encontrar a palavra "galho" na frase: "Cada macaco em seu galho", podemos usar a regex `/galho/` para fazer esse match. Aqui, uma observação importante é notar que não é necessário que as palavras as serem buscadas estejam entre aspas.

Em JavaScript, podemos usar as expressões regulares de várias formas. Uma delas é utilizando o método *test()* própria expressão regular, recebendo como parâmetro a string a ser verificada. Esse método retorna um booleano - *true*  ou *false.*

```jsx
let testStr = "MiltonAntonioSoares";
let testRegex = /Soares/;
testRegex.test(testStr); // RETORNA true
```

Outra observação importante para as regex, é que elas são case sensitive. Portanto, fazendo buscas literais, com a do exemplo anterior, a depender da forma que o texto for procurado a regex poderá não entender o texto buscado, retornando um valor falso. Exemplo:

```jsx
let testStr = "MiltonAntonioSoares";
let testRegex = /soares/;
testRegex.test(testStr); // RETORNA false
```

Nas expressões regulares, podemos utilizar alguns operadores para construirmos expressões poderosas com maior nível de dinamismo nas buscas. Como exemplo operador OU, que verifica uma string, comparando um ou outro valor da expressão regular. O separador OU, é presentado por uma `|` e podemos passar quantos valores que quisermos para fazer a comparação. Exemplo:

```jsx
let petString = "James has a pet cat.";
let petRegex = /dog|cat|bird|fish/; 
let result = petRegex.test(petString);
```

Para conseguirmos construir regex mais poderosas, que captam letras maiúsculas e/ou minúsculas em uma mesma string, podemos utilizar uma flag específica para isso. Nesse caso, utilizaremos a flag `i` . Uma forma de utilizar essa flag, é passando ela no final da expressão: `/ignorecase/i` ⇒ essa expressão procura frases como **IGnoreCase** ou **IGNORECASE** ou **ignorecase**... Na prática:

```jsx
let myString = "MiltonAntonioSoares";
let fccRegex = /miltonantonioSoares/i; 
let result = fccRegex.test(myString);// RETORNA true
```

Até então, apenas verificamos se certa expressão (ou padrão) existe em determinada string. Outro método existente em JavaScript, que nos permite trabalhar com regex é o método *match()*. O modo de aplicação do *match()* é o contrário do método *test()* visto anteriormente. O método *match()* retorna a própria regex procurada na string, caso não encontrar (ou não der match) retorna null. Veja o exemplo abaixo:

```jsx
let myStr = 'Milton Soares Moraes';
let myRegx = /Milton/i;
let v = myStr.match(myRegx);
console.log(v);
/* RETORNA:
[
  'Milton',
  index: 0,
  input: 'Milton Soares Moraes',
  groups: undefined
]

*/
```

Aplicando uma regex que não existe na string

```jsx
let myStr = 'Milton Soares Moraes';
let myRegx = /nao tem essa string/i;
let v = myStr.match(myRegx);
console.log(v); //RETORNA nu
```

Adicionado a flag `g` na nossa expressão regular, conseguimos encontrar padrões repetidos no todo de uma string. Com o método match, retornamos sempre a primeira ocorrência do match que ocorrer entre a regex e a string analisada. Com a flag `g` o método *match()* retorna um array de comprimento n, em que n é igual a quantidade de elementos que deram match. Veja no exemplo:

```jsx
let myString = 'Repetir, Repetir, Repetir, Repetir';
let myRegex = /Repetir/;
let result = myString.match(myRegex);
console.log(result); //RETORNA [ 'Repetir']
```

Usando a flag `g` :

```jsx
let myString = 'Repetir, Repetir, Repetir, Repetir';
let myRegex = /Repetir/g;
let result = myString.match(myRegex);
console.log(result); //RETORNA [ 'Repetir', 'Repetir', 'Repetir', 'Repetir' ]
```

**OBS: *Importante lembrar que podemos combinar o uso de flags, podendo usar a flag `g` em conjunto com a flag `i` por exemplo.***

Outro comando pertinente que existe nas expressões regulares é o chamado *wildcard* representado por um ponto `.` . O wildcard permite substituir qualquer caractere da regex por qualquer um outro. Esse comando é muito utilizado quando não precisamos ou não queremos saber determinada letra ou palavra de uma string. Veja como usar:

```jsx
let humStr = "I'll hum a song";
let hugStr = "Bear hug";
let huRegex = /hu./;
huRegex.test(humStr); //RETORNA true
huRegex.test(hugStr); // RETORNA true
```

```jsx
let myString = 'Milton Soares Moraes';
let myRegex = /mil./i;
let result = myRegex.test(myString);
console.log(result); //RETORNA true
```

Até então, vimos os casos mais extremos existentes nas regex, utilizando pesquisas literais `/minha regex/` ou utilizando pesquisas gerais que dão *match* com tudo com o *wildcard* `.`. Porém, eventualmente precisamos encontrar palavras ou frases em nossas strings que não, necessariamente, sejam literais ou estáticas. Por exemplo, digamos que precisamos encontrar (ou dar match) em *bag*, *big* e *bug*, mas não queremos encontrar *bog* e nem *beg*. Para isso, podemos utilizar as os caracteres de **classes** das expressões regulares representadas por `[ ]`. Vamos ao exemplo acima:

```jsx
let myString = 'big, bag, beg, bog, bug';
let myRegex = /b[aiu]g/gi;
let result = myString.match(myRegex);
console.log(result); // RETORNA [ 'big', 'bag', 'bug' ]
```

Em conjunto com as formas de classes (`[ ]`) podemos *setar* um range de caracteres para buscar casos específicos em uma string. Por exemplo, imagine que queremos buscar todas as letras do alfabeto, construir uma regex passando todos as letras dentro dos caracteres de classes seria inviável. Por isso, existe o recurso `-` que determina um range entre dois caracteres. Por exemplo, para termos todas as letras do alfabeto podemos usar: `/[a-z]/gi`

```jsx
let catStr = "cat";
let batStr = "bat";
let matStr = "mat";
let bgRegex = /[a-e]at/;
catStr.match(bgRegex); //RETORNA "cat"
batStr.match(bgRegex); //RETORNA "bat"
matStr.match(bgRegex); //RETORA null
```

***OBS: Importante destacar que o recurso de range, proporcionado pelo hífen `-` pode ser usado tanto para letras quanto para números. Exemplo, pesquisando por todas as letras e números: `/[a-z0-9]/ig`***

```jsx
let quoteSample = "Blueberry 3.141592653s are delicious.";
let myRegex = /[h-s2-6]/gi;
let result = quoteSample.match(myRegex);
```