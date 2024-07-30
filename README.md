# STUDENT DATABASE

## Learn SQL by Building a Student Database: Part 1

En este tutorial se construyó y gestionó una base de datos de estudiantes utilizando SQL y PostgreSQL. 
A través de comandos SQL, se creó tablas con claves primarias y foráneas, se realizó la inserción y la consulta de datos, además la actualización y eliminación de registros.
Por otra parte, se utilizó Bash para automatizar tareas y gestionar permisos de archivos.

## Comandos Ejecutados

### Paso 1: Iniciar la terminal
En el terminal bash se ejecuta el siguiente comando:
```bash
echo hello SQL
```
La terminal muestra el siguiente mensaje: ` hello SQL `

### Paso 2: Iniciar sesión en terminal de SQL
En el terminal bash se ejecuta el siguiente comando:
```bash 
psql --username=freecodecamp --dbname=postgres
```
Se visualiza esto en la terminal:
```
Border style is 2.
Title is " ".
Pager usage is off.
psql (12.17 (Ubuntu 12.17-1.pgdg22.04+1))
SSL connection (protocol: TLSv1.3, cipher: TLS_AES_256_GCM_SHA384, bits: 256, compression: off)
Type "help" for help.
```

### Paso 3: Visualizar las bases de datos existentes
En el terminal de PostgresSQL se escribe el siguiente comando abreviado:
```md
postgres=> \l
```
Este comando muestra una lista de las bases de datos existentes.
![Imagen1](https://github.com/user-attachments/assets/7e4392b7-cf52-4f14-81c5-2bd664d5a752)

### Paso 4: Crear una base de datos
Se requiere crear una nueva base de datos con el nombre de **_students_**, para ello se ejecuta el siguiente comando:
```md
postgres=> CREATE DATABASE students;
```
La terminal muestra el mensaje de confirmación `CREATE DATABASE` que indica que la base de datos fue creada exitosamente.

### Paso 5: Comprobar que la base de datos está creada
En el listado de base de datos comprobamos que se encuentre la **_base de datos students_** que creamos.
```md
postgres=> \l
```
![Sin título](https://github.com/user-attachments/assets/0463ec5f-eb2d-4b05-b57f-be00f8f9656f)

### Paso 6: Conectar a la base de datos students
Nos conectamos a la **_base de datos students_** para comenzar a agregar tablas en ella
```md
postgres=> \c students
```
Se observa en la terminal que nos hemos conectado a la base de datos de manera exitosa.

### Paso 7: Crear tablas
Los archivos CSV tienen un grupo de estudiantes con información sobre ellos y algunos cursos y especialidades. 
Es por ello que se **_crean 4 tablas:_**
  1. Tabla **_students_** con la información de los estudiantes.
  2. Tabla **_majors_** con la información sobre las especialidades.
  3. Tabla **_courses_** con la información sobre los cursos.
  4. Tabla **_majors_courses_** que contiene información de unión de las especialidades con los cursos.
     
Para ello se ejecutan los siguientes comandos:  
```md
students=> CREATE TABLE students();
students=> CREATE TABLE majors();
students=> CREATE TABLE courses();
students=> CREATE TABLE majors_courses();
```

### Paso 8: Verificar tablas
Se utiliza el comando abreviado de visualización para ver sus tablas
```md
students=> \d
```
Muestra la lista de tablas que hemos creado
![Imagen2](https://github.com/user-attachments/assets/a7813b51-04d3-4a68-a80a-3aef4c815c54)

### Paso 9: Crear columnas en la tabla students
El **_archivo Students.csv_** 


esto todavia falta
Sobre las columnas. El archivo Students.csv tiene cuatro campos; creará una columna para cada uno de ellos, así como una columna de ID. 
Agregue una columna a la tabla de estudiantes llamada Student_id. Dale un tipo de SERIAL para que incremente automáticamente y conviértelo en CLAVE PRIMARIA.









