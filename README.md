## Tutorial Hadoop con Docker

Instrucciones para ejecutar Hadoop MapReduce con un archivo `.txt` usando Docker

Este tutorial te guía para ejecutar un trabajo MapReduce de ejemplo sobre un archivo `.txt` utilizando Hadoop dentro de un contenedor Docker.

## Requisitos Previos

- Docker instalado en tu sistema.
- Archivo `input.txt` con datos para procesar.
- Imagen de Hadoop disponible (por ejemplo: `sequenceiq/hadoop-docker:2.7.1`).

## 1.- Clonar el repositorio Docker-Hadoop de Github
- Ir al repositorio `https://github.com/big-data-europe/docker-hadoop`

- Dar click en Code y después Download ZIP 

- Colocar en una carpeta y abrir la carpeta en terminal o desde la terminal

## 2.- Iniciar el contenedor de Docker
- Abrir una terminal en la carpeta docker-hadoop y ejecutar: `docker-compose up -d` 
- para verificar que los contenedores han sido iniciados ejecutar: `docker ps`

## 3.- Entrar al nodo maestro
- Ejecutar `docker exec -it namenode bash` para acceder al nodo maestro
- Tenemos que crear la caperta `/user/root/`, ya que hadoop trabaja con esta estructura definida, para lo anterior ejecutamos: `hdfs dfs -mkdir -p /user/root/`.

verificar si se creó correctamente con 

- `hdfs dfs -ls /user/`

### EJEMPLOS DE MAPREDUCE

## 1. Contar Palabras de un archivo txt

- Usaremos un archivo .jar que contiene las clases necesarias para ejecutar el algoritmo MapReduce. 

- Para este tutorial, descargaremos el archivo .jar listo para usar.

- Ir a `https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-mapreduce-examples/2.7.1/`

- Descargue el archivo con nombre `hadoop-mapreduce-examples-2.7.1-sources.jar `

- Mueva el archivo `hadoop-mapreduce-examples-2.7.1-sources.jar` a la misma carpeta donde esta el repositorio docker-hadoop.

## 2.- Seleccionar archivo txt 

- Usaremos un archivo txt del clásico libro “Dracula” como texto plano.
- Descargar el archivo de `https://github.com/hold-the-phone/classic_books_in_txt/tree/master/Texts`

- Mueva el archivo a la misma carpeta donde esta el repositorio docker-hadoop y abra la carpeta desde la terminal

## 3.- Copiar los archivos .jar y .txt al contenedor

- Para mover el archivo hadoop-mapreduce-examples-2.7.1-sources.jar ejecute

`docker cp hadoop-mapreduce-examples-2.7.1-sources.jar namenode:/tmp`

Haga lo mismo para el archivo Dracula_Stoker.txt

## 4.- Crea la carpeta de entrada dentro del contenedor namenode
- Ingrese al contenedor namenode ejecutando 

- `docker exec -it namenode bash`

- Despues

- `docker cp Dracula_Stoker.txt namenode:/tmp`

- Cree la carpeta del contador o input

- `hdfs dfs -mkdir /user/root/input_contador`
  
## 5.- Copie el archivo txt al HDFS

-Ejecute 

- `cd /tmp`
  
- Luego ejecute: 

- `hdfs dfs -put Dracula_Stoker.txt /user/root/input_contador`

## 6.- Ejecutar MapReduce

- En una sola linea de comando, ejecutar:

- `hadoop jar hadoop-mapreduce-examples-2.7.1-sources.jar org.apache.hadoop.examples.WordCount input_contador output_contador`

## 7.- Ver Resultados

- Ejecute

- `hdfs dfs -cat /user/root/output_contador/*`

- Puedes comprobar los resultados accediendo a la carpeta de salida: 

- `hdfs dfs -ls /user/root/output_contador`

- Para copiar los resultados a un archivo txt ejecutar:

- `hdfs dfs -cat /user/root/output_contador/part-r-00000 > /tmp/Dracula_wc.txt`

- Después ejecutamos:

 - `exit`

- Por último: 

- `docker cp namenode:/tmp/quijote_wc.txt .`

Ahora el archivo de texto esta en la carpeta del  repositorio docker-hadoop.

### ORDENAR TEMPERATURAS 

## 1.- Dercargar el archivo a trabajar

- Puedes obtener el archivo desde aqui:
  
- `https://github.com/Rkrahul04/Maximum_Temp_Calculation_mapreduce/blob/master/Dataset%20-%20Calculate%20Maximum%20Temperature/Temperature`
  
- 
Mueva el archivo `Temperature.txt` a la misma carpeta donde esta el repositorio docker-hadoop y abra la carpeta en terminal

## 2.- Copiar archivos al contenedor

-Para mover el archivo `hadoop-mapreduce-examples-2.7.1-sources.jar` ejecute

- `docker cp hadoop-mapreduce-examples-2.7.1-sources.jar namenode:/tmp `

- Si ya cuenta con este archivo en su nodo hadoop puedo omitir este paso

- Haga lo mismo para el archivo `Temperature.txt`

- `docker cp Temperature.txt namenode:/tmp `

## 3.- Crea la carpeta de entrada dentro del contenedor namenode

- Ingrese al contenedor namenode ejecutando 

- `docker exec -it namenode bash`

- Luego ejecute: 

- `hdfs dfs -mkdir /user/root/input_temperaturas`

## 4.- Copie su archivo .txt a HDFS

- Ejecute
- `cd /tmp `

- Después: 

- `hdfs dfs -put Temperature.txt /user/root/input_temperaturas`

## 5.- Ejecutar MapReduce

- Ejecute en una sola linea de comando

- `hadoop jar hadoop-mapreduce-examples-2.7.1-sources.jar org.apache.hadoop.examples.SecondarySort input_temperaturas output_temperaturas`

## 6.- Ver Resultados

- Ejecutar: 

- `hdfs dfs -cat /user/root/output_temperaturas/*`

- Para obtener los resultados en un archivo txt en la carpeta base, ejecutar
  
- `hdfs dfs -cat /user/root/output_temperaturas/part-r-00000 > /tmp/temperaturas_ordenadas.txt `

- Finalmente ejecute `exit` para salir del nodo

### Resolver Sudoku

## 1.- Descargar archivo 

- En este ejemplo resolveremos sudokus contenidos en un archivo de texto. El archivo lo puedes encontrar aqui:

- `https://drive.google.com/file/d/1m6uSyzNCQV1617fmhQyW59sMQ2DYef2E/view`

- Mueva el archivo hadoop-examples-0.20.205.0.jar a la misma carpeta donde esta el repositorio docker-hadoop.

## 2.- Archivo txt para procesar

- Descarge el archivo puzzle1.dta de aqui:

- `https://miguelevangelista.gitbook.io/herramientasavanzadas/ejemplos-de-mapreduce/resolver-sudoku`

- Coloquelo en la misma carpeta que el repositorio de Hadoop y abra la carpeta desde terminal

## 3.- Copiar los archivos .jar y .txt al contenedor

Para mover el archivo `hadoop-examples-0.20.205.0.jar` ejecute

`docker cp hadoop-examples-0.20.205.0.jar namenode:/tmp `

Si ya cuenta con este archivo en su nodo hadoop puedo omitir este paso

Haga lo mismo para el archivo puzzle1.dta

`docker cp puzzle1.dta namenode:/tmp `

## 4.-Ejecutar MapReduce

- Ingrese al contenedor namenode ejecutando 

`docker exec -it namenode bash`

- Primero ejecute: 

- `cd /tmp `

- Ejecutar

- `hadoop jar hadoop-examples-0.20.205.0.jar sudoku puzzle1.dta`

## 5.- Ver resultados

- Ejecutar: 

- `hadoop jar hadoop-examples-0.20.205.0.jar sudoku puzzle1.dta > solucion_puzzle1.txt `

- Después ejecutamos:

 - `exit`

- Por último, ejecuta: 

- `docker cp namenode:/tmp/solucion_puzzle1.txt .`

- Ahora el archivo de texto esta en la carpeta del repositorio docker-hadoop.



  
