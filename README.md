# Potenciando tus Análisis con Power BI: Una Profunda Inmersión en la Lógica, ETL y Modelado de Datos![principal](https://github.com/vicente2121/Analisis_negocio/assets/72566296/e218b8ed-c732-47c3-b95d-c40f54b5a289)


En el mundo de la analítica de datos, el poder de una herramienta como Power BI es inigualable. En este artículo, exploraremos a fondo cómo utilizar Power BI para dominar la lógica, el proceso ETL y el modelado de datos. Desde la extracción de datos hasta la creación de medidas personalizadas, desentrañaremos los secretos de esta poderosa plataforma.

## Orígenes de Datos y Conexión Tipo Carpeta

Comenzamos nuestro viaje analizando la diversidad de orígenes de datos disponibles, desde archivos Excel hasta documentos PDF almacenados en diferentes ubicaciones, incluyendo local y SharePoint. A través de la conexión tipo carpeta de Power Query, destacamos cómo esta funcionalidad nos permite consolidar una gran cantidad de archivos en una única conexión, simplificando así nuestro proceso de transformación y análisis.

## Transformación de Datos con Power Query![modelado](https://github.com/vicente2121/Analisis_negocio/assets/72566296/60caaae3-f236-4df3-89f5-f9c6d178eee9)


La clave para aprovechar al máximo nuestros datos radica en la capacidad de transformación de Power Query. Exploramos la lógica detrás de la primera obtención de datos, enfocándonos en la extracción y normalización de múltiples archivos PDF con datos no estructurados. Detallamos los procesos utilizados, como la división de columnas, el reemplazo de valores y la extracción de texto, destacando cómo estas técnicas nos permiten convertir datos caóticos en información procesable.

## Creación de Tablas y Medidas DAX

Con nuestros datos transformados, pasamos al modelado de datos en Power BI. Explicamos la importancia de las tablas transaccionales y dimensionales en la creación de un modelo sólido. Destacamos la dimensión de fechas como elemento fundamental y profundizamos en la implementación de medidas DAX para calcular indicadores financieros clave. Utilizamos un ejemplo práctico para ilustrar cómo definir medidas personalizadas, como la medida "Icono Costo", que calcula la variación entre costos previos y actuales y devuelve un icono visual correspondiente.

Icono Costo: Esta medida calcula la variación entre el costo actual y el costo del trimestre anterior y devuelve un icono visual correspondiente.
Aquí está el proceso paso a paso:
Se calcula la variación entre el costo actual (Valor_Actual) y el costo del trimestre anterior (ValorPrevio).
Se utiliza la función DIVIDE para evitar errores de división por cero.

Luego, se utiliza una declaración IF para determinar si la variación es negativa o positiva.
Si la variación es negativa, devuelve un icono de flecha hacia abajo, que es el carácter Unicode correspondiente a una flecha hacia abajo.
Si la variación es positiva, devuelve un icono de flecha hacia arriba, que es el carácter Unicode correspondiente a una flecha hacia arriba.
Finalmente, se devuelve el resultado.

Color Costo: Esta medida calcula la variación entre el costo actual y el costo del trimestre anterior y devuelve un color correspondiente (rojo para variación negativa y verde para variación no negativa).
Al igual que en la medida anterior, se calcula la variación entre el costo actual y el costo del trimestre anterior.
Se utiliza una declaración IF para determinar si la variación es menor o igual a cero.
Si la variación es menor o igual a cero, devuelve "Rojo"; de lo contrario, devuelve "Verde".

Costo Total: Esta medida calcula el costo total restando la utilidad del ingreso y formatea el resultado para mostrarlo en millones de unidades monetarias.
Se calcula el ingreso total y la utilidad total utilizando la función CALCULATE, considerando todos los filtros excepto los de la tabla de calendario (ALL(Calendario)).
Luego, se realiza la resta entre el ingreso y la utilidad.
El resultado se formatea utilizando la función FORMAT para mostrar el valor en millones de unidades monetarias, seguido del símbolo de la moneda (💶).

Costo Y&Q Actual: Esta medida calcula el costo del trimestre actual.
Se calcula el ingreso total y la utilidad total, y luego se realiza la resta entre ambos.

Costo PQ (Costo del Trimestre Anterior): Esta medida calcula el costo del trimestre anterior.
Utiliza la función DATEADD para restar un trimestre a la fecha actual, luego calcula el ingreso total y la utilidad total de ese trimestre y finalmente realiza la resta entre ambos.

Estas medidas son útiles para calcular y visualizar indicadores financieros importantes, como la variación de costos y el costo total, lo que permite una mejor comprensión de los datos financieros en Power BI.
Ejemplos usados:

Medidas como
Icono Costo =

VAR ValorPrevio = [Costo PQ]

VAR Valor_Actual=[Costo Y&Q Actual]

VAR Valor =DIVIDE(Valor_Actual-ValorPrevio,ValorPrevio)

VAR Resultado =

IF(

Valor < 0 ,

UNICHAR( 128078 ) ,

UNICHAR( 128077 )

)

RETURN

Resultado

Color Costo =

VAR ValorPrevio = [Costo PQ]

VAR Valor_Actual=[Costo Y&Q Actual]

VAR Valor =DIVIDE(Valor_Actual-ValorPrevio,ValorPrevio)

VAR Resultado=IF(Valor<=0,"Red","Green")




return

Resultado

Costo_Total =

var Ingreso=CALCULATE(

SUM( 'Finanzas ETL'[Ingresos] ),ALL(Calendario)

)  / 1000000

var Utilidad=CALCULATE(

SUM( 'Finanzas ETL'[Utilidad] ),ALL(Calendario)

)  / 1000000

var resta=Ingreso-Utilidad

var Resultado=

"💶 "&FORMAT( resta,"#,##") & " Millones"

RETURN

Resultado

Costo Y&Q Actual =

var Ingreso=CALCULATE(

SUM( 'Finanzas ETL'[Ingresos] )

)  / 1000000

var Utilidad=CALCULATE(

SUM( 'Finanzas ETL'[Utilidad] )

)  / 1000000

var resta=Ingreso-Utilidad

RETURN

resta

Costo PQ =

var Ingreso=CALCULATE(

SUM( 'Finanzas ETL'[Ingresos]), DATEADD('Finanzas ETL'[Fecha],-1,QUARTER)

)  / 1000000

var Utilidad=CALCULATE(

SUM( 'Finanzas ETL'[Utilidad] ), DATEADD('Finanzas ETL'[Fecha],-1,QUARTER)

)  / 1000000

var resta=Ingreso-Utilidad

RETURN




resta
![variacion](https://github.com/vicente2121/Analisis_negocio/assets/72566296/56d69429-9c7f-46a1-8600-6b171234884d)

## Visualización de Datos y Toque Personal

Con el modelado de datos completo, nos adentramos en la visualización de datos en Power BI. Mostramos cómo utilizar las nuevas tarjetas visuales para condensar múltiples opciones en un solo lugar, proporcionando una visión rápida y clara de los datos. Exploramos la configuración de etiquetas y colores personalizados para mejorar la comprensión y destacamos la función![OBEJTO NATIVO BARRAS ibcs](https://github.com/vicente2121/Analisis_negocio/assets/72566296/c75f7cbb-b4e3-4c99-ad97-037a864c790c)
 overlap para comparar proyecciones con resultados reales de manera efectiva.![overlap](https://github.com/vicente2121/Analisis_negocio/assets/72566296/7fd7d30c-c6fe-429e-b3cd-17e023b5b84a)


## Conclusiones y Próximos Pasos

En conclusión, dominar la lógica, ETL y modelado de datos en Power BI es esencial para desbloquear todo el potencial de tus análisis. Al comprender la lógica detrás de cada paso del proceso y aplicar técnicas avanzadas de transformación y modelado, puedes crear informes impactantes y tomar decisiones informadas. ¡Acompáñanos en nuestro próximo viaje de análisis de datos con Power BI y continúa explorando las infinitas posibilidades que ofrece esta poderosa plataforma!

Link de mi reporte:https://www.novypro.com/project/análisis-de-negocio

Link Power BI:https://app.powerbi.com/view?r=eyJrIjoiNDhlZDkyNjktMzY5OC00NzU2LWFlZGUtMzgzZWY1ZDFiZGJjIiwidCI6IjkxMTVmY2FmLWE5NGQtNDBiMS1hM2JhLWIwNjJjODA1NTVlMCIsImMiOjl9

Link YouTube: https://youtu.be/A-yclzq0-9U
