Tutorial 03: Tabelas
================

### Sobre este tutorial

Aqui você aprenderá sobre o tipo de objeto mais comum no R: *data
frames* (tabelas). 
Para iniciar esse tutorial você precisará antes ter instalado o pacote `tidyverse` como
indicado no primeiro tutorial de todos.

### O básico

Para criar uma tabela no R, precisamos de apenas uma função
`data.frame()`. Com ela, podemos passar a estrutura das suas colunas e
receber de volta um objeto com o qual é bastante simples trabalhar.

``` r
alunos <- data.frame(
  id = c(1, 2, 3, 4, 5, 6),
  nome = c("Ana", "Bia", "Caio", "Denise", "Edu", "Fábio"),
  idade = c(21, 22, 22, 24, 20, 21))

alunos
```

    #>   id   nome idade
    #> 1  1    Ana    21
    #> 2  2    Bia    22
    #> 3  3   Caio    22
    #> 4  4 Denise    24
    #> 5  5    Edu    20
    #> 6  6  Fábio    21

Obs.: Existe uma diferença entre o “`=`” e o “`<-`”. Por enquanto não
precisa se preocupar com os detalhes, lembre-se apenas que usamos o
“`<-`” para criar novos objetos e o “`=`” para dizer qual nome
corresponde a quais valores dentro de uma função. Acima, a função
`data.frame()` recebe uma série de vetores, cujos nomes serão as
colunas.

Obs. 2: Como cada coluna da tabela é muito grande, usamos o **Enter**
para quebrar a chamada da função em múltiplas linhas\! Não há nada de
diferente entre `data.frame()` e `mean()` por exemplo.

Observe com atenção como o objeto `alunos` é exibido: primeiramente
temos uma coluna “fantasma” com o número das linhas e depois vemos as
colunas exatamente da forma como as descrevemos (a coluna `nome` não tem
aspas mesmo, não se preocupe).

### Uma forma melhor

A função `data.frame()` é apresentada acima, pois ela é extremamente
comum em códigos de R mais antigos; mas veja o que acontece quando
tentamos exibir no console uma tabela um pouco
    maior.

``` r
mtcars
```

    #>                      mpg cyl  disp  hp drat    wt  qsec vs am gear carb
    #> Mazda RX4           21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4
    #> Mazda RX4 Wag       21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4
    #> Datsun 710          22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1
    #> Hornet 4 Drive      21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1
    #> Hornet Sportabout   18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2
    #> Valiant             18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1
    #> Duster 360          14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4
    #> Merc 240D           24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2
    #> Merc 230            22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2
    #> Merc 280            19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4
    #> Merc 280C           17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4
    #> Merc 450SE          16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3
    #> Merc 450SL          17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3
    #> Merc 450SLC         15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3
    #> Cadillac Fleetwood  10.4   8 472.0 205 2.93 5.250 17.98  0  0    3    4
    #> Lincoln Continental 10.4   8 460.0 215 3.00 5.424 17.82  0  0    3    4
    #> Chrysler Imperial   14.7   8 440.0 230 3.23 5.345 17.42  0  0    3    4
    #> Fiat 128            32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
    #> Honda Civic         30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
    #> Toyota Corolla      33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1
    #> Toyota Corona       21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1
    #> Dodge Challenger    15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2
    #> AMC Javelin         15.2   8 304.0 150 3.15 3.435 17.30  0  0    3    2
    #> Camaro Z28          13.3   8 350.0 245 3.73 3.840 15.41  0  0    3    4
    #> Pontiac Firebird    19.2   8 400.0 175 3.08 3.845 17.05  0  0    3    2
    #> Fiat X1-9           27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1
    #> Porsche 914-2       26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2
    #> Lotus Europa        30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
    #> Ford Pantera L      15.8   8 351.0 264 4.22 3.170 14.50  0  1    5    4
    #> Ferrari Dino        19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6
    #> Maserati Bora       15.0   8 301.0 335 3.54 3.570 14.60  0  1    5    8
    #> Volvo 142E          21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2

O objeto `mtcars` já vem embutido no R, por isso você não precisa
criá-lo. Perceba que todas as linhas são exibidas, de forma que fica
difícil se orientar dentro da tabela\! Isso pode ser um problema se a sua tabela for muito comprida ou muito larga, tornando a
visualização do objeto completamente impossível.

Por isso usamos uma alternativa proveniente do `tidyverse`. Essa
biblioteca não passar de um conjunto (imenso) de funções extremamente
otimizadas e simplificadas que tornam a tarefa de programar em R algo
muito mais simples. Para disponibilizar as funções do `tidyverse` na sua
sessão, basta rodar o comando abaixo (e não se preocupe com todas as
mensagens que
    aparecerem).

``` r
library(tidyverse)
```

    #> ── Attaching packages ────────────────────────────────────────────── tidyverse 1.2.1 ──

    #> ✔ ggplot2 3.0.0     ✔ purrr   0.2.5
    #> ✔ tibble  1.4.2     ✔ dplyr   0.7.6
    #> ✔ tidyr   0.8.1     ✔ stringr 1.3.1
    #> ✔ readr   1.1.1     ✔ forcats 0.3.0

    #> ── Conflicts ───────────────────────────────────────────────── tidyverse_conflicts() ──
    #> ✖ dplyr::filter() masks stats::filter()
    #> ✖ dplyr::lag()    masks stats::lag()

No `tidyverse` a função utilizada para criar tabelas é a `tibble()`.
Além disso também podemos converter tabelas do formato antigo para o
formato novo com `as_tibble()` (“como tibble” em inglês).

Obs.: A palavra “tibble” não tem significado nenhum em inglês\! Na
verdade ela é proveniente da forma como um anglófono pronunciaria “tbl”,
a abreviação de “*table*” (“tabela”).

``` r
as_tibble(mtcars)
```

    #> # A tibble: 32 x 11
    #>      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
    #>  * <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    #>  1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
    #>  2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
    #>  3  22.8     4  108     93  3.85  2.32  18.6     1     1     4     1
    #>  4  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
    #>  5  18.7     8  360    175  3.15  3.44  17.0     0     0     3     2
    #>  6  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
    #>  7  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
    #>  8  24.4     4  147.    62  3.69  3.19  20       1     0     4     2
    #>  9  22.8     4  141.    95  3.92  3.15  22.9     1     0     4     2
    #> 10  19.2     6  168.   123  3.92  3.44  18.3     1     0     4     4
    #> # ... with 22 more rows

Veja como agora temos a tabela apresentada de uma forma muito mais
interessante\! A primeira linha da saída mostra o formato da tabela (32
linhas e 11 colunas); a segunda linha mostra os nomes das colunas; a
terceira contém abreviações dos tipos das colunas (mais sobre isso
adiante); a partir daí temos as primeiras 10 linhas da tabela e, no fim,
quantas linhas foram omitidas (22 nesse caso). Se a tabela tivesse
colunas demais, nas últimas linhas também apareceriam os nomes das
colunas omitidas.

Obs.: Se você quiser ver a tabela completa, isso ainda é possível com o
comando `View(mtcars)`. Não é possível demonstrar esse comando no
tutorial porque ele depende do RStudio.

Veja agora como criar a tabela `alunos` com `tibble()`:

``` r
alunos <- tibble(
  id = c(1, 2, 3, 4, 5, 6),
  nome = c("Ana", "Bia", "Caio", "Denise", "Edu", "Fábio"),
  idade = c(21, 22, 22, 24, 20, 21))

alunos
```

    #> # A tibble: 6 x 3
    #>      id nome   idade
    #>   <dbl> <chr>  <dbl>
    #> 1     1 Ana       21
    #> 2     2 Bia       22
    #> 3     3 Caio      22
    #> 4     4 Denise    24
    #> 5     5 Edu       20
    #> 6     6 Fábio     21

Exatamente da mesma forma\! Basta trocar o nome da função `data.frame()`
por `tibble()`. Mas agora preste atenção na terceira linha da saída; ela
representa o tipo daquela coluna e geralmente assume um dos seguintes
valores:

  - `<dbl>`: Números reais (abreviação de “*double*”), o padrão de
    qualquer número do R.

  - `<int>`: Números inteiros, criados com a letra “L” como em `12L`.

  - `<chr>`: Textos (abreviação de “*character*”).

  - `<lgl>`: Valores lógicos, retornados por verificações como as
    apresentadas no tutorial passado.

  - `<fct>`: Fatores ou variáveis categóricas (abreviação de *factors*),
    abordadas nos tutoriais de gráficos.

  - `<dttm>`: Data-horas (abreviação de “*date time*”), um tipo um pouco
    mais complexo de se lidar.

Estes não são os únicos tipos possíveis, mas são os mais comuns.

### Funcionalidades

Você já deve imaginar que, dado o suporte do R para tabelas, ele também
suportaria operações nestas tabelas. A operação mais simples que você
pode fazer em uma tabela é extrair os valores de uma coluna.

``` r
alunos$nome
```

    #> [1] "Ana"    "Bia"    "Caio"   "Denise" "Edu"    "Fábio"

Obs.: Digite o comando acima letra por letra, não apenas copie e cole.
Quando você digitar o cifrão, você perceberá que o RStudio já te dá os
nomes de todas as colunas\! Você pode escolher um deles com as setas do
teclado e usando a tecla **Tab**.

Extraindo uma coluna, é possível usar qualquer outra função do R como se
você estivesse trabalhando com um vetor. Abaixo tiramos a média das
idades dos alunos.


``` r
# Média da idade dos alunos
mean(alunos$idade)
```

    #> [1] 21.66667

Obs.: Lembre-se que linhas que começam com “\#” são comentários\! O R
não faz nada com elas, sendo apenas uma anotação no meio do código para
que você se lembre o que aquilo faz.

Outra função interessante para usar com tabelas é `summary()`
(“resumo”), que retorna as medidas resumo daquela coluna.

``` r
summary(alunos$idade)
```

    #>    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    #>   20.00   21.00   21.50   21.67   22.00   24.00

Da esquerda para a direita, você pode ver o mínimo, o primeiro quartil,
a mediana, a média, o terceiro quartil e o máximo.

Por fim, caso você tenha uma tabela muito comprida, vale a pena usar a
função `glimpse()` (“espiar”) porque ela exibe tomba a tabela e exibe
principalmente os nomes e tipos de cada coluna.

``` r
glimpse(alunos)
```

    #> Observations: 6
    #> Variables: 3
    #> $ id    <dbl> 1, 2, 3, 4, 5, 6
    #> $ nome  <chr> "Ana", "Bia", "Caio", "Denise", "Edu", "Fábio"
    #> $ idade <dbl> 21, 22, 22, 24, 20, 21
