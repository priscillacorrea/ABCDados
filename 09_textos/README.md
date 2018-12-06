Tutorial 09: Textos
================

### Sobre este tutorial

Neste tutorial você aprenderá algumas funções úteis para trabalhar com
textos. Esse tipo de conhecimento é útil porque pode te ajudar a criar
filtros mais interessantes ou mesmo a tratar colunas que tenham
problemas de preenchimento.

Mais uma vez será utilizada a tabela `turmas` do tutorial 7, assim não
se esqueça de carregá-la em sua sessão do R antes de começar os
exercícios deste tutorial.

### Detecção

A operação mais simples de se realizar em variáveis de texto é a
detecção de um padrão. Depois de carregar o `tidyverse` você terá
acesso a um conjunto de funções dedicadas exclusivamente ao tratamento
de textos, todas começando com `str_`; para detectar padrões, você
utilizará `str_detect()`.

``` r
library(tidyverse)

# Três textos para exemplificar as fuções deste tutorial
textos <- c("01-Feminino", "02-Masculino", "03-Indefinido")

str_detect(textos, "ino")
```

    #> [1]  TRUE  TRUE FALSE

Perceba que `str_detect()` retornou `TRUE` (“verdadeiro”) nos textos que
contém a sequência “ino” e `FALSE` (“falso”) para o texto que não a
contém.

É importante entender também que a sequência deve diferenciar letras
maiúsculas de minúsculas\! Teste os comandos abaixo para notar a
diferença entre seus dois resultados.

``` r
# Detectando M maiúsculo
str_detect(textos, "M")

# Detectando M minúsculo
str_detect(textos, "m")
```

Uma grande utilidade da detecção de textos é junto com a função
`filter()`. Veja por exemplo como `str_detect()` é utilizada para
selecionar todas as linhas de `turmas` em que `DISTRITO` contém a
palavra “VILA”:

``` r
turmas %>%
  filter(str_detect(DISTRITO, "VILA")) %>%
  select(DISTRITO)
```

    #> # A tibble: 7,274 x 1
    #>    DISTRITO  
    #>    <chr>     
    #>  1 VILA SONIA
    #>  2 VILA SONIA
    #>  3 VILA SONIA
    #>  4 VILA SONIA
    #>  5 VILA SONIA
    #>  6 VILA SONIA
    #>  7 VILA SONIA
    #>  8 VILA SONIA
    #>  9 VILA SONIA
    #> 10 VILA SONIA
    #> # ... with 7,264 more rows

Se você inspecionar a tabela resultante, ficará evidente que sobraram
somente as linhas nas quais `DISTRITO` é igual a “VILA SONIA”, “VILA
ANDRADE”, “VILA MARIANA”, “VILA PRUDENTE” e assim por diante:

``` r
turmas %>%
  filter(str_detect(DISTRITO, "VILA")) %>%
  distinct(DISTRITO)
```

    #> # A tibble: 12 x 1
    #>    DISTRITO       
    #>    <chr>          
    #>  1 VILA SONIA     
    #>  2 VILA ANDRADE   
    #>  3 VILA MARIANA   
    #>  4 VILA PRUDENTE  
    #>  5 VILA FORMOSA   
    #>  6 VILA MARIA     
    #>  7 VILA GUILHERME 
    #>  8 VILA MEDEIROS  
    #>  9 VILA CURUCA    
    #> 10 VILA JACUI     
    #> 11 VILA MATILDE   
    #> 12 VILA LEOPOLDINA

Obs.: A função `distinct()` (“distinto”) retorna uma linha para cada
valor diferente que aparece naquela coluna.

### Uniformização

Se você precisar uniformizar um texto, você pode utilizar as funções
`str_to_lower()` (“txt para minúscula”) e `str_to_upper()` (“txt para
maiúscula”). Com elas é possível uniformizar tanto uma variável quanto
uma coluna de uma tabela.

``` r
str_to_upper(textos)
```

    #> [1] "01-FEMININO"   "02-MASCULINO"  "03-INDEFINIDO"

``` r
turmas %>%
  mutate(distrito = str_to_lower(DISTRITO)) %>%
  distinct(distrito)
```

    #> # A tibble: 96 x 1
    #>    distrito         
    #>    <chr>            
    #>  1 vila sonia       
    #>  2 raposo tavares   
    #>  3 rio pequeno      
    #>  4 butanta          
    #>  5 itaim bibi       
    #>  6 pinheiros        
    #>  7 jardim paulista  
    #>  8 morumbi          
    #>  9 alto de pinheiros
    #> 10 capao redondo    
    #> # ... with 86 more rows

Esse tipo de transformação pode, por exemplo, simplificar uma tarefa de
filtragem.

### Substituição

Se for necessário fazer substituições em textos, a função mais genérica
é `str_replace()` (“txt substituir”). Ela encontra a primeira
ocorrência do padrão desejado e a substitui por outro padrão.

``` r
str_replace(textos, "i", "X")
```

    #> [1] "01-FemXnino"   "02-MasculXno"  "03-IndefXnido"

Se você quiser substituir todas as ocorrências de um padrão basta
utilizar a variante `str_replace_all()` (“txt substituir todos”):

``` r
str_replace_all(textos, "i", "X")
```

    #> [1] "01-FemXnXno"   "02-MasculXno"  "03-IndefXnXdo"

Veja um exemplo abaixo de como esta função pode ser utilizada em
parceria com um `filter()` e um `mutate()`:

``` r
turmas %>%
  filter(str_detect(DISTRITO, "VILA")) %>%
  mutate(DISTRITO = str_replace(DISTRITO, "VILA", "V.")) %>%
  distinct(DISTRITO)
```

    #> # A tibble: 12 x 1
    #>    DISTRITO     
    #>    <chr>        
    #>  1 V. SONIA     
    #>  2 V. ANDRADE   
    #>  3 V. MARIANA   
    #>  4 V. PRUDENTE  
    #>  5 V. FORMOSA   
    #>  6 V. MARIA     
    #>  7 V. GUILHERME 
    #>  8 V. MEDEIROS  
    #>  9 V. CURUCA    
    #> 10 V. JACUI     
    #> 11 V. MATILDE   
    #> 12 V. LEOPOLDINA

Outra função útil para substituições é `str_remove()` (“txt remover”),
juntamente com a sua variante `str_remove_all()` (“txt remover todos”).
Ao invés de substituir um padrão por outro, estas funções removem
completamente um padrão.

``` r
str_remove(textos, "0")
```

    #> [1] "1-Feminino"   "2-Masculino"  "3-Indefinido"

### Expressões regulares

De acordo com a
[Wikipédia](https://pt.wikipedia.org/wiki/Express%C3%A3o_regular), uma
expressão regular

> \[…\] provê uma forma concisa e flexível de identificar cadeias de
> caracteres de interesse, como caracteres particulares, palavras ou
> padrões de caracteres.

Todas as funções para lidar com textos vistas até agora aceitam
expressões regulares (mais comumente chamadas de *regex* por causa do
termo em inglês “*regular expression*”). Quando você descreve uma
sequência ou padrão para ser identificado e/ou substituído, você
poderia na verdade passar outros caracteres especiais que caracterizam
expressões regulares.

Os caracteres `.`, `^` e `$` casam respectivamente com qualquer
caractere, o início de um texto e o final de um texto.

``` r
str_detect(textos, "i.o")
```

    #> [1] TRUE TRUE TRUE

O *regex* acima retorna `TRUE` para todas as palavras porque ele está
procurando por três letras onde a primeira é um “i” e a última é um “o”;
as duas primeiras palavras têm “ino” e a última tem “ido”.

``` r
str_detect(textos, "^M")
```

    #> [1] FALSE FALSE FALSE

``` r
str_detect(textos, "o$")
```

    #> [1] TRUE TRUE TRUE

O primeiro comando acima retorna `FALSE` para todas as palavras porque
nenhuma começa com “M” (todas começam com “0”), já o segundo comando
retorna `TRUE` para todas porque as três terminam com “o”.

Obs.: Caso você queira detectar um ponto-final, não é possível
simplesmente utilizar o “.” porque ele já tem um significado específico
como você acabou de ver\! Estes caracteres especiais do *regex* só podem
ser detectados se você utilizar duas barras oblíquas para a esquerda
antes deles: “\\\\.” e “\\\\$” por exemplo.

Outra funcionalidade do *regex* é permitir que você defina conjuntos de
padrões. Esse tipo de estrutura permite que uma mesma expressão regular
case com múltiplas sequências diferentes pré-determinadas:

``` r
str_replace_all(textos, "[mn]i", "X")
```

    #> [1] "01-FeXXno"    "02-Masculino" "03-IndefiXdo"

Este comando detecta os padrões “mi” e “ni”, os substituindo por “X”. Os
colchetes indicam que qualquer uma das letras dentro deles pode ser
detectada independentemente.

Expressões regulares são um assunto extremamente complexo e praticamente
inesgotável, sendo portanto impossível abordá-lo nestes tutoriais
introdutórios. Neste
[link](http://www.gagolewski.com/software/stringi/manual/?manpage=stringi-search-regex)
(em inglês) é possível encontrar uma documentação sobre todos os
tipos de padrão que podem ser utilizados com as funções do R.
