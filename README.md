## Tutorial Hadoop con Docker

# Instrucciones para ejecutar Hadoop MapReduce con un archivo `.txt` usando Docker

Este tutorial te guía para ejecutar un trabajo MapReduce de ejemplo sobre un archivo `.txt` utilizando Hadoop dentro de un contenedor Docker.

## Requisitos Previos

- Docker instalado en tu sistema.
- Archivo `input.txt` con datos para procesar.
- Imagen de Hadoop disponible (por ejemplo: `sequenceiq/hadoop-docker:2.7.1`).

## 1.- Clonar el repositorio Docker-Hadoop de Github
-Ir al repositorio `https://github.com/big-data-europe/docker-hadoop`

-Dar click en Code y después Download ZIP 

-Colocar en una carpeta y abrir la carpeta en terminal o desde la terminal

## 2.- Iniciar el contenedor de Docker
-Abrir una terminal en la carpeta docker-hadoop y ejecutar: `docker-compose up -d` 
-para verificar que los contenedores han sido iniciados ejecutar: `docker ps`

## 3.- Entrar al nodo maestro
-Ejecutar `docker exec -it namenode bash` para acceder al nodo maestro
-Tenemos que crear la caperta `/user/root/`, ya que hadoop trabaja con esta estructura definida, para lo anterior ejecutamos: `hdfs dfs -mkdir -p /user/root/`.

verificar si se creó correctamente con 

`hdfs dfs -ls /user/`

