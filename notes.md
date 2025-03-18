# Basic Data Types

* numeric - (10.5, 55, 787)
* integer - (1L, 55L, 100L, where the letter "L" declares this as an integer)
* complex - (9 + 3i, where "i" is the imaginary part)
* character (a.k.a. string) - ("k", "R is exciting", "FALSE", "11.5")
* logical (a.k.a. boolean) - (TRUE or FALSE, T or F)

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
In R lists act as containers. Unlike atomic vectors, the contents of a list are 
not restricted to a single mode and can encompass any mixture of data types. 
Lists are sometimes called generic vectors, because the elements of a list 
can by of any type of R object, even lists containing further lists. 
This property makes them fundamentally different from atomic vectors.

```
v <- c(1, 2, 3)
m <- matrix(1:10,nrow=2)
df <- mtcars

my.list <- list(v, m, df)
my.list <- list(un_vector = v, una_matric = m, un_dataframe = df)
my.list$un_vector
```
```
> list_data <- list(
    c("Jan","Feb","Mar"), 
    matrix(c(3,9,5,1,-2,8), nrow = 2), 
    list("green",12.3)
   )
> names(list_data) <- c("A_Vector", "A_Matrix", "A_List")
> list_data
$A_Vector
[1] "Jan" "Feb" "Mar"

$A_Matrix
     [,1] [,2] [,3]
[1,]    3    5   -2
[2,]    9    1    8

$A_List
$A_List[[1]]
[1] "green"

$A_List[[2]]
[1] 12.3

> list_data$A_Vector
[1] "Jan" "Feb" "Mar"

> list_data$A_List
[[1]]
[1] "green"

[[2]]
[1] 12.3

> list_data$A_List[1]
[[1]]
[1] "green"

> list_data$A_List[2]
[[1]]
[1] 12.3
```
Otra forma de crear una named-list en una sola línea:
```
> list_data <- list(
    A_Vector =  c("Jan","Feb","Mar"), 
    A_Matrix = matrix(c(3,9,5,1,-2,8), nrow = 2), 
    A_List = list("green",12.3))
```

Esto es importante: In R, double square brackets [[ ]] are used to access or extract elements
from a list. When you use single square brackets [ ], you get a list containing the specified
elements. However, when you use double square brackets [[ ]], you directly access 
the elements themselves.
```
# Create a list in R
my_list <- list(a = 1, b = 2, c = 3)

# Using single square brackets, you get a sublist
sublist <- my_list["a"]
print(sublist)  # Output: $a [1] 1

# Using double square brackets, you get the element itself
element <- my_list[[ "a" ]]
print(element)  # Output: [1] 1
```
In summary:
```
* [ ] returns a list containing the specified elements.
* [[ ]] returns the elements themselves.
```

Vamos a crear una named-list de named-lists, o dicho de otra forma
una lista de listas anidadas:

```
# Create the inner lists
inner_list_1 <- list(inner_list_1_element_1 = "Element 1.1",
                     inner_list_1_element_2 = "Element 1.2",
                     inner_list_1_element_3 = "Element 1.3")

inner_list_2 <- list(inner_list_2_element_1 = "Element 2.1",
                     inner_list_2_element_2 = "Element 2.2",
                     inner_list_2_element_3 = "Element 2.3")

inner_list_3 <- list(inner_list_3_element_1 = "Element 3.1",
                     inner_list_3_element_2 = "Element 3.2",
                     inner_list_3_element_3 = "Element 3.3")

# Create the main list containing the inner lists
mi_list <- list(inner_list_1 = inner_list_1,
                inner_list_2 = inner_list_2,
                inner_list_3 = inner_list_3)

# Print the list
print(mi_list)
```
Para obtener un elemento en particular, por ejemplo "Element 3.2":

```
element_3_2 <- mi_list[["inner_list_3"]][["inner_list_3_element_2"]]

# Print the element
print(element_3_2)
```

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

En R tenemos disponibles distintos sistemas gráficos, aunque los más comunes son:

- Sistema gráfico base de R (autor: R Core Team and contributors). El núcleo (core en inglés) gráfico en R se encuentra en los paquetes graphics (contiene las funciones de gráficos base: plot, hist, etc.) y grDevices (que implementa los distintos dispositivos gráficos: pdf, ps, png, …).

- Lattice (autor:Deepayan Sarkar). El libro Lattice. Multivariate Data Visualization with R (http://www.springer.com/gp/book/9780387759685) proporciona una gran cantidad de ejemplos (con código R).

- ggplot2 (autor: Hadley Wickham). Hadley Wickham ha escrito un libro en el que explica de forma muy didáctica los fundamentos para elaborar gráficos con este paquete. En este enlace lo puedes encontrar http://link.springer.com/book/10.1007%2F978-3-319-24277-4

- Esquisse is a package built on top of ggplot2 that provides interactive drag-and-drop visualizations. The package creates a Tableau-like interface for plotting in ggplot2, allowing the user to go through the data quickly and without the code

- Plotly is the second most popular visualization package in R after ggplot2. Whereas ggplot2 is used for static plots, plotly is used for creating dynamic plots. Similarly, it offers a plethora of options in terms of chart type we can visualize our data with. Still, compared to ggplot2, it is primarily utilized for producing interactive and 3D web-based plots that are lacking in ggplot2 
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

The easiest way to get dplyr is to install the whole tidyverse
```
install.packages("tidyverse")
```
Alternatively, install just dplyr:
```
install.packages("dplyr")
```

Un claro ejemplo de la simplicidad de uso, contrastado con el estándar R, es este ejemplo.
Crear un DF con las rows que cumplen esas columnas:
```
filter(my-dataframe, month==11, day==3)
```
Lo mismo pero con las sintaxis R estándar (built-in) sería mas engorroso:
```
my-dataframe[my-dataframe$month == 11 & my-dataframe$day == 3]
```
Otras operaciones de dplyr:

```
# crea un DF seleccionando las rows por posicion, en el ejemplo saca las primeras 10 rows:
slice(my-dataframe,1:10)

# Es igual a filter(), pero ordena las rows. orders the rows of a data frame by the values of selected columns:
arrange(my-dataframe, month, day)

# obligamos a que sea ordenados los dias descendentemente.
arrange(my-dataframe, month, desc(day))

# saca la columna/s indicada/s
select(my-dataframe, month)

# renombra columnas, ahora la columna month se llama mes.
rename(my-dataframe, mes = month)

# selecciona los valores distintos de una columna, the uniq values of this column. Es lo miso que usar unique
distinct(my-dataframe, month)

mutate()
transmutate()
summarise()
sample_n()
sample_frac()
```

## purr: FP

The tidyverse package in R provides some useful tools for managing lists, especially through the purrr package, 
which is part of the tidyverse. The purrr package is designed for functional programming and provides a consistent 
and concise syntax for working with lists and other data structures.

Here are some common functions from purrr that can be used to manage lists:

* map(): Apply a function to each element of a list.
* map2(): Apply a function to corresponding elements of two lists.
* pmap(): Apply a function to corresponding elements of multiple lists.
* reduce(): Reduce a list to a single value by iteratively applying a function.
* keep(): Keep elements that satisfy a predicate.
* discard(): Discard elements that satisfy a predicate.
* pluck(): Extract elements by name or position.

Here are some examples to illustrate the use of these functions:

```
# Create a list
my_list <- list(a = 1, b = 2, c = 3)

# Use map() to apply a function to each element
squared_list <- map(my_list, ~ .x ^ 2)
print(squared_list)  # Output: $a [1] 1, $b [1] 4, $c [1] 9

# Use map2() to apply a function to corresponding elements of two lists
list1 <- list(a = 1, b = 2, c = 3)
list2 <- list(x = 10, y = 20, z = 30)
sum_list <- map2(list1, list2, ~ .x + .y)
print(sum_list)  # Output: $a [1] 11, $b [1] 22, $c [1] 33

# Use pmap() to apply a function to corresponding elements of multiple lists
list1 <- list(a = 1, b = 2, c = 3)
list2 <- list(x = 10, y = 20, z = 30)
list3 <- list(m = 100, n = 200, o = 300)
product_list <- pmap(list(list1, list2, list3), ~ ..1 * ..2 * ..3)
print(product_list)  # Output: $a [1] 1000, $b [1] 8000, $c [1] 27000

# Use reduce() to reduce a list to a single value
my_list <- list(1, 2, 3, 4, 5)
sum_value <- reduce(my_list, `+`)
print(sum_value)  # Output: [1] 15

# Use keep() to keep elements that satisfy a predicate
my_list <- list(a = 1, b = 2, c = 3)
filtered_list <- keep(my_list, ~ .x > 1)
print(filtered_list)  # Output: $b [1] 2, $c [1] 3

# Use discard() to discard elements that satisfy a predicate
my_list <- list(a = 1, b = 2, c = 3)
filtered_list <- discard(my_list, ~ .x > 1)
print(filtered_list)  # Output: $a [1] 1

# Use pluck() to extract elements by name or position
nested_list <- list(a = list(b = list(c = 42)))
value <- pluck(nested_list, "a", "b", "c")
print(value)  # Output: [1] 42
```

## ggplot2: Grammar of Graphics

La "grammar of graphics" (gramática de gráficos) es un marco teórico para describir y construir gráficos de manera sistemática. 
Fue popularizada en gran parte por el libro "The Grammar of Graphics" de Leland Wilkinson y se encuentra en la base de muchas 
herramientas modernas de visualización de datos, como ggplot2 en R.

En este contexto, dos conceptos clave son la "data" (datos) y el "mapping" (mapeo):

- Data (Datos)
Los datos son la entrada fundamental para cualquier visualización. En el contexto de la gramática de gráficos, los datos se estructuran generalmente en forma de tablas (data frames), donde cada fila representa una observación y cada columna una variable. Los datos pueden provenir de cualquier fuente y pueden ser de cualquier tipo: cuantitativos, cualitativos, temporales, etc.

- Mapping (Mapeo)
El mapeo es el proceso de vincular las variables de los datos a las propiedades visuales de los gráficos. Esto se hace utilizando "aesthetics" (estéticas), que son los atributos visuales que pueden ser modificados para representar datos. Algunos ejemplos comunes de estéticas incluyen:

- x: la posición en el eje x.
- y: la posición en el eje y.
- color: el color de los elementos gráficos.
- size: el tamaño de los elementos gráficos.
- shape: la forma de los puntos en un gráfico de dispersión.
- line: el tipo de línea en un gráfico de líneas.

Para ilustrar estos conceptos, veamos un ejemplo simple utilizando ggplot2 en R:

```
library(ggplot2)

# Ejemplo de datos
data <- data.frame(
  x = rnorm(100),
  y = rnorm(100),
  category = sample(letters[1:3], 100, replace = TRUE)
)

# Creación del gráfico
ggplot(data, aes(x = x, y = y, color = category)) +
  geom_point()
```
En este ejemplo:

- data: es el data frame que contiene las variables x, y y category.
- aes(): es la función que define el mapeo de las variables a las estéticas.
  - x = x: mapea la variable x a la estética de posición en el eje x.
  - y = y: mapea la variable y a la estética de posición en el eje y.
  - color = category: mapea la variable category a la estética de color.
- geom_point(): añade puntos al gráfico, utilizando las estéticas definidas

En el contexto de la gramática de gráficos, y específicamente en herramientas como ggplot2 en R, 
los componentes del mapeo (mapping) incluyen los siguientes elementos: capa (layer), escalas (scales), 
coordenadas (coord), facetas (facet) y tema (theme). Aquí hay una explicación de cada uno:

1. Layer (Capa)
   
Las capas son componentes fundamentales en la construcción de gráficos. Cada capa representa una adición a la visualización, como puntos, líneas, barras, etc. Los componentes de una capa incluyen:

- Datos (Data): El conjunto de datos que se visualizará en la capa.
- Estéticas (Aesthetics): Las variables del conjunto de datos mapeadas a atributos visuales (ejes, colores, tamaños, etc.).
- Geometrías (Geometries): El tipo de gráfico usado para representar los datos (puntos, líneas, barras, etc.).
- Estadísticas (Statistics): Transformaciones estadísticas aplicadas a los datos antes de la visualización.
- Posición (Position): Ajustes de posición aplicados a los elementos gráficos (apilamiento, apilamiento en diente de sierra, etc.).

A layer is a collection of geometric elements and statistical transformations. Geometric elements, geoms for short, represent what you actually see in the plot: points, lines, polygons, etc. Statistical transformations, stats for short, summarise the data: for example, binning and counting observations to create a histogram, or fitting a linear model.
```
ggplot(data, aes(x = x, y = y)) +
  geom_point() +  # Capa de puntos
  geom_smooth()   # Capa de línea suavizada
```

2. Scales (Escalas)
   
Las escalas controlan cómo se mapean los datos a las estéticas. Esto incluye la transformación de los datos y la asignación de valores a las estéticas visuales. Ejemplos de escalas incluyen:

- scale_x_continuous(): Escala continua para el eje x.
- scale_y_log10(): Escala logarítmica para el eje y.
- scale_color_manual(): Escala de color manual.

Scales map values in the data space to values in the aesthetic space. This includes the use of colour, shape or size. Scales also draw the legend and axes, which make it possible to read the original data values from the plot (an inverse mapping).
```
ggplot(data, aes(x = x, y = y, color = category)) +
  geom_point() +
  scale_color_manual(values = c("red", "green", "blue"))
```

3. Coord (Coordenadas)
   
El sistema de coordenadas define cómo se mapean los datos a la posición en el gráfico. Algunos sistemas de coordenadas comunes incluyen:

- coord_cartesian(): Sistema de coordenadas cartesiano.
- coord_polar(): Sistema de coordenadas polares.
- coord_flip(): Intercambia los ejes x e y.

A coord, or coordinate system, describes how data coordinates are mapped to the plane of the graphic. It also provides axes and gridlines to help read the graph. We normally use the Cartesian coordinate system, but a number of others are available, including polar coordinates and map projections.
```
ggplot(data, aes(x = x, y = y)) +
  geom_point() +
  coord_flip()  # Intercambia los ejes x e y
```

4. Facet (Facetas)
   
Las facetas permiten dividir los datos en subconjuntos y crear gráficos separados para cada subconjunto. Esto es útil para comparar diferentes grupos dentro de los datos. Ejemplos de facetas incluyen:

- facet_wrap(): Crea una matriz de gráficos separados por una variable.
- facet_grid(): Crea una cuadrícula de gráficos usando dos variables.

A facet specifies how to break up and display subsets of data as small multiples. This is also known as conditioning or latticing/trellising.
```
ggplot(data, aes(x = x, y = y)) +
  geom_point() +
  facet_wrap(~ category)  # Divide el gráfico por la variable 'category'
```

5. Theme (Tema)
   
El tema controla la apariencia general del gráfico, incluyendo elementos no relacionados con los datos como fuentes, colores de fondo, bordes, etc. ggplot2 proporciona varios temas predefinidos y permite personalizar cada aspecto del gráfico.
A theme controls the finer points of display, like the font size and background colour. While the defaults in ggplot2 have been chosen with care, you may need to consult other references to create an attractive plot.
```
ggplot(data, aes(x = x, y = y)) +
  geom_point() +
  theme_minimal()  # Aplica un tema minimalista
```

