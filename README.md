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
En la **_tabla students_** se crean las siguientes columnas:

1. **Columna student_id:** Se crea una columna llamada **_student_id_** de tipo **_SERIAL_** para que se incremente automáticamente y que sea **_PRIMARY KEY_**.
  ```md
  students=> ALTER TABLE students ADD COLUMN student_id SERIAL PRIMARY KEY;
  ```
2. **Columna first_name:** Crea una columna **_first_name_** en la tabla **_students_** que es de tipo **_VARCHAR(50)_** y con la restricción **_NOT NULL_**.
  ```md
  students=> ALTER TABLE students ADD COLUMN first_name VARCHAR(50) NOT NULL;
  ```
3. **Columna last_name:** Posee el mismo tipo de datos y longitud máxima que **_first_name_** y con la restricción **_NOT NULL_**.
 ```md
  students=> ALTER TABLE students ADD COLUMN last_name VARCHAR(50) NOT NULL;
  ```
4. **Columna major_id:** Esta columna es de tipo de dato **_INT_**.
 ```md
  students=> ALTER TABLE students ADD COLUMN major_id INT;
  ```
5. **Columna gpa:** La última columna **_gpa_** en la tabla **_students_** es de tipo **_NUMERIC(2,1)._**
 ```md
  students=> ALTER TABLE students ADD COLUMN gpa NUMERIC(2,1);
  ```

### Paso 10: Ver detalles de la tabla students
Se utiliza el comando de acceso directo para mostrar los detalles de la tabla de **_students_**.
 ```md
  students=> \d students
  ```

![Imagen1](https://github.com/user-attachments/assets/3e6e6d73-6097-436d-9376-6ba83b80ea10)

### Paso 11: Crear columnas en la tabla majors
En la **_tabla majors_** se crean las siguientes columnas:

1. **Columna major_id:** Se crea una columna llamada **_major_id_** de tipo **_SERIAL_** y que sea **_PRIMARY KEY_** de la **_tabla majors_**  .
  ```md
  students=> ALTER TABLE majors ADD COLUMN major_id SERIAL PRIMARY KEY;
  ```
2. **Columna major:** Crea una columna **major** que es de tipo **_VARCHAR(50)_** y con la restricción **_NOT NULL_**.
  ```md
  students=> ALTER TABLE majors ADD COLUMN major VARCHAR(50) NOT NULL;
  ```

### Paso 12: Ver detalles de la tabla majors
Se utiliza el comando de acceso directo para mostrar los detalles de la tabla de **_majors_**.
 ```md
  students=> \d majors
  ```
![Imagen3](https://github.com/user-attachments/assets/1f110bed-bba9-40f4-8f27-acdf1be0fcb4)

### Paso 13: Establecer la llave foránea (foreign key) en la tabla de students
Se establezce la **_columna major_id_** de la tabla students como una **_clave foránea_** que hace referencia a la **_columna major_id_** de la tabla **_majors_**. 
`ALTER TABLE <nombre_tabla> ADD FOREIGN KEY(<nombre_columna>) REFERENCES <nombre_tabla_referenciada>(<nombre_columna_referenciada>);`
 ```md
  students=> ALTER TABLE students ADD FOREIGN KEY(major_id) REFERENCES majors(major_id);
 ```

### Paso 14: Verificar que la llave foránea se ha establecido en la tabla de students
Para verificar que la llave foránea se ha establecido en la **_tabla students_** se utiliza el comando abreviado de visualización para ver los detalles tablas.

![Imagen4](https://github.com/user-attachments/assets/30207928-bec8-4c61-9894-c9cb03cd9757)

### Paso 15: Crear columnas en la tabla courses
En la **_tabla courses_** se crean las siguientes columnas:

1. **Columna course_id:** Se crea una columna llamada **_course_id_** de tipo **_SERIAL_** y que sea la **_PRIMARY KEY_**.
  ```md
  students=> ALTER TABLE courses ADD COLUMN course_id SERIAL PRIMARY KEY;
  ```
2. **Columna course:** Crea una columna **course** que es de tipo **_VARCHAR(100)_** y con la restricción **_NOT NULL_**.
  ```md
  students=> ALTER TABLE courses ADD COLUMN course VARCHAR(100) NOT NULL;
  ```
### Paso 16: Ver detalles de la tabla courses
Se utiliza el comando de acceso directo para mostrar los detalles de la tabla de **_courses_**.
 ```md
  students=> \d courses
  ```
![Imagen5](https://github.com/user-attachments/assets/abac54b5-14f7-40e5-9b8a-33f4a601ea42)

### Paso 17: Crear columnas en la tabla majors_courses
La **_tabla de unión majors_courses_** tiene dos columnas, cada una hace referencia a la clave primaria de dos tablas relacionadas.

1. **Columna major_id:** Se crea una columna llamada **_major_id_** de tipo **_INT_**.
  ```md
  students=> ALTER TABLE majors_courses ADD COLUMN major_id INT;
  ```
2. **Columna course_id:** Crea una columna **course_id** que es de tipo **_INT_**.
  ```md
  students=> ALTER TABLE majors_courses ADD COLUMN course_id INT;
  ```

### Paso 18: Establecer llaves foráneas en la tabla majors_courses

1. Se establece la **_columna major_id_** de la **_tabla majors_courses_** como una **_llave foránea_** que hace referencia a la **_columna major_id_** de la **_tabla majors_**.
  ```md
  students=> ALTER TABLE majors_courses ADD FOREIGN KEY(major_id) REFERENCES majors(major_id);
  ```
2. Se establece la **_columna course_id_** como una **_llave foránea_**  que haga referencia a la otra **_columna course_id_** de la **_tabla courses_**.
  ```md
  students=> ALTER TABLE majors_courses ADD FOREIGN KEY(course_id) REFERENCES courses(course_id);
  ```

### Paso 19: Ver detalles de la tabla majors_courses
Se utiliza el comando de acceso directo para mostrar los detalles de la tabla de **_majors_courses_**. Y se verificar que la llaves foránea se establecieron de forma correcta.
 ```md
  students=> \d majors_courses
  ```
![Imagen6](https://github.com/user-attachments/assets/31c323d3-e48b-420e-9013-9a5a97eab128)

### Paso 20: Crear llave primaria compuesta en majors_courses
Se crea una **_llave primaria compuesta_**  que utilice más de una columna como par único de la siguiente manera: `ALTER TABLE <nombre_tabla> ADD PRIMARY KEY(<nombre_columna>, <nombre_columna>);` 
 ```md
  students=> ALTER TABLE majors_courses ADD PRIMARY KEY(major_id, course_id);
  ```
Con el uso comando de acceso directo para mostrar los detalles de la tabla de **_majors_courses_**, se verificar que la **_llave primaria compuesta_** se estableció de forma correcta.
 ```md
  students=> \d majors_courses
  ```
![Imagen7](https://github.com/user-attachments/assets/8f2bb60b-1f45-449d-8752-af0b9869b610)

### Paso 21: Insertar datos en la tabla majors





