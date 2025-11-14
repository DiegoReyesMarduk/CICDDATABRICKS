Proyecto databirkcs
el objetivo es crear pipeline/ETL a un fichero externo de internet y aplicar todo lo visto en el curso con la estructura medallion. bronze-silver-golden.

1. Fuente de datos:
import kagglehub

# Download latest versionw
path = kagglehub.dataset_download("stefanydeoliveira/summer-olympics-medals-1896-2024")

print("Path to dataset files:", path)


https://www.kaggle.com/datasets/stefanydeoliveira/summer-olympics-medals-1896-2024


<img width="1908" height="1808" alt="image" src="https://github.com/user-attachments/assets/c6bc1031-e56c-4da9-a9ed-984011ab81a3" />



import kagglehub

# Download latest version
path = kagglehub.dataset_download("rovnez/fc-26-fifa-26-player-data")

print("Path to dataset files:", path)


https://www.kaggle.com/datasets/rovnez/fc-26-fifa-26-player-data


<img width="1974" height="1753" alt="image" src="https://github.com/user-attachments/assets/5570f8bd-958c-42d8-ae80-150348e335e8" />

2. Una vez se importa el dataset a nuestro contenedor en  la capa row se procede a preparar el ambiente 

<img width="1399" height="765" alt="image" src="https://github.com/user-attachments/assets/a894a8bf-9ad8-485e-b880-c2ba65ab4b28" />


en donde se crearan todos nuestros schenmas , external location y tablas

<img width="1731" height="1776" alt="image" src="https://github.com/user-attachments/assets/5ad29208-b2da-4333-bdee-4df1f0381bfe" />

para ver mas, abrir el arechivo "Preparacion_Ambiente.dbc"

3. al terminar de preparar al ambiente y tener todas las tablas creadas se procedde a hacer la carga de la capa row a bronze
y se ejecuta el archivo "Extract_FC26.dbc" y "Extract_Olimpic.dbc"

<img width="1617" height="1617" alt="image" src="https://github.com/user-attachments/assets/970c1441-6cb7-4163-ac5c-357cee83907f" />

<img width="1445" height="1594" alt="image" src="https://github.com/user-attachments/assets/32d45f9e-cecb-46b2-8c51-64f3c5df4f68" />

Esto hace que se cree una copia igual a la original

4. Ahora se procede a ejecutar el archivo "Transform_FC26_&_Olimpic.dbc" en donde se hace la transformacion logica de los datos, aca es en donde se decide transformar los datos brutos a unos a los cuales se pueda analizar mas facilmente

<img width="1535" height="1551" alt="image" src="https://github.com/user-attachments/assets/33b7b23f-098a-4c97-97f1-fa8b726bec74" />

<img width="2457" height="1522" alt="image" src="https://github.com/user-attachments/assets/14be2d63-457c-4d97-ad27-215f98370e58" />


5. Una vez se haya limpiada y transformada la informacion se procede a dejar la informacion con un proposito, agregada y separada para ser usada en futuros dashboards.
Ver archivo "Load_FC26_&_Olimpic.dbc"

<img width="1482" height="1491" alt="image" src="https://github.com/user-attachments/assets/b6ea4c08-7efc-4b5a-9d97-76a0abd3e816" />
<img width="1523" height="1484" alt="image" src="https://github.com/user-attachments/assets/4127d8dd-21a7-4745-9288-21f8735e20ae" />


En esto consiste el proceso de ETL que se realizo en el curso, por obvias razones no se muestran la creacion de credenciales, contenedores,tokens y demas pasos que se realizan para poder interconectar los recursos de azure con databricks, asi mismo tampoco se adjunta la estructura de las tablas porque todo esto ya estan en los .dbc que se han nombrado en el paso a paso de esta ETL que ahora se mostrara evidencia  del proceso que hace GITHUB.

6. Paso de desarrolo a produccion y creacion de workflow a partir del .yaml

Este es el workflow que genera el .yaml una vez se programan los scripts en el archivo "deploy-notebook" 

<img width="3524" height="1233" alt="image" src="https://github.com/user-attachments/assets/657fe816-a012-4f96-a495-06bccc5ec904" />

Este proceso se genera una vez se programan los scripts y se cargan de la rama construction

<img width="1564" height="450" alt="image" src="https://github.com/user-attachments/assets/bc58e79f-d5a2-4a80-b1ee-4608f89878e7" />

una vez se modifica el script se deja un comentario y se procede a hacer el commit and push

<img width="1378" height="1882" alt="image" src="https://github.com/user-attachments/assets/83ce06e9-c59c-4fe5-965d-1d8c647ad493" />

esto hace que se deba ir a GITHUB y montar estos cambios de construccion a main

una vez se procede a cargar al main, git ejecuta una interfaz "Action" en donde se ejecuta y se valida paso a paso el codigo creado previamente en el .yaml

<img width="3799" height="1256" alt="image" src="https://github.com/user-attachments/assets/e8a43b32-c984-46d3-9021-24b62a91aa33" />

Una vez termina de ejecutarse esta interfaz, en databricks de produccion se crea el workflow automaticamente.

<img width="2545" height="1250" alt="image" src="https://github.com/user-attachments/assets/9208a6ab-d10e-4c9c-861b-f5b32a2e41a9" />

7. Dashboard
para este caso se decide utilizar la misma herramienta de databricks para hacer un pequeño cuadro y mostrar los datos que se analizaron y mostrar su relevancia.

Este para olimpics  
<img width="921" height="534" alt="image" src="https://github.com/user-attachments/assets/5fa911f7-3e6b-4536-b103-3564d500ef83" />

Este para FC
<img width="921" height="495" alt="image" src="https://github.com/user-attachments/assets/fde9a38a-7638-43b5-97c5-7525f7ac3c7d" />


**Proyecto**: Data Engineering - Arquitectura Medallion  
**Tecnología**: Azure Databricks + Delta Lake + CI/CD  
**Última actualización**: 2025





