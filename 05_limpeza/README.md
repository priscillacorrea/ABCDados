Tutorial 05: Limpeza
================

### Sobre este tutorial

Depois que você tiver uma tabela importada no R começa a parte difícil
do trabalho: limpar os dados. Neste tutorial você aprenderá algumas
funções úteis para filtrar linhas e colunas de uma base de dados,
permitindo que você selecione apenas as informações com as quais você
irá trabalhar.

Neste ponto assume-se que você já realizou o tutorial 04 sobre
importação e tem no seu ambiente os objetos `dicionario` e `cadastro`,
pois aqui eles serão utilizados com frequência.

### Selecionando colunas

A limpeza mais simples que você pode fazer em uma tabela é selecionar um
subconjunto de colunas. Aqui você utilizará uma função chamada
`select()` (“selecionar”) e algumas auxiliares chamadas `starts_with()`
(“começa com”) e `contains()` (“contém”). Só não se esqueça de carregar
o `tidyverse`\!

``` r
library(tidyverse)

# Selecionando duas colunas por nome
select(cadastro, NOMESC, DATABASE)
```

    #> # A tibble: 6,878 x 2
    #>    NOMESC                                  DATABASE 
    #>    <chr>                                   <chr>    
    #>  1 PAULO CAMILHIER FLORENCANO              28-dez-17
    #>  2 VICENTE PAULO DA SILVA                  28-dez-17
    #>  3 JOSE ERMIRIO DE MORAIS, SEN.            28-dez-17
    #>  4 ALIPIO CORREA NETO, PROF.               28-dez-17
    #>  5 VERA LUCIA APARECIDA RIBEIRO, PROFA.    28-dez-17
    #>  6 ANTONIO CARLOS PACHECO E SILVA, PROF.   28-dez-17
    #>  7 NAIR CORREA BUARQUE                     28-dez-17
    #>  8 MARIA YOLANDA DE SOUZA PINTO HAHNE, DA. 28-dez-17
    #>  9 WALFRIDO DE CARVALHO, CEL.              28-dez-17
    #> 10 WILMA ALVARENGA DE OLIVEIRA, PROFA.     28-dez-17
    #> # ... with 6,868 more rows

A função `select()` recebe como primeiro argumento uma tabela e, depois
disso, todas as colunas que você quiser selecionar. Se você precisar
selecionar um número muito grande de colunas, há alguns atalhos
mostrados a seguir. Não será exibido o resultado de cada comando porque
isso deixaria o tutorial desnecessariamente comprido, então copie toda a
caixa abaixo e execute cada linha para ver o que acontece\!

``` r
# Selecionar colunas número 1, 3 e 6
select(cadastro, 1, 3, 6)

# Selecionar as colunas de 1 a 6
select(cadastro, 1:6)

# Selecionar as colunas de DRE a DIRETORIA
select(cadastro, DRE:DIRETORIA)

# Selecionar as colunas de DRE a DIRETORIA e ENDERECO
select(cadastro, DRE:DIRETORIA, ENDERECO)

# Selecionar as colunas cujo nome começa com "T2"
select(cadastro, starts_with("T2"))

# Selecionar as colunas cujo nome contém "TURNO"
select(cadastro, contains("TURNO"))

# Descartar a coluna FAX
select(cadastro, -FAX)

# Selecionar as colunas 1 a 6, exceto pela 4
select(cadastro, 1:6, -4)

# Selecionar as colunas de DRE a DIRETORIA, exceto pela CODESC
select(cadastro, DRE:DIRETORIA, -CODESC)
```

### Filtrando linhas

Outra limpeza que você pode querer fazer em uma base é remover linhas
indesejadas. Às vezes você sabe que uma coluna não pode ter um valor
pequeno demais, que uma coluna não pode ter um certo valor específico, e
assim por diante. Para fazer isso vamos utilizar a função `filter()`
(“filtrar”).

``` r
# Filtrar escolas da Diretoria Regional abreviada por "FO"
filter(cadastro, DRE == "FO")
```

    #> # A tibble: 406 x 53
    #>    DRE   CODESC TIPOESC NOMESC DIRETORIA SUBPREF CEU   ENDERECO NUMERO
    #>    <chr> <chr>  <chr>   <chr>  <chr>     <chr>   <chr> <chr>    <chr> 
    #>  1 FO    000094 EMEI    VICEN… FREGUESI… CASA V… <NA>  RUA DOU… 295   
    #>  2 FO    000221 EMEI    NAIR … FREGUESI… FREGUE… <NA>  RUA SAN… 51    
    #>  3 FO    000299 EMEF    ROBER… FREGUESI… CASA V… <NA>  RUA ANT… 147   
    #>  4 FO    013111 EMEI    CAIO … FREGUESI… FREGUE… <NA>  RUA PED… 74    
    #>  5 FO    013315 EMEI    MARIA… FREGUESI… CASA V… <NA>  RUA SOL… 303   
    #>  6 FO    014567 EMEI    TITO … FREGUESI… FREGUE… <NA>  RUA JER… 300   
    #>  7 FO    018295 EMEI    ALEX … FREGUESI… FREGUE… <NA>  RUA SAN… 185   
    #>  8 FO    018554 EMEI    ANTON… FREGUESI… CASA V… <NA>  RUA ARA… 100   
    #>  9 FO    019252 EMEI    JOSE … FREGUESI… FREGUE… <NA>  RUA MON… S/N   
    #> 10 FO    019304 CEU EM… PAZ    FREGUESI… FREGUE… PAZ   RUA DAN… 1549  
    #> # ... with 396 more rows, and 44 more variables: BAIRRO <chr>, CEP <chr>,
    #> #   TEL1 <chr>, TEL2 <chr>, FAX <chr>, SITUACAO <chr>, CODDIST <chr>,
    #> #   DISTRITO <chr>, SETOR <chr>, CODINEP <int>, CODCIE <int>, EH <dbl>,
    #> #   DT_CRIACAO <chr>, ATO_CRIACAO <chr>, DOM_CRIACAO <chr>,
    #> #   DT_INI_FUNC <chr>, DT_AUTORIZA <chr>, NOME_ANT <chr>, T2D3D <chr>,
    #> #   T2D3D16 <chr>, T2D3D15 <chr>, T2D3D14 <chr>, T2D3D13 <chr>,
    #> #   T2D3D12 <chr>, T2D3D11 <chr>, T2D3D10 <chr>, T2D3D09 <chr>,
    #> #   T2D3D08 <chr>, T2D3D07 <chr>, DTURNOS <chr>, DTURNOS16 <chr>,
    #> #   DTURNOS15 <chr>, DTURNOS14 <chr>, DTURNOS13 <chr>, DTURNOS12 <chr>,
    #> #   DTURNOS11 <chr>, DTURNOS10 <chr>, DTURNOS09 <chr>, DTURNOS08 <chr>,
    #> #   DTURNOS07 <chr>, LATITUDE <int>, LONGITUDE <int>, REDE <chr>,
    #> #   DATABASE <chr>

Note que a saída da função agora só tem 406 linhas\! Isso é porque esse
comando mantém apenas as linhas nas quais a coluna `DRE` possui valor
igual a “FO”.

Obs.: O comando acima não contém nenhum erro de digitação. Para
verificar se duas coisas são iguais em R usamos dois símbolos de
igualdade (`==`)\! Você verá mais sobre isso na seção a seguir e no
tutorial sobre controle.

Obs. 2: Perceba que quando você usa o nome de uma coluna dentro de
`filter()` não se colocam aspas em volta dele, mas as aspas são
necessárias quando trata-se do valor verificado. Isso é porque a coluna
`DRE` contém textos, então, para verificar se a quela coluna é igual a
um valor, este valor precisa ser um texto.

Como com a `select()`, abaixo são apresentados alguns comandos exemplos
para `filter()`. Copie a caixa abaixo no seu R e veja o que eles fazem\!

``` r
# Filtrar escolas com DRE diferente de "FO"
filter(cadastro, DRE != "FO")

# Filtrar escolas com CODINEP menor que 35000000
filter(cadastro, CODINEP < 35000000)

# Filtrar escolas com CODINEP menor que 35000000 e DRE igual a "FO"
filter(cadastro, CODINEP < 35000000, DRE == "FO")

# Filtrar escolas com DRE dentre "FO", "G" e "IQ"
filter(cadastro, DRE %in% c("FO", "G", "IQ"))

# Filtrar escolas sem informação na coluna CEU
filter(cadastro, is.na(CEU))

# Filtrar escolas com informação na coluna CEU
filter(cadastro, !is.na(CEU))
```

### Operadores lógicos

Abaixo você vai encontrar uma breve lista com todos os operadores
lógicos que podem ser utilizados dentro da função `filter()`. A maior
parte deles é apenas um comparador matemático, mas alguns podem ser
fontes de dúvida.

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

A operação de “ou” (barra vertical) é um pouco delicada e merece atenção
especial. Ela será atendida se apenas `op1` for atendida, se apenas
`op2` for atendida ou se tanto `op1` quanto `op2` forem atendidas.

Diferentemente das outras, `is.na()` não é exatamente um operador
lógico, mas sim uma função que lida com um tipo de objeto particular ao
R: `NA` (abreviação de “não disponível”). Se você abrir `cadastro` com a
função `View()` e observar a coluna `CEU`, você notará que grande parte
das linhas contém as letras “NA” em itálico e com uma cor diferente;
isso é a forma do R de dizer que não há nada naquela célula, equivalente
a uma célula absolutamente vazia no Excel.

### Ordenando colunas

A última função que você aprenderá neste tutorial é `arrange()`
(“organizar”). Ela recebe uma tabela e uma série de colunas,
ordenando-as uma a uma exatamente da mesma forma que acontece no SQL por
exemplo. Com `desc()` também é possível ordenar as colunas de forma
decrescente.

``` r
# Ordenar escolas por ordem alfabética de DRE
arrange(cadastro, DRE)
```

    #> # A tibble: 6,878 x 53
    #>    DRE   CODESC TIPOESC NOMESC DIRETORIA SUBPREF CEU   ENDERECO NUMERO
    #>    <chr> <chr>  <chr>   <chr>  <chr>     <chr>   <chr> <chr>    <chr> 
    #>  1 BT    000191 EMEF    ALIPI… BUTANTA   BUTANTA <NA>  AVENIDA… 140   
    #>  2 BT    000213 EMEI    ANTON… BUTANTA   BUTANTA <NA>  AVENIDA… 90    
    #>  3 BT    000477 EMEF    EDA T… BUTANTA   BUTANTA <NA>  RUA ENG… 333   
    #>  4 BT    011924 EMEF    MARIA… BUTANTA   BUTANTA <NA>  RUA CAC… 575   
    #>  5 BT    014591 EMEI    BENED… BUTANTA   BUTANTA <NA>  RUA CAC… S/N   
    #>  6 BT    018236 EMEI    MARIA… BUTANTA   BUTANTA <NA>  RUA JOA… S/N   
    #>  7 BT    018244 EMEI    CAMIL… BUTANTA   BUTANTA <NA>  RUA JOS… 495   
    #>  8 BT    018384 EMEI    MOREN… BUTANTA   BUTANTA <NA>  RUA MAR… 381   
    #>  9 BT    019160 EMEF    ILEUS… BUTANTA   BUTANTA <NA>  RUA D    10    
    #> 10 BT    019242 EMEI    MARIA… BUTANTA   BUTANTA <NA>  RUA EUD… 118   
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
    #> #   DTURNOS09 <chr>, DTURNOS08 <chr>, DTURNOS07 <chr>, LATITUDE <int>,
    #> #   LONGITUDE <int>, REDE <chr>, DATABASE <chr>

Abaixo seguem mais alguns exemplos para você testar no seu R:

``` r
# Ordenar escolas por ordem alfabética de DRE e NOMESC
arrange(cadastro, DRE, NOMESC)

# Ordenar escolas por ordem anti-alfabética de TIPOESC
arrange(cadastro, desc(TIPOESC))
```
