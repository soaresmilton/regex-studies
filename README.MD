## Regular Expressions (Regex)
Esse repositório é destinado aos meus estudos em expressões regulares. 
Primeiramente, será feito um breve estudo das aulas encontradas em [Free Code Camp](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/), especificamente na parte de expressões regulares. Além disso, alguns cotneúdos e explicações são retirados do [REGEXR](https://regexr.com/).

---
### Introdução

Expressões regulares ou **regex** é um método conciso e flexível para identificação de caracteres específicos, palavras e/ou frases em *strings.* As regex possuem uma maneira padrão de escrita e é entendível por quase qualquer linguagem de programação.

Nesse artigo, iremos discorrer a respeito das regex e introduzir os comandos e padrões básicos dessa ferramenta

---

### Matches perfeitos e o método test(

Por exemplo, para encontrar a palavra "galho" na frase: "Cada macaco em seu galho", podemos usar a regex `/galho/` para fazer esse match. Aqui, uma observação importante é notar que não é necessário que as palavras as serem buscadas estejam entre aspas como geralmente usamos essa notação para descrever strings em linguagens de programação.

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

---

### Operador "ou" ( | ):

Nas expressões regulares, podemos utilizar alguns operadores para construirmos expressões poderosas com maior nível de dinamismo nas buscas. Como exemplo operador OU, que verifica uma string, comparando um ou outro valor da expressão regular. O separador OU, é presentado por uma `|` e podemos passar quantos valores que quisermos para fazer a comparação. Exemplo:

```jsx
let petString = "James has a pet cat.";
let petRegex = /dog|cat|bird|fish/; 
let result = petRegex.test(petString);
```

---

### Flags: ignorecase ( i )

Para conseguirmos construir regex mais poderosas, que captam letras maiúsculas e/ou minúsculas em uma mesma string, podemos utilizar uma flag específica para isso. Nesse caso, utilizaremos a flag `i` . Uma forma de utilizar essa flag, é passando ela no final da expressão: `/ignorecase/i` ⇒ essa expressão procura frases como **IGnoreCase** ou **IGNORECASE** ou **ignorecase**... Na prática:

```jsx
let myString = "MiltonAntonioSoares";
let fccRegex = /miltonantonioSoares/i; 
let result = fccRegex.test(myString);// RETORNA true
```

---

### Utilizando o método match()

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
console.log(v); //RETORNA null
```

---

### Flags: global searching ( g )

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

---

### Wildcard ( . )

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

---

### Caracteres de classes ( [ ] ) e conjuntos de caracteres ( - )

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

---

### Negated Character Sets ( ^ )

Ate então vimos situações as quais procuramos por palavras ou frases que gostaríamos de encontrar (necessariamente). Com as expressões regulares, podemos também, determinar palavras, letras ou frases que temos a certeza que não queremos encontrar em uma *string*. Esse tipo de situação é chamada de *negated character sets.* 

Para usar esse recurso, utilizaremos o operador `^` . Para utilizar esse recurso, devemos passar o acento (*caret*) após nosso operador de classes `[ ]` e antes do conjunto de caracteres que não queremos identificar. Por exemplo: `/[^aeiou]/gi` ⇒ essa regex não identifica as vogais em uma string. Em outras palavras, essa regex dará *match* com todas os caracteres que não sejam vogais, incluindo caracteres especiais como: *., !, [, @, /*

Na prática:
Uma *regex* que ignora todos os caracteres que são vogais e números 

```jsx
let myString = "3 tigres brancos";
let myRgx = /[^aeiou0-9]/gi;
let result = myString .match(myRgx ); 
console.log(result);

/* RETORNA 
[
  ' ', 't', 'g', 'r',
  's', ' ', 'b', 'r',
  'n', 'c', 's'
]
*/
```

***OBS: nota-se que essa regex também retorna os espaços em branco no array.***

---

### Encontrando caracteres seguidos em uma string ( + )

Em algum momento iremos precisar encontrar caracteres ou grupos de caracteres que aparecem seguidos um dos outros ao longo de uma *string.* Por exemplo, na palavra "Massachusetts", temos 'ss' e  'tt' seguidos um dos outros. Então, caso quisermos encontrar em um único *match* algum desses caracteres, utilizamos o operador `+` podemos construir a seguinte regex: `/s+|t+/gi` . Veja na prática:

```jsx
let myStr = "Massachusetts";
let myRgx = /s+|t+/gi;
let result = myStr.match(myRgx);
console.log(result); // RETORNA [ 'ss', 's', 'tt', 's' ]
```

***OBS: essa regex inclusive retorna os caracteres que não estão seguidos uns aos outros como valores separados no array.***

---

### Operador ( * ):

Em algumas situações precisamos identificar caracteres ou conjunto de caracteres que ocorrem zero ou mais vezes. Para montar esse tipo de expressão utilizamos o operador `*` após os caracteres que quisermos identificar. Veja na prática:

```jsx
let myString1 = "goooooooaaall!";
let myString2 = "Garbage Collector";
let myString3 = "sem chances para a essa";
let myString4 = "gggggggo";
let myRgx = /go*/gi;
let result1 = myString1.match(myRgx);
let result2 = myString2.match(myRgx);
let result3 = myString3.match(myRgx);
let result4 = myString4.match(myRgx);
console.log(result1); //RETORNA [ 'gooooooo' ]
console.log(result2); //RETORNA [ 'G', 'g' ]
console.log(result3); //RETORNA null
console.log(result4); //RETORNA [ 'g',  'g', 'g', 'g',  'g', 'g', 'go' ]
```

***OBS: Perceba que não é encontrado o caractere "o" sozinho na segunda string, porém é encontrado o caractere "g". Além disso, em myString4 ("***gggggggo***") são encontrados os "g" e colocados em index diferentes do array de retorno, salvo pelo último valor "go" que foi identificado conforme o esperado.***

---

### Encontrando caracteres com o Lazy Matching ( ? )

Em expressões regulares, um *greedy match* encontra a maior parte possível de uma string que satisfaça o padrão de determinada regex, retornando o valor do *match* como resultado. Por exemplo:

```jsx
let myStr = "Titanic";
let myRgx = /t[a-z]*i/gi;
let result = myStr.match(myRgx);
console.log(result); //RETORNA [ 'Titani' ]
```

Uma alternativa contrária a isso, ou seja, buscar a menor substring que satisfaça a regex é utilizando o operador `?`

Aplicando na mesma situação:

```jsx
let myStr = "Titanic";
let myRgx = /t[a-z]*?i/gi;
let result = myStr.match(myRgx);
	console.log(result); // RTORNA [ 'Ti', 'tani' ]
```

***OBS:*** ***Parsing HTML with regular expressions should be avoided, but pattern matching an HTML string with regular expressions is completely fine.***

---

### Encontrando padrões no início de uma string

Anteriormente vimos o uso do operador *caret* `^` como uma forma de ignorar caracteres em uma *string* usando o operador dentro de colchetes: `/[^caracteresQueQueremosIgnorar]/` **.

Fora dos colchetes, o mesmo operador `^` é utilizado para dar *match* em caracteres ou conjunto de caracteres que iniciam uma determinada *string*. Na prática:
 

```jsx
let myRegex = /^Milton/;
let firstString = "Milton é a primeira palavra dessa frase";
let isFirst = myRegex.test(firstString);
console.log(isFirst); //RETORNA true
let secondString = "Nessa frase, Milton não é a primera palavra";
let isNotFirst = myRegex.test(secondString);
console.log(isNotFirst) //RETORNA false
```

---

### Encontrando padrões no final de uma string

Além de encontrar padrões no início de uma *string* como vimos anteriormente. Também podemos encontrar padrões no final de uma *string.* Para isso, utilizamos o operador `$` no final da construção da regex. Veja na prática:

```jsx
let myRegex = /Milton$/;
let firstString = "Nessa frase, a última palavra é Milton";
let isFirst = myRegex.test(firstString);
console.log(isFirst); //RETORNA true
let secondString = "Nessa frase, Milton não é a última palavra";
let isNotFirst = myRegex.test(secondString);
console.log(isNotFirst) //RETORNA false
```

---

### Encontrando todas as letras e números (shorthand character classes):

Como vimos nos tópicos anteriores podemos usar os caracteres de classes `[ ]` para determinar conjuntos de caracteres de forma mais prática. Por exemplo, caso quisermos encontrar todas as letras e números poderíamos escrever uma regex como essa: `/[A-Za-z0-9_]/g` . 

Como esse padrão de regex é bem comum de ser utilizado, foi desenvolvido um atalho que representa esse padrão e é representado por: `/\w/`

Na prática:

```jsx
let longHand = /[A-Za-z0-9_]+/;
let shortHand = /\w+/;
let numbers = "55";
let varNames = "uma string importante";
console.log(longHand.test(numbers)); //RETORNA true
console.log(shortHand.test(numbers)); //RETORNA true
console.log(longHand.test(varNames)); //RETORNA true
console.log(shortHand.test(varNames)); //RETORNA true
```

---

### Encontrando tudo que não seja números e letras

Para encontrarmos todos os caracteres que não sejam letras ou números, podemos representar: `/[^A-Za-z0-9_]/`. No entanto, também existe uma forma prática de escrever esse padrão utilizando: `/\W/`.

Na prática:

```jsx
let shortHand = /\W/;
let percentage = "42%";
let myString = "Codandoooo!";
percentage.match(shortHand); //RETORNA %
myString.match(shortHand); //RETORNA !
```

---

### Encontrando todos os números

Conforme vimos anteriormente, podemos construir expressões regulares que encontram números usando: `[0-9]`  porém, também existe um shortHand para esses casos, que é representado por: `/\d/` . Na prática:

```jsx
let myStr = 'Aqui podemos encontrar o ano de 2021'
let myRegex = /\d/g;
let result = myStr.match(myRegex);
console.log(result); // RETORNA [ '2', '0', '2', '1' ]
```

Se combinarmos o operador `+` temos o seguinte resultado:

```jsx
let myStr = 'Aqui podemos encontrar o ano de 2021'
let myRegex = /\d+/g;
let result = myStr.match(myRegex);
console.log(result); // RETORNA [ '2021' ]
```

---

### Encontrando tudo que não seja números

Assim como no caso do shortHand `/\w/`, temos um shortHand contrário para ignorar todos os números, seguindo a mesma lógica:  `/\D/` que representa `/[^0-9]/`.

Na prática:

```jsx
let myStr = 'Aqui podemos encontrar o ano de 2021'
let myRegex = /\D/g;
let result = myStr.match(myRegex);
console.log(result); 
/*
RETORNA

[
  'A', 'q', 'u', 'i', ' ', 'p',
  'o', 'd', 'e', 'm', 'o', 's',
  ' ', 'e', 'n', 'c', 'o', 'n',
  't', 'r', 'a', 'r', ' ', 'o',
  ' ', 'a', 'n', 'o', ' ', 'd',
  'e', ' '
] 
*/
```

---

### Desafio:

Crie uma regex que verifica o nome de usuário (*username*) em uma base de dados. Os nomes dos usuários devem seguir as seguintes restrições:

1. Os usernames podem conter somente caracteres alfa-numéricos
2. Os usernames não podem iniciar com números. Os números devem estar somente ao final do username e podem ser seguidos por zero ou mais números
3. As letras no nome do usuário podem ser minúsculas e maiúsculas
4. Os usernames devem possuir pelo menos dois caracteres, sendo que, quando for dois não podem ser números. 

**RESOLVENDO:**

1. ^[a-z] ⇒ A string deve iniciar com letras
2. [a-z]+ ⇒ Pode conter zero ou mais letras a partir do primeiro caractere
3. \d*$ ⇒ Pode conter zero ou mais números ao final da string
4. | ⇒ ou
5. ^[a-z] ⇒ A string deve iniciar com letras
6. \d\d+$ ⇒ Após a primeira letra, pode conter números, sendo seguidos por zero ou mais números ao final da string
7. gi ⇒ Flags: global e ignorecase

**NO CÓDIGO:**

```jsx
let username = 'userName123';
let userRegex = /^[a-z][a-z]+\d*$|^[a-z]\d\d+$/gi;
let result = userRegex.test(username );
console.log(result); //RETORNA true
```

---

### Encontrando espaços em branco:

Até agora vimos somente como encontrar números, letras e símbolos nas strings. Porém, também podemos encontrar espaços em branco ao decorrer de uma string. Para isso, podemos usar: `/\s/` 

Esse padrão não encontra somente espaços em branco, mas também encontra caracteres de *returns*, *tab*, *form feed* e *new line.* Parecido com a classe:`[ \r\t\f\n\v]`

Na prática:

```jsx
let myWhiteSpace = "Espaço em branco, espaços em branco."
let myRegex = /\s/g;
let result = myWhiteSpace.match(myRegex);
console.log(result); // RETORNA [ " ", " ", " ", " ", " ",]
```

---

### Encontrando tudo que não seja espaço em branco

Como já vimos, os operadores curtos (*shortHands*) possuem formas contrárias de serem escritos. No caso, quando não queremos dar *match* em espaços em branco, podemos usar: `/\S/` 

```jsx
let myWhiteSpace = "Espaço em branco, espaços em branco."
let myRegex = /\S/g;
let result = myWhiteSpace.match(myRegex);
console.log(result); 
/* RETORNA:
[
  'E', 's', 'p', 'a', 'ç', 'o',
  'e', 'm', 'b', 'r', 'a', 'n',
  'c', 'o', ',', 'e', 's', 'p',
  'a', 'ç', 'o', 's', 'e', 'm',
  'b', 'r', 'a', 'n', 'c', 'o',
  '.'
]
*/
```

---

### Especificando limites em um padrão ( { } )

Por exemplo, para encontrar somente a letra "a" que esteja aparecendo  de 3 a 5 vezes na string "ah":

```jsx
let firstString = "aaaaaaah";
let secondString = "aah";
let multipleA = /a{3,5}h/g;
multilpleA.test(firstString) //RETORNA true
multipleA.test(secondString) //RETORNA false
```

Caso queiramos especificar somente o menor número do limite, como em casos que não queremos delimitar um valor máximo para o range, podemos usar : 

```jsx
let A4 = "haaaah";
let A2 = "haah";
let A100 = "h" + "a".repeat(100) + "h";
let multipleA = /ha{3,}h/;
multipleA.test(A4); //RETORNA true
multipleA.test(A2); //RETORNA false
multipleA.test(A100); //RETORNA true
```

---

### Especificando um número exato de matches

Da mesma forma que podemos definir um range, ou até mesmo um limite inferior de matches que queremos identificar, podemos passar uma quantidade exata usando o mesmo padrão anterior. 

**Na prática:** Suponhamos que queremos encontrar apenas a palavra `hah` com a letra `a` repetindo 3 vezes:

```jsx
let A4 = "haaaah";
let A3 = "haaah";
let A100 = "h" + "a".repeat(100) + "h";
let multipleHA = /ha{3}h/;
multipleHA.test(A4); // RETORNA false
multipleHA.test(A3); // RETORNA true
multipleHA.test(A100); // RETORNA false
```

---

### Procurando caracteres que possam ou não existir ( ? )

Em alguns casos, podemos querer procurar um determinado padrão que possa ou não existir. Nesses casos, usamos o operador  `?`  para determinar se o caractere anterior existe ou não no padrão a ser buscado.

Um exemplo fácil para assimilar essa situação é no caso das diferentes formas de escrever uma mesma palavra em determinadas linguas. Por exemplo a palavra "cor*"* possui diferente escrita entre o inglês americano e o britânico. Veja, na prática, como encontrar essa palavra para ambos os casos:

```jsx
let american = "color";
let british = "colour";
let myRegex = /colou?r/;
myRegex.test(american); // RETORNA true
myRegex.test(british); // RETORNA true
```

---

### Lookaheads positivos e negativos

*Lookaheads* são padroes que dizem ao JavaScript (nesse caso) para "olhar adiante" na nossa string para checar se existem padrões a serem identificados em seu decorrer. Isso pode ser bem útil quando nós queremos procurar por múltiplos padrões em uma mesma string.

Existem dois tipos de *lookaheads*: positivos e negativos

- Positivos:

O *lookhead* positivo irá olhar uma string para ter certeza se o elemento no padrão a ser buscado realmente existe na string, mas não irá dar um *mach* com o elemento buscado. O *lookahead* positivo é usado como `(?=...)`, onde `...` é o elemento buscado que não terá sido "encontrado"

- Negativos:

O *Lookahead* negativo irá olhar para uma string para ter certeza que o elemento buscado de fato não existe ao longo da string. Esse *lookahead* é representado por `(?!...)`. Nesse caso, a regex retorna o "resto" do padrão, se o elemento passado ao *lookahead* não for encontrado.

Vendo na prática:

```jsx
let quit = "qu";
let noquit = "qt";
let quRegex= /q(?=u)/;
let qRegex = /q(?!u)/;
quit.match(quRegex); //RETORNA [ "q" ]
noquit.match(qRegex); //RETORNA [ "q" ]
```

**Em outro exemplo:** Checando dois ou mais padrões em uma única string. Suponha uma regex que verifica se uma senha possui de 3 a 6 caracteres, sendo que pelo menos um deles seja um número:

```jsx
let password = "abc123";
let checkPass = /(?=\w{3,6})(?=\D*\d)/;
checkPass.test(password); //RETORNA true
```

---

### Desafio 2

Construa uma regex que encontre senhas maiores que 5 dígitos e tenham 2 números consecutivos:

**RESPOSTA:**

```jsx
let password = "astronaut";
let passRegex = /(?=\w{6,})(?=\w*\d{2})/g;
let result = pasRegex.test(password) // RETORNA false
```

---

### Encontrando grupos mistos de caracteres

Algumas vezes queremos encontrar grupos de caracteres usando as regex. Para estes casos, podemos utilizar especificamente os parenteses `( )`

Por exemplo, caso quiser encontrar em uma string a palavra "penguin" ou "pumpkin", podemos construir o seguinte padrão: `/p(engu)|(umpk)in/g` .

Na prática:

```jsx
let myString = "Eleanor Roosevelt";
let myRegex = /(Franklin|Eleanor).*Roosevelt/;
let result = myRegex.test(myString); // RETORNA true
```

---

### Reusando padrões  usando Capture Groups

Imagine um caso em que tenhamos uma string que contém palavras repetidas e queremos retornar essas palavras repetidas de maneira fácil. 

Para fazer isso usamos o padrão que quisermos encontrar dentro dos parenteses e acessamos o padrão em uma "variável" criada automaticamente, representada pelo número do grupo criado. Como nesse caso foi criado apenas um grupo (contendo a palavra row, que é representado por (\w+)) acessamos essa variável através de \1.

```jsx
let strRepetida = 'row row row your boat';
let repeatRegex = /(\w+) \1 \1/;
repeatRegex.test(repeatStr); // Returns true
repeatStr.match(repeatRegex); // Returns ["row row row", "row"]
```

---

### Usando Capture Groups para procurar e substituir

Procurar por meio das regex é fantástico, porém, ainda mais poderoso é poder localizar padrões e substituí-los quando necessário.

Nos podemos procurar e trocar um texto em uma string, utilizando o método *`replace()`* em uma string.

Esse método aceita dois parâmetros, sendo que o primeiro é a regex que desejamos procurar e o segundo parâmetro é a string que desejamos substituir ou uma callback function que especifica algo.

```jsx
let wrongText = "The sky is silver.";
let silverRegex = /silver/;
wrongText.replace(silverRegex, "blue");
```

Nós também podemos chamar os *capture groups* com um sinal de $ antes do número que representa grupo:

```jsx
let str = "one two three";
let fixRegex = /(\w+)\s(\w+)\s(\w+)/; 
let replaceText = "$3 $2 $1"; 
let result = str.replace(fixRegex, replaceText); // RETORNA "three two one"
```

---

### Desafio 3

Remova os espaços em branco no início e no final de uma string utilizando regex e o método replace:

```jsx
let myStr = " Hello, World! ";
let myRegex = /^s+|\s+$/g;
let result = myStr.replace(myRegex, ""); // RETORNA 'Hello, World!'
```

---

### Finalizando

Dessa forma finalizamos os estudos iniciais em regex, com base no conteúdo disponibilizado, gratuitamente, pelo site FreeCodeCamp (acesse pelo link das referências).

Esses foram os principais métodos estudados durante o curso de Expressões Regulares do FreeCodeCamp, o qual pode ser acessado no link deixado nas referências.

Os próximos passos consiste em treino, treino e muito treino.

---

### REFERÊNCIAS:

Learn Regular Expressions - FreeCodeCamp. Disponível em: [https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/)

RegExr: Learn, Build, & Test RegEx. Disponível em: [https://regexr.com/](https://regexr.com/)