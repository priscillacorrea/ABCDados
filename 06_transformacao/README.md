Tutorial 06: Transformação
================

### Sobre este tutorial

Tendo concluído o tutorial passado, o próximo passo que você deve dar é
transformar colunas. Transformação é um termo genérico utilizado para
descrever qualquer operação que crie novas colunas ou modifique o
significado de uma coluna já existente. Neste tutorial você aprenderá
sobre as funções `mutate()`, `group_by()`, `summarise()` e mais algumas.

Neste ponto assume-se que você já realizou o Tutorial 04 sobre
importação e tem no seu ambiente os objetos `dicionario` e `cadastro`,
pois aqui eles serão utilizados com frequência.

### Modificar colunas

Provavelmente a função que você mais utilizará quando estiver
programando em R se chama `mutate()` (“modificar”). Ela é extremamente
útil, pois permite alterar colunas já existentes e até criar colunas
novas com um só comando.

Assim como as funções que você viu no tutorial passado, a `mutate()`
recebe como primeiro argumento uma tabela e depois quantas expressões
você quiser. Entretanto, estas expressões precisam ter um formato um
tanto quanto específico: a primeira parte deve sempre ser o nome de uma
coluna (nova ou antiga), um símbolo de igualdade e, então, uma expressão
ou cálculo que retorne os valores da coluna especificada.

Antes de demonstrar o funcionamento desta função, abra `cadastro` com
`View()` e examine as coluna `LATITUDE` e `LONGITUDE`. Normalmente
latitudes e longitudes são valores pequenos e, para a cidade de São
Paulo, deveriam ser algo em torno de -23 para latitude e -46 para
longitude. Quando a tabela foi preenchida, não foi colocado o separador
da parte decimal\!

O comando abaixo usa `mutate()` para dividir latitudes e longitudes por
1000000 de modo que os valores fiquem corretos.

``` r
library(tidyverse)

mutate(cadastro, LATITUDE = LATITUDE/1000000, LONGITUDE = LONGITUDE/1000000)
```

    #> # A tibble: 6,878 x 53
    #>    DRE   CODESC TIPOESC NOMESC DIRETORIA SUBPREF CEU   ENDERECO NUMERO
    #>    <chr> <chr>  <chr>   <chr>  <chr>     <chr>   <chr> <chr>    <chr> 
    #>  1 G     000086 EMEI    PAULO… GUAIANAS… GUAIAN… <NA>  RUA FEL… 502   
    #>  2 FO    000094 EMEI    VICEN… FREGUESI… CASA V… <NA>  RUA DOU… 295   
    #>  3 MP    000108 EMEF    JOSE … SAO MIGU… SAO MI… <NA>  RUA SAO… 159   
    #>  4 BT    000191 EMEF    ALIPI… BUTANTA   BUTANTA <NA>  AVENIDA… 140   
    #>  5 PJ    000205 EMEBS   VERA … PIRITUBA  PIRITU… <NA>  RUA BEN… 206   
    #>  6 BT    000213 EMEI    ANTON… BUTANTA   BUTANTA <NA>  AVENIDA… 90    
    #>  7 FO    000221 EMEI    NAIR … FREGUESI… FREGUE… <NA>  RUA SAN… 51    
    #>  8 JT    000230 EMEI    MARIA… JACANA/T… VILA M… <NA>  RUA GAS… 340   
    #>  9 JT    000248 EMEI    WALFR… JACANA/T… JACANA… <NA>  RUA VIC… 200   
    #> 10 CL    000256 EMEI    WILMA… CAMPO LI… CAMPO … <NA>  RUA INT… 395   
    #> # ... with 6,868 more rows, and 44 more variables: BAIRRO <chr>,
    #> #   CEP <chr>, TEL1 <chr>, TEL2 <chr>, FAX <chr>, SITUACAO <chr>,
    #> #   CODDIST <chr>, DISTRITO <chr>, SETOR <chr>, CODINEP <int>,
    #> #   CODCIE <int>, EH <dbl>, DT_CRIACAO <chr>, ATO_CRIACAO <chr>,
    #> #   DOM_CRIACAO <chr>, DT_INI_FUNC <chr>, DT_AUTORIZA <chr>,
    #> #   NOME_ANT <chr>, T2D3D <chr>, T2D3D16 <chr>, T2D3D15 <chr>,
    #> #   T2D3D14 <chr>, T2D3D13 <chr>, T2D3D12 <chr>, T2D3D11 <chr>,
    #> #   T2D3D10 <chr>, T2D3D09 <chr>, T2D3D08 <chr>, T2D3D07 <chr>,
    #> #   DTURNOS <chr>, DTURNOS16 <chr>, DTURNOS15 <chr>, DTURNOS14 <chr>,
    #> #   DTURNOS13 <chr>, DTURNOS12 <chr>, DTURNOS11 <chr>, DTURNOS10 <chr>,
    #> #   DTURNOS09 <chr>, DTURNOS08 <chr>, DTURNOS07 <chr>, LATITUDE <dbl>,
    #> #   LONGITUDE <dbl>, REDE <chr>, DATABASE <chr>

Infelizmente, as colunas nas quais estamos interessados são umas das
últimas e portanto não aparecem na saída do comando. Não seria ótimo se
você pudesse aplicar um `select()` logo depois do `mutate()` para poder
ver somente as colunas que foram modificadas? No comando abaixo você
será apresentado ao operador mais famoso do R: o *pipe* (“cano”)\!

``` r
cadastro %>%
  mutate(LATITUDE = LATITUDE/1000000, LONGITUDE = LONGITUDE/1000000) %>%
  select(LATITUDE, LONGITUDE)
```

    #> # A tibble: 6,878 x 2
    #>    LATITUDE LONGITUDE
    #>       <dbl>     <dbl>
    #>  1    -23.6     -46.4
    #>  2    -23.5     -46.7
    #>  3    -23.5     -46.4
    #>  4    -23.6     -46.7
    #>  5    -23.5     -46.7
    #>  6    -23.6     -46.8
    #>  7    -23.5     -46.7
    #>  8    -23.5     -46.6
    #>  9    -23.4     -46.6
    #> 10    -23.7     -46.8
    #> # ... with 6,868 more rows

Para escrever o *pipe* com facilidade, tecle **Ctrl + Shift + M** no seu
teclado. O que este operador está fazendo facilita muito o seu
trabalho na hora de analisar dados, então lembre-se bem dele\!
Essencialmente, ele passa o que está à esquerda dele como entrada da
função que está na linha de baixo; no comando acima, portanto, passamos
`cadastro` como tabela para a `mutate()` e, então, a tabela resultante
desta transformação como entrada para a `select()`.

Este tipo de notação denominada *pipeline* (“encanamento”) é
extremamente útil porque permite transformar uma tarefa de tratamento de
dados em algo parecido com uma receita de bolo. Note que para executar o
*pipeline* inteiro basta colocar o cursor na primeira linha e teclar
**Ctrl + Enter** apenas uma vez.

Veja agora mais um exemplo de transformação com `mutate()`:

``` r
cadastro %>%
  mutate(CODDIST = as.numeric(CODDIST)) %>%
  select(CODDIST)
```

    #> # A tibble: 6,878 x 1
    #>    CODDIST
    #>      <dbl>
    #>  1      31
    #>  2      50
    #>  3      44
    #>  4      94
    #>  5      63
    #>  6      94
    #>  7      29
    #>  8      89
    #>  9      81
    #> 10      19
    #> # ... with 6,868 more rows

Antes da execução do comando acima, a coluna `CODDIST` era uma coluna de
texto, algo que nem sempre é apropriado para um código numérico. Com a
função `as.numeric()` (“como numérico”) este problema é resolvido. Agora
é inclusive possível usar a funcionalidade de calculadora do R para
fazer matemática com este código:

``` r
cadastro %>%
  mutate(CODDIST = as.numeric(CODDIST), NOVOCOD = (CODDIST+1)*2) %>%
  select(NOVOCOD)
```

    #> # A tibble: 6,878 x 1
    #>    NOVOCOD
    #>      <dbl>
    #>  1      64
    #>  2     102
    #>  3      90
    #>  4     190
    #>  5     128
    #>  6     190
    #>  7      60
    #>  8     180
    #>  9     164
    #> 10      40
    #> # ... with 6,868 more rows

O comando acima cria uma nova coluna (`NOVOCOD`) que é `CODDIST` mais 1
dividido por 2.

Se você rodar o comando `View(dicionario)` e ler a descrição da coluna
`T2D3D` você notará que seria muito melhor que seu valor fosse 2 ou 3 e
não “2D” ou “3D”. O comando abaixo usa a função `if_else()` (“se e
senão”) para transformar todo “2D” em 2 e o resto (“3D” no caso) em
3:

``` r
cadastro %>%
  mutate(T2D3D = if_else(T2D3D == "2D", 2, 3)) %>%
  select(T2D3D)
```

    #> # A tibble: 6,878 x 1
    #>    T2D3D
    #>    <dbl>
    #>  1     2
    #>  2     2
    #>  3     2
    #>  4     2
    #>  5     2
    #>  6     2
    #>  7     2
    #>  8     2
    #>  9     2
    #> 10     2
    #> # ... with 6,868 more rows

### Resumir colunas

Uma outra tarefa muito comum ao trabalhar com bases de dados, é
transformar uma coluna inteira em um valor. No SQL esse tipo de
transformação é feita com o `GROUPP BY`, mas no R geralmente são
necessárias duas funções: `group_by()` (“agrupar por”) e `summarise()`
(“resumir”).

Se você quiser extrair medidas resumo de uma coluna inteira, basta usar
`summarise()`. Ela recebe uma tabela e expressões que recebam uma lista
de valores mas retornem apenas um valor só (como média, mediana, soma,
etc.).

``` r
summarise(cadastro, MEDIALAT = mean(LATITUDE), MEDIALON = mean(LONGITUDE))
```

    #> # A tibble: 1 x 2
    #>   MEDIALAT MEDIALON
    #>      <dbl>    <dbl>
    #> 1       NA       NA

Perceba que o comando acima retornou uma nova tabela com uma linha só,
mas os valores desta linha são `NA` (omissos). Isso acontece porque o R
não sabe tirar a média de uma coluna que possua valores omissos (afinal,
quanto é `1 + NA`?). Para resolver isso, usamos o argumento `na.rm`
(“remover NA”) da função `mean()`; se colocarmos este argumento
valendo `TRUE` (“verdade”), então ela automaticamente removerá os
valores omissos antes de tirar a média.

``` r
# Lembre-se que quebrar as linhas não faz diferença
summarise(cadastro,
          MEDIALAT = mean(LATITUDE, na.rm = TRUE),
          MEDIALON = mean(LONGITUDE, na.rm = TRUE))
```

    #> # A tibble: 1 x 2
    #>     MEDIALAT   MEDIALON
    #>        <dbl>      <dbl>
    #> 1 -23573537. -46604085.

O mais comum, no entanto, é agrupar a tabela por uma ou mais colunas e
somente então extrair medidas resumo de outras colunas. O comando abaixo
agrupa a tabela por `DRE` e depois conta quantas escolas estão com
`SITUACAO` “Ativa”.

``` r
cadastro %>%
  group_by(DRE) %>%
  summarise(ATIVAS = sum(SITUACAO == "Ativa"))
```

    #> # A tibble: 14 x 2
    #>    DRE   ATIVAS
    #>    <chr>  <int>
    #>  1 BT       361
    #>  2 CL       603
    #>  3 CS       336
    #>  4 FO       383
    #>  5 G        417
    #>  6 IP       503
    #>  7 IQ       395
    #>  8 JT       322
    #>  9 MP       445
    #> 10 PE       479
    #> 11 PJ       491
    #> 12 SA       361
    #> 13 SM       360
    #> 14 <NA>    1250

### Uma análise completa

Suponha que você recebeu uma demanda: contar o número de escolas ativas
nos DREs “FO”, “IQ” e “SA” e determinar quantos porcento das escolas de
cada DRE este número representa. Depois de criada uma tabela com estas
especificações, você deve salvá-la em um formato que pode ser enviado a
outra pessoa.

Usando as funções que foram abordas no tutorial passado e neste, fazer
isso com o R se torna uma tarefa bem mais simples do que em outras
linguagens.

``` r
demanda <- cadastro %>%
  filter(DRE %in% c("FO", "IQ", "SA")) %>%
  group_by(DRE) %>%
  summarise(ATIVAS = sum(SITUACAO == "Ativa"), PERC_ATIVAS = ATIVAS/n())

demanda
```

    #> # A tibble: 3 x 3
    #>   DRE   ATIVAS PERC_ATIVAS
    #>   <chr>  <int>      <dbl>
    #> 1 FO       383      0.943
    #> 2 IQ       395      0.975
    #> 3 SA       361      0.958

Obs.: A função `n()` só pode ser utilizada dentro de um `summarise()`
porque ela retorna o número de linhas dentro de cada grupo (ou seja, no
comando acima o número de escolas ativas em cada DRE é dividido pelo
número total de escolas naquele DRE).

Agora para salvar basta usar as irmãs das funções `read_***()` do
tutorial passado: as `write_***()` ("escrever \*\*\*"). Neste caso você
irá salvar a nova tabela `demanda` em um CSV:

``` r
# O caminho abaixo deve ser o nome do arquivo onde salvar a tabela
write_csv(demanda, "Documents/demanda.csv")
```

### Funções bônus

Outras funções que podem ser úteis de se aprender são o par `gather()`
(“reunir”) e `spread()` (“espalhar”). A primeira transforma uma
coleção de colunas em uma coluna “chave” e outra “valor”, enquanto a
segunda faz a operação inversa.

Observe as colunas `T2D3D`, `T2D3D16` e assim por diante. No fundo elas
expressam a mesma coisa mas em anos diferentes; se você quisesse
analisar esse conjunto de colunas como um todo seria muito difícil
fazê-lo com tantas colunas separadas.

Para isso o comando abaixo utiliza `gather()`. Ele cria uma nova coluna
`ANO` com os nomes as variáveis tombados e uma coluna `TURNOS` com os
valores correspondentes daquelas variáveis antes de serem tombadas (note
que isso deixa a tabela bem mais alta).

``` r
cadastro %>%
  select(CODESC, starts_with("T2")) %>%
  gather("ANO", "TURNOS", starts_with("T2")) %>%
  arrange(CODESC)
```

    #> # A tibble: 75,658 x 3
    #>    CODESC ANO     TURNOS
    #>    <chr>  <chr>   <chr> 
    #>  1 000086 T2D3D   2D    
    #>  2 000086 T2D3D16 2D    
    #>  3 000086 T2D3D15 2D    
    #>  4 000086 T2D3D14 2D    
    #>  5 000086 T2D3D13 2D    
    #>  6 000086 T2D3D12 2D    
    #>  7 000086 T2D3D11 2D    
    #>  8 000086 T2D3D10 2D    
    #>  9 000086 T2D3D09 3D    
    #> 10 000086 T2D3D08 3D    
    #> # ... with 75,648 more rows

Obs.: O terceiro argumento de `gather()` deve ser um seletor de colunas
escrito na mesma forma que faz-se com `select()`.

Agora para demonstrar a operação inversa, você pode colocar `spread()`
ao final do *pipeline* acima.

``` r
cadastro %>%
  select(CODESC, starts_with("T2")) %>%
  gather("ANO", "TURNOS", starts_with("T2")) %>%
  arrange(CODESC) %>%
  spread(ANO, TURNOS)
```

    #> # A tibble: 6,878 x 12
    #>    CODESC T2D3D T2D3D07 T2D3D08 T2D3D09 T2D3D10 T2D3D11 T2D3D12 T2D3D13
    #>    <chr>  <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    #>  1 000086 2D    2D      3D      3D      2D      2D      2D      2D     
    #>  2 000094 2D    3D      3D      3D      2D      2D      2D      2D     
    #>  3 000108 2D    3D      3D      2D      2D      2D      2D      2D     
    #>  4 000191 2D    2D      2D      2D      2D      2D      2D      2D     
    #>  5 000205 2D    2D      2D      2D      2D      2D      2D      2D     
    #>  6 000213 2D    3D      3D      3D      2D      2D      2D      2D     
    #>  7 000221 2D    3D      2D      2D      2D      2D      2D      2D     
    #>  8 000230 2D    3D      3D      2D      2D      2D      2D      2D     
    #>  9 000248 2D    3D      3D      3D      3D      2D      2D      2D     
    #> 10 000256 2D    3D      3D      3D      3D      2D      2D      2D     
    #> # ... with 6,868 more rows, and 3 more variables: T2D3D14 <chr>,
    #> #   T2D3D15 <chr>, T2D3D16 <chr>
