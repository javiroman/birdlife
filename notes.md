# Basic Data Types

* numeric - (10.5, 55, 787)
* integer - (1L, 55L, 100L, where the letter "L" declares this as an integer)
* complex - (9 + 3i, where "i" is the imaginary part)
* character (a.k.a. string) - ("k", "R is exciting", "FALSE", "11.5")
* logical (a.k.a. boolean) - (TRUE or FALSE)

# Vectors
A vector is simply a list of items that are of the same type. For creating
a vector we use the c() function which is used to concatenate items together.

```
a <- c(1, 2, 3, 4)
fruits <- c("banana", "apple", "orange")
b <- 1:6 (the same as c(1:6) or c(1,2,3,4,5,6))
```
Podemos crear vectores con nombres: Creando un vector con los nombres y asociandolo al 
vector original. En este punto seria un named vector.

```
> days <- c('Mon','Tue','Wed','Thu','Fri','Sat','Sun')
> temps <- c(1,2,3,4,5,6,7) 
> names(temps) <- days 
> temps
Mon Tue Wed Thu Fri Sat Sun 
  1   2   3   4   5   6   7
```

Modificar/Añadir/Eliminar elementos de un vector:
Modificar
```
> v.tres
[1] "TRUE"  "TRUE"  "FALSE"
> v.tres[3]
[1] "FALSE"
> v.tres[3] <- "TRUE"
> v.tres[3]
[1] "TRUE"
```
Añadir
```
> v.tres <- append(v.tres, c("TRUE", "FALSE"))
[1] "TRUE"  "TRUE"  "TRUE"  "TRUE"  "FALSE"
> v.tres <- append(v.tres, "TRUE")           
[1] "TRUE" "TRUE" "TRUE" "TRUE"
```

Eliminar
```
> v.uno
 [1]  1  2  3  4  5  6  7  8  9 10
> v.uno[-c(1)] ==> Eliminamos elemento posicion uno del vector
[1]  2  3  4  5  6  7  8  9 10
```

Operaciones sobre vectores:

```
sum(v1)
# Standard Deviation
sd(v)
#Variance
var(v)
# Maximum Element
max(v)
#Minimum Element
min(v)
# Product of elements
prod(v)
# numero de elementos
length(v)

> v.tres
[1] "TRUE"  "TRUE"  "TRUE"  ""      NA      "FALSE" "T"    
> is.na(v.tres)     
[1] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
> any(is.na(v.tres))
[1] TRUE
> sum(is.na(v.tres))
[1] 1
> v.tres <- append(v.tres, NA)
> sum(is.na(v.tres))
[1] 2
> v.tres
[1] "TRUE"  "TRUE"  "TRUE"  ""      NA      "FALSE" "T"     NA     
```
Buscar caracteres con grep
```
> v.dos
 [1] "a" "b" "c" "d" "e" "f" "g" "h" "i" "j"
> grep("f", v.dos)
[1] 6
> grep("f|c", v.dos)
[1] 3 6
```
Sumar ocurrencias
```
> v.uno
 [1]  1  2  3  4  5  6  7  8  9 10  7  7  7  6  6
> sum(v.uno == 7)
[1] 4
> v.tres
[1] "TRUE"  "TRUE"  "TRUE"  ""      "TRUE"  "FALSE" "T"     "FALSE"
> sum(v.tres == "TRUE")
[1] 4
```

# Matrix

A matrix is a two dimensional data set with columns and rows.
The same as vector but two dimensions.

```
matrix(1:9, nrow = 3, ncol = 3)
thismatrix <- matrix(c(1,2,3,4,5,6), nrow = 3, ncol = 2)
```
# Data Frame

```
days <- c('lunes', 'martes', 'miercoles', 'jueves', 'viernes')
temp <- c(22,23,24,23,21)
rain <- c(T,T,F,F,T)

df <- data.frame(days,temp,rain)

       days temp  rain
1     lunes   22  TRUE
2    martes   23  TRUE
3 miercoles   24 FALSE
4    jueves   23 FALSE
5   viernes   21  TRUE
```
Note: El nombre de la columna (cada vector) es el nombre
de la variable del vector.
```
> c1 <- 1:10
> c2 <- letters[1:10]
> df <- data.frame(c1, c2)
> df
   c1 c2
1   1  a
2   2  b
3   3  c
4   4  d
5   5  e
6   6  f
7   7  g
8   8  h
9   9  i
10 10  j
> df <- data.frame(col.name1 = c1, col.name2 = c2)
> df
   col.name1 col.name2
1          1         a
2          2         b
3          3         c
4          4         d
5          5         e
6          6         f
7          7         g
8          8         h
9          9         i
10        10         j

> df$days #### Devuelve un vector
[1] "lunes"     "martes"    "miercoles" "jueves"    "viernes"  

> df[,"days"] #### Devuelve un vector
[1] "lunes"     "martes"    "miercoles" "jueves"    "viernes"  

> df["days"]  #### Devuelve un dataframe
       days
1     lunes
2    martes
3 miercoles
4    jueves
5   viernes

> df[1,] ### Devuelve un dataframe
   days temp rain
1 lunes   22 TRUE

> subset(df, subset = rain==T)
     days temp rain
1   lunes   22 TRUE
2  martes   23 TRUE
5 viernes   21 TRUE

> df[c("days", "temp")]
       days temp
1     lunes   22
2    martes   23
3 miercoles   24
4    jueves   23
5   viernes   21

> a <- order(df[,'temp']) #### ordenamos un vector, no un dataframe
> a
[1] 5 1 2 4 3 ### esto son las rows, el numero de la row
> df[a,] #### indexamos por el el resultado que es por indice
       days temp  rain
5   viernes   21  TRUE
1     lunes   22  TRUE
2    martes   23  TRUE
4    jueves   23 FALSE
3 miercoles   24 FALSE

 <- order(-df[,'temp'])
> df[a,]
       days temp  rain
3 miercoles   24 FALSE
2    martes   23  TRUE
4    jueves   23 FALSE
1     lunes   22  TRUE
5   viernes   21  TRUE

> df[[3,2]]
[1] 24
> df[[3,1]]
[1] "miercoles"
> df[[3,"days"]] ### ponemos el nombre de la columna
[1] "miercoles"

> df[[4,"temp"]] <- 999
> df
       days temp  rain
1     lunes   22  TRUE
2    martes   23  TRUE
3 miercoles   24 FALSE
4    jueves  999 FALSE
5   viernes   21  TRUE

df <- rbind(df, c("sabado", 25, T))


df <- read.csv("my-file.csv")
write.csv(df, "my-saved-file.csv")

> empty <- data.frame() ### creamos un datafreame vacio
> empty <- rbind(c(T, "hola", 24))
> empty
     [,1]   [,2]   [,3]
[1,] "TRUE" "hola" "24"
> colnames(empty) <- c("col.1", "col.2", "col.3")
> empty
     col.1  col.2  col.3
[1,] "TRUE" "hola" "24"


any(is.na(df)) ### algun missing data N/A
df[is.na(df)] <- 0

nrow(df)
ncol(df)
colnames(df)
rownames(df)
head(df)
tail(df)
```
# Lists

Allow store data structures in one varialbe, for
example a vector, a dataframe and a matrix.
A list in R can contain many different data types inside it. A list is a 
collection of data which is ordered and changeable.

v <- c(1, 2, 3)
m <- matrix(1:10,nrow=2)
df <- mtcars

my.list <- list(v, m, df)
my.list <- list(un_vector = v, una_matric = m, un_dataframe = df)
my.list$un_vector

# Data Input/Output -> CSV, EXCEL

```
write.csv(mtcars, file='mi_example.csv') 
df <- read.csv('example.csv') <- Lee un dataframe
```
Note: EXCEL files. There is a new library called readxl and writexl which are really easy to 
install and use, you can check them out here: https://readxl.tidyverse.org/
The older library requires Java to be installed, also with the RJava library.
```
install.packages('readxl')
library(readxl)
excel_sheets('mi_execl_file.xlsx') -> List all sheets in an excel spreadsheet
[1] "Sheet1"
df <- read_excel('mi_excel_file.xlsx', sheet="Sheet1") -> como siempre carga un DataFrame
```
Leer todo el excel
```
entire.df <- lapply(excel_sheets("my_excel.xlsx"),read_excel,patch="my_excel.xlsx") 
```
Note: Apply a Function over a List or Vector
```
install.packages('xlsx') => Esto es para poder escribir EXCELs
library('xlsx')
write.xlsx(mtcars, "output.xlsx")
```
# Misc:
```
data()
ls()
rm(variable-name)
class(variable-name)
summary(variable-name)
str(variable-name) -> structure of object, saca las columnas disponibles y un pequeño resumen
factor() -> Un factor es una estructura de datos que sirve para trabajar con variables categóricas, es decir, aquellas variables que toman una cantidad limitada o finita de variables o categorías
shell("clear") ==> borrar screen tirando del shell
ncol(df) => numero columnas
nrow(df) => numero filas
all.equal(x, y) => is a utility to compare R objects x and y testing ‘near equality’. 
If they are different, comparison is still made to some extent, and a report of the differences is returned.
rep(3, times=7)
length(unique(cur1.df$BillingPeriodStart)) => si sale uno significa que todos los elementos son iguales
```
RStudio:

```
Ctrl+Shift+1 -> toggle full screen Editor
Ctrl+Shift+2 -> toggle full screen Console
```

# Plotting
```
plot(factor(mi-variable-categorica))

par() => This function allows you to control various graphical "parameters"

par(mar = c(5, 4, 4, 2) + 0.1):
  mar => margin
  c(5, 4, 4, 2) + 0.1 => botton, left, top and right margins
plot(1:10)

- Como exportar PNG una tabla textual (un data frame en este ejemplo):

cur.tmp <- head(filter(select(cur2.df, 
            BillingPeriodStart, 
            BillingPeriodEnd,
            ChargePeriodStart,
            ChargePeriodEnd,
            ServiceName,
            ResourceId,
            BillingCurrency,
            BilledCost
            ),
            ServiceName == "Amazon Virtual Private Cloud", ResourceId != "", BilledCost != 0
          ), n=20)

install.packages("gridExtra")
library(gridExtra)

myTable <- tableGrob(cur.tmp)
grid.draw(myTable)
```

# Tidyverse

The tidyverse is an opinionated collection of R packages designed for data science. All packages share an underlying design philosophy, 
grammar, and data structures. Puesto que R es un paquete estadístico muy extendido, es frecuente añadir nuevas funcionalidades
y formas de trabajar en forma de paquetes, en vez de cambiar el core de R en si mismo. Este paquete Tidyverse es un claro
ejemplo de ello, proporcionando nuevas formas y/o optimizaciones. Los paquetes incluidos en este "universo" son:

* ggplot2: Graphics, based on The Grammar of Graphics book.
* dplyr: Grammar of data manipulation.
* tidyr: Functions that help you get to tidy data. Tidy data is data with a consistent form.
* purrr: R’s functional programming (FP) toolkit by providing a complete and consistent set of tools for working with functions and vectors.
* readr: Readr provides a fast and friendly way to read rectangular data (like csv, tsv, and fwf).
* tibble: A modern re-imagining of the data frame.
* stringr: Cohesive set of functions designed to make working with strings as easy as possible.
* forcats: Useful tools that solve common problems with factors.
* lubridate: Functions for working with date-times

## dplyr: A Grammar of Data Manipulation

```
# The easiest way to get dplyr is to install the whole tidyverse:
install.packages("tidyverse")

# Alternatively, install just dplyr:
install.packages("dplyr")

filter(my-dataframe, month==11, day==3) => crea un DF con las rows que cumplen esas columnas
- Lo mismo pero con las sintaxis built-in sería mas engorroso:
my-dataframe[my-dataframe$month == 11 & my-dataframe$day == 3]

slice(my-dataframe,1:10)  ==> crea un DF seleccionando las rows por posicion, en el ejemplo saca las primeras 10 rows
arrange(my-dataframe, month, day) ==> Es igual a filter(), pero ordena las rows. orders the rows of a data frame by the values of selected columns.
arrange(my-dataframe, month, desc(day)) ==> obligamos a que sea ordenados los dias descendentemente.
select(my-dataframe, month) ==> saca la columna indicada, o las columnas indicadas
rename(my-dataframe, mes = month) ==> renombra columnas, ahora la columna month se llama mes.
distinct(my-dataframe, month) ==> selecciona los valores distintos de una columna, the uniq values of this column. Es lo miso que usar unique
mutate()
transmutate()
summarise()
sample_n()
sample_frac()
```



