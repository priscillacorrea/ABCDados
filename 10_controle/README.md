Tutorial 10: Controle
================

### Sobre este tutorial

Neste tutorial você aprenderá um tópico extremamente importante tanto
para o R como para qualquer outra linguagem de programação. O principal
conceito abordado será o que chamamos de “controle de fluxo”, mas
tangencialmente também serão apresentados operadores lógicos.

### Se/senão

Lembrando o que foi tratado nos tutoriais anteriores, você pode estar se
perguntando como fazer programas mais complexos. Até agora, você
essencialmente só foi apresentado a funções, variáveis e *pipelines*,
mas por enquanto o seu programa não passa de uma sequência linear de
comandos que o computador executa um a um. É verdade que com funções
podemos reutilizar algum código várias vezes sem reescrevê-lo,
entretanto isso não faz com que o programa em si deixe de ser
sequencial.

Uma ferramenta que você encontrará em toda linguagem de programação é a
dupla “se-senão” (em inglês “*if-else*”). Com essas palavras-chave, você
pode fazer com que o programa execute uma certa seção de código somente
se uma condição for atendida.

Abaixo você pode ver um exemplo muito simples do que seria um comando
com estes condicionais:

``` r
numero <- -10

if (numero > 0) {
  print("O número é positivo")
} else {
  print("O número é negativo")
}
```

    #> [1] "O número é negativo"

Como você já deve estar percebendo, a estrutura de um if-else é muito
semelhante à forma como usamos essas palavras no dia-a-dia: **se** uma
**condição** for atendida, fazer uma coisa, **senão**, fazer outra
coisa. No caso acima, a condição a ser atendida é o valor de `numero`
ser maior que zero.

Obs.: A função `print()` (“imprimir” em inglês) faz apenas o que o seu
nome indica: ela exibe um texto no Console.

Agora vejamos um exemplo um pouco mais complexo:

``` r
eh_par <- function(x) {
  
  if (x %% 2 == 0) {
    print("O número é par!")
  } else {
    print("O número é ímpar.")
  }

}

eh_par(2)
```

    #> [1] "O número é par!"

No código acima foi criada uma função que imprime no Console uma
mensagem se o número de entrada for par e outra mensagem se o número for
ímpar. Perceba quão complexa é a condição dessa vez; ela está testando
se o resto da divisão de `x` por 2 (`x %% 2`) é igual a 0 (`== 0`).
Teste se `eh_par()` funciona quando você passa para ela um número
ímpar\!

### Várias condições

Uma funcionalidade muito conveniente do if-else é a possibilidade de
fazer várias verificações em seguida. O comando abaixo pode ser lido da
seguinte maneira: **se** `numero` for maior que 0, então o número é
positivo; se `numero` não for maior que 0 mas for menor que 0, então o
número é `negativo`; se `numero` não for maior que 0 nem menor que 0,
então ele é 0.

``` r
numero <- -10

if (numero > 0) {
  print("O número é positivo")
} else if (numero < 0) {
  print("O número é negativo")
} else {
  print("O número é zero")
}
```

    #> [1] "O número é negativo"

Teste o if-else acima com outros números para ver quais são as saídas\!
O código pode parecer um pouco apertado, mas no RStudio todas as
palavras-chave ficam em destaque, então basta lembrar de passar
condições entre parênteses para todo `if` e todo `else if`.

Assim como em funções, os if-else possuem chaves para que seja possível
executar mais de um comando dentro de cada corpo. Além disso, é
perfeitamente possível ter apenas um `if` sozinho (já que nem sempre é
necessário fazer algo no “senão”).

``` r
valor_absoluto <- function(x) {
  
  if (x < 0) {
    print("O número foi convertido!")
    x <- -1*x
  }
  
  return(x)
}

valor_absoluto(-10)
```

    #> [1] "O número foi convertido!"

    #> [1] 10

Obs.: O comando `return()` (“retorno” em inglês) serve apenas para
deixar explícito qual deve ser o resultado de uma função. Quando o
último comando da sua função já retorna o resultado final, o `return()`
não é necessário; neste caso, não há um *último comando* por causa do
`if`.

Obs. 2: Perceba que essa função mostra duas saídas no Console\! Isso é
perfeitamente possível com o `print()`, mas é importante notar que
somente um valor pode ser retornado apesar de vários poderem ser
impressos.

### Operadores lógicos

Relembrando o tutorial de limpeza de dados, abaixo estão os operadores
lógicos mais comuns. Você pode utilizá-los dentro da `filter()` ou de
qualquer if-else.

| Operação      | Significado                                  |
| :------------ | :------------------------------------------- |
| x \< y        | x é menor que y?                             |
| x \> y        | x é maior que y?                             |
| x \>= y       | x é maior ou igual a y?                      |
| x \<= y       | x é menor ou igual a y?                      |
| x == y        | x é igual a y?                               |
| x \!= y       | x é diferente de y?                          |
| x %in% y      | x é um elemento de y?                        |
| is.na(x)      | x é vazio/omisso?                            |
| \!op1         | O contrário da operação 1 é verdadeiro?      |
| (op1) ｜ (op2) | A operação 1 ou a operação 2 é verdadeira?   |
| (op1) & (op2) | A operação 1 e a operação 2 são verdadeiras? |

Preste bastante atenção no teste de igualdade\! É necessário dois
símbolos de igual (`==`) para verificar se dois objetos são iguais.

### Enquanto

Um “enquanto” (também conhecido como *loop* ou *while* por causa dos
seus termos em inglês) é outra estrutura importante de qualquer
linguagem. Com ele podemos repetir um mesmo comando enquanto alguma
condição for atendida.

``` r
numero <- 0
vezes <- 6

while (vezes > 0) {
  numero <- numero + 5
  vezes <- vezes - 1
}

numero
```

    #> [1] 30

No comando acima, somamos 5 a `numero` enquanto `vezes` for maior que 0;
a cada soma, também subtraímos 1 de `vezes`. Em outras palavras,
implementamos um algoritmo para multiplicar 5 por 6\!

Também podemos usar loops para percorrer um vetor. Consulte o tutorial 2
caso você precise refrescar a sua memória, mas um vetor não passa de um
objeto que contém vários elementos dentro de si.

``` r
numeros <- 5:9
i <- 1

while (i <= length(numeros)) {
  numeros[i] <- i
  i <- i + 1
}

numeros
```

    #> [1] 1 2 3 4 5

Obs.: A sintaxe `x:y` não passa de um atalho para `c(x, x+1, x+2, ...,
y)`. No comando acima, `numeros` é declarado como `numeros <-
c(5, 6, 7, 8, 9)`.

Apesar de apresentar alguns elementos novos, este código é bastante
simples:

  - Declara-se um vetor que vai de 5 a 9 (`numeros`) e uma variável
    auxiliar `i`.

  - Executa-se uma série de comandos enquanto `i` for menor ou igual ao
    comprimento (`length()`) de `numeros`:
    
      - O `i`-ésimo elemento de `numeros` passa a valer `i` (a notação
        `vetor[indice]` serve para acessar elementos dentro de um
        vetor).
    
      - `i` passa a valer `i` mais 1.

  - Imprime-se `numeros` no console.

### Para

Esse padrão de repetir um código um certo número de vezes é extremamente
comum. Para evitar a necessidade da linha `i <- i + 1` usamos uma
abstração do `while` chamada `for` (“para” em inglês).

No `for`, você já será obrigado a declarar uma variável no meio da
própria condição\! Para ver como essa palavra-chave funciona, veja
primeiro o que faz a função `seq_along()` (cujo nome é abreviado da
expressão em inglês para “sequência ao longo de”):

``` r
numeros <- 5:9
seq_along(numeros)
```

    #> [1] 1 2 3 4 5

Essencialmente ela retorna o índice de cada elemento do objeto que ela
recebe (justamente os valores que `i` assumia no código anterior). Com o
`for` podemos usar essa função para já declarar todos os valores de `i`
de forma muito mais simples\!

``` r
numeros <- 5:9

for (i in seq_along(numeros)) {
  numeros[i] <- i
}

numeros
```

    #> [1] 1 2 3 4 5

Antes leríamos o comando com `while` da seguinte forma: “**enquanto**
`i` for menor ou igual a 5, executar os comandos a seguir”. Com o `for`
passamos a ler o comando assim: “**para** um `i` indo de 1 a 5, executar
os comandos a seguir”.
