# GettingAndCleaningData
El script analiza los datos de UCI HAR Dataset . Se supone que el archivo se extrae al directorio de trabajo.

Se utilizan los siguientes archivos del conjunto de datos inicial:

features.txt : incluye las descripciones de las características medidas
train / X_train.txt : incluye las medidas de las características en el conjunto de trenes (una fila - 1 medición de 561 características)
test / X_test.txt : incluye las medidas de las características en el conjunto de prueba
train / subject_train.txt : tema para cada medición del conjunto de trenes
test / subject_test.txt - sujeto para cada medición del conjunto de prueba
train / y_train.txt - actividad (de 1 a 6) para cada medición del conjunto de trenes
test / y_test.txt - actividad (de 1 a 6) para cada medición del conjunto de prueba
Cómo funciona el script
El guión comprende las siguientes etapas:

Descargas de R ids y descripciones de las características que se miden en el experimento desde el archivo features.txt .

Carga de forma independiente datos completos para trenes y conjuntos de prueba. Revoquemos estos procesos de carga considerando el juego de trenes:
a. Primero carga las medidas de X_train.txt como un marco de datos
b. Para estos marcos de datos, los nombres de las columnas se actualizan para que sean más fáciles de usar mediante la descripción de las funciones cargadas en la etapa anterior. ( PASO 4 : Etiquete adecuadamente el conjunto de datos con nombres de variables descriptivas del Proyecto del curso
c. Las etiquetas de actividad y los temas para las mediciones también se cargan desde los archivos train / y_train.txty train / subject_train.txt y se agregan al marco de datos como columnas separadas.

Se realizan pasos similares para el conjunto de datos de prueba y, finalmente, 2 filas de 2 marcos de datos se fusionan para formar un marco de datos con datos completos ( PASO 1 : Combinar el entrenamiento y los conjuntos de prueba para crear un conjunto de datos de asignación)

Para extraer mediciones que involucran solo valores de desviación estándar y media, el script usa grep, que busca nombres de columnas que incluyen "mean ()" o "std ()" (también se agrega la actividad y el asunto de las columnas al marco de datos filtrado, ya que son dimensiones importantes). Después de eso, se crea todo el nuevo marco de datos con solo las columnas necesarias. ( PASO 2 : Extraiga solo las mediciones de la media y la desviación estándar para cada medición de la asignación)

Para proporcionar valores descriptivos para las etiquetas de actividad, se agrega una nueva variable "activitylabel" al conjunto de datos, que es una variable de factor con los niveles mencionados en el archivo activity_labels.txt ( PASO 3 : Use nombres de actividad descriptivos para nombrar las actividades en el conjunto de datos de la asignación)

Crea un marco de datos fundido usando la etiqueta de actividad y el sujeto como identificadores, después de eso, los valores medios para todas las variables se calculan agrupados por actividad y tema usando la función dcast () y se crea un marco de datos ordenado. ( PASO 5 : Cree un segundo conjunto de datos ordenado e independiente con el promedio de cada variable para cada actividad y cada tema )
