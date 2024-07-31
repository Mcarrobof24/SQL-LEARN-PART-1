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

### Paso 21: Insertar datos en la tablas
Para insertar datos en nuestras tablas se utiliza la siguiente sintáxis `INSERT INTO <nombre_tabla>(<nombre_columna>) VALUES(<valor>);`
1. **INSERT INTO en la tabla students**
 ```md
  students=> INSERT INTO students(first_name, last_name, major_id, gpa) VALUES('Rhea', 'Kellems', 1, 2.5);
  ```
2. **INSERT INTO en la tabla majors**
 ```md
  students=> INSERT INTO majors(major) VALUES('Database Administration');
  ```
3.  **INSERT INTO en la tabla courses**
 ```md
  students=> INSERT INTO courses(course) VALUES('Data Structures and Algorithms');
  ```
4.  **INSERT INTO en la tabla majors_courses**
 ```md
  students=> INSERT INTO majors_courses(major_id, course_id) VALUES(1, 1);
  ```

### Paso 22: Usar SELECT para mostrar detalles de las tablas
Utilice **_SELECT_** para ver todos los datos de las tablas.
 ```md
  students=> SELECT * FROM students;
  students=> SELECT * FROM majors;
  students=> SELECT * FROM courses;
  students=> SELECT * FROM majors_courses;
  ```
### Paso 23: Añadir datos a las tablas mediante script
1. Se utiliza el **_comando touch_** en la terminal de bash para crear un archivo llamado **_insert_data.sh_** en la carpeta de tu proyecto.
 ```sh
  camper: /project$ touch insert_data.sh
  ```
2. Se utiliza el **_comando chmod +x_** para darle nuevos permisos ejecutables de script.
 ```sh
  camper: /project$ chmod +x insert_data.sh
  ```
3. En el archivo **_insert_data.sh_** inserta la primera línea lo siguiente: **_`#!/bin/bash`_**
   
4. Se añade el comentario: **_`#Script to insert data from courses.csv and students.csv into students database.`_** en el archivo **_insert_data.sh_**
   
5. El comando de terminal **_`cat <filename>`_** imprime el contenido de un archivo. Se escribe **_`cat courses.csv`_** debajo del comentario anterior para mostrar los datos del **_archivos courses.csv_**.

6. Se ejecuta el script para ver si se imprime el contenido del archivo.
 ```sh
  camper: /project$ ./insert_data.sh
  ```
![Imagen7](https://github.com/user-attachments/assets/62bdf279-6dd3-4bdc-bbbe-ba9bc5495f39)

### Paso 24: Utilizar el bucle WHILE 
Para canalizar la salida se utiliza el bucle WHILE para recorrer las filas una a la vez. Cada nueva línea se leerá en las variables `MAJOR` y `COURSE`, use `echo` para imprimir la variable `MAJOR`.
 ```sh
  cat courses.csv | while read MAJOR COURSE
  do
    echo $MAJOR
  done
 ```

### Paso 25: Declarar y establecer IFS(Internal Field Separator o Separador de campo interno)
1. Se utiliza IFS para determinar los límites de las palabras y se declara la IFS en la terminal:
 ```sh
  camper: /project$ declare -p IFS
  ```
2. Se establece IFS entre los `comandos while y read` de la siguiente manera:
 ```sh
  cat courses.csv | while IFS="," read MAJOR COURSE
  do
    echo $MAJOR
  done
 ```

### Paso 26: Agregar comentarios
Se agrega comentarios de una línea en el bucle `WHILE` en el siguiente orden:
 ```sh
  cat courses.csv | while IFS="," read MAJOR COURSE
  do
    # get major_id

    # if not found

    # insert major

    # get new major_id

    # get course_id

    # if not found

    # insert course

    # get new course_id

    # insert into majors_courses

  done
 ```

### Paso 27: Agregar el comando PSQL
Se agrega el siguiente **_`comando PSQL`_** que permite consultar la base de datos desde el script.

 ```sh
  PSQL="psql -X --username=freecodecamp --dbname=students --no-align --tuples-only -c"
 ```
Las partes importantes son el `username`, el nombre de la base de datos `dbname` y el indicador -c que sirve para ejecutar un solo comando y salir. 

### Paso 28: Crear la variable MAJOR_ID
Se puede consultar la base de datos usando la variable PSQL de esta manera: **_`$($PSQL "<query_here>")`_**

Este código se ejecuta en un subshell, que es un proceso bash independiente. Debajo del comentario **_`# get major_id`_** se crea una variable **_`MAJOR_ID`_**. Se establece una consulta que obtiene el **_`major_id`_**  del **_`MAJOR`_** actual en el bucle.
```sh
  cat courses.csv | while IFS="," read MAJOR COURSE
  do
    # get major_id

    MAJOR_ID=$($PSQL "SELECT major_id FROM majors WHERE major='$MAJOR'")

  done
 ```

### Paso 29: Imprimir la variable MAJOR_ID utilizando echo
Se usa echo para imprimir la variable **_`MAJOR_ID`_** y poder ver su valor cuando ejecute el script.
```sh
  cat courses.csv | while IFS="," read MAJOR COURSE
  do
    # get major_id

    MAJOR_ID=$($PSQL "SELECT major_id FROM majors WHERE major='$MAJOR'")
    echo $MAJOR_ID

  done
 ```
### Paso 30: Utilizar IF para comprobar si una variable está vacía.
Se agrega una condición if para verificar si la variable **_`MAJOR_ID`_** está vacía. Se puede hacerlo con esta prueba: **_`[[ -z $MAJOR_ID ]]`_**.
```sh
  cat courses.csv | while IFS="," read MAJOR COURSE
  do
    # get major_id

    MAJOR_ID=$($PSQL "SELECT major_id FROM majors WHERE major='$MAJOR'")
    echo $MAJOR_ID

    # if not found
    if [[ -z $MAJOR_ID ]]
    then
  done
 ```
### Paso 31: Crear la variable INSERT_MAJOR_RESULT
Se crea una variable INSERT_MAJOR_RESULT, se establece su valor en una consulta que inserte la major (especialización) actual en la base de datos. Y se agrega el `echo` a la variable para imprimirla.
```sh
  cat courses.csv | while IFS="," read MAJOR COURSE
  do
    # get major_id

    MAJOR_ID=$($PSQL "SELECT major_id FROM majors WHERE major='$MAJOR'")
    echo $MAJOR_ID

    # if not found
    if [[ -z $MAJOR_ID ]]
    then
    # insert major
    INSERT_MAJOR_RESULT=$($PSQL "INSERT INTO majors(major) VALUES('$MAJOR')")
    echo $INSERT_MAJOR_RESULT 
  done
 ```
### Paso 32: Copiar el archivo courses.csv
Se usa el **_`comando copiar (cp)`_** para copiar el archivo **_courses.csv_** en un nuevo archivo llamado **_courses_test.csv_**.
```sh
  camper: /project$ cp courses.csv courses_test.csv
 ```
En el archivo **_courses_test.csv_** se elimina todas las líneas excepto las cinco primeras. El archivo debería verse así:
```sh
  major,course
  Database Administration,Data Structures and Algorithms
  Web Development,Web Programming
  Database Administration,Database Systems
  Data Science,Data Structures and Algorithms
 ```

### Paso 33: Cambiar el script a analizar
En el archivo **_`insert_data.sh`_** se cambia el **_`comando cat`_** para recorrer el archivo de prueba **_`courses_test.csv`_** en lugar del completo.
```sh
  cat courses_test.csv | while IFS="," read MAJOR COURSE
 ```
Al ejecutar el script se revisará los datos de prueba e insertará un major (especialidad) en la base de datos cada vez que no encuentre ninguna allí e imprimirá las variables **_`MAJOR_ID`_** e **_`INSERT_MAJOR_RESULT`_**.

Ya no es necesario imprimir el ID, así que se elimina la línea echo **_`$MAJOR_ID`_**.

### Paso 34: Eliminar tablas con TRUNCATE
Se utiliza **_`TRUNCATE`_** para eliminar todos los datos de una tabla. Se elimina todos los datos de todas las **_`tablas`_** ingresando **_`TRUNCATE <table1>, <table2>, <table3>;`_**
```sh
  students=> TRUNCATE majors, students, courses, majors_courses;
 ```
### Paso 35: Agregar IF major
Se agrega una condición if en la parte superior de su bucle que verifique si **_`$MAJOR != major`_**.
```sh
  do
  if [[ $MAJOR != major ]]
  then
    # get major_id
    MAJOR_ID=$($PSQL "SELECT major_id FROM majors WHERE major='$MAJOR'")
    # if not found
    if [[ -z $MAJOR_ID ]]
    then
      # insert major
      INSERT_MAJOR_RESULT=$($PSQL "INSERT INTO majors(major) VALUES('$MAJOR')")
      echo $INSERT_MAJOR_RESULT
      # get new major_id
    fi
    # get course_id
    # if not found
    # insert course
    # get new course_id
    # insert into majors_courses
  fi
done
 ```

### Paso 36: Eliminar INSERT_MAJOR_RESULT
Se borra la línea echo **_`$INSERT_MAJOR_RESULT`_**
```sh
  do
  if [[ $MAJOR != major ]]
  then
    # get major_id
    MAJOR_ID=$($PSQL "SELECT major_id FROM majors WHERE major='$MAJOR'")
    # if not found
    if [[ -z $MAJOR_ID ]]
    then
      # insert major
      INSERT_MAJOR_RESULT=$($PSQL "INSERT INTO majors(major) VALUES('$MAJOR')")
      # get new major_id
    fi
    # get course_id
    # if not found
    # insert course
    # get new course_id
    # insert into majors_courses
  fi
done
 ```
### Paso 37: Añadir IF en INSERT_MAJOR_RESULT
Se agregue una declaración **_`if`_** que verifique si la variable es igual a INSERT 0 1, se utiliza **_`echo`_** para imprimir el mensaje **_`Inserted into majors, $MAJOR"`_**.
```sh
  do
  if [[ $MAJOR != major ]]
  then
    # get major_id
    MAJOR_ID=$($PSQL "SELECT major_id FROM majors WHERE major='$MAJOR'")
    # if not found
    if [[ -z $MAJOR_ID ]]
    then
      # insert major
      INSERT_MAJOR_RESULT=$($PSQL "INSERT INTO majors(major) VALUES('$MAJOR')")
      if [[ $INSERT_MAJOR_RESULT == "INSERT 0 1" ]]
      then
        echo "Inserted into majors, $MAJOR"
      fi
      # get new major_id
    fi
    # get course_id
    # if not found
    # insert course
    # get new course_id
    # insert into majors_courses
  fi
done
 ```

### Paso 38: Añadir MAJOR_ID, COURSE_ID, INSERT_COURSE_RESULT 
1. Se establece la variable **_`MAJOR_ID`_** en una consulta que obtenga el nuevo **_`major_id`_** de la base de datos.
2. Se agrega una variable **_`COURSE_ID`_** que obtenga el **_`courses_id`_** de la base de datos.
3. Se escribe una declaración **_`if`_** que verifique si la consulta estaba vacía para que pueda insertar el curso si es necesario.
4. Debajo del comentario de # insert course, se crea una variable **_`INSERT_COURSE_RESULT`_** que inserte el curso en la base de datos.
5. Debajo de la variable **_`INSERT_COURSE_RESULT`_**, se agrega una condición **_`if`_** que verifique si lo es e imprima le mensaje **_`"Inserted into majors,  $COURSE" usando echo`_**.
```sh
  do
  if [[ $MAJOR != major ]]
  then
    # get major_id
    MAJOR_ID=$($PSQL "SELECT major_id FROM majors WHERE major='$MAJOR'")
    # if not found
    if [[ -z $MAJOR_ID ]]
    then
      # insert major
      INSERT_MAJOR_RESULT=$($PSQL "INSERT INTO majors(major) VALUES('$MAJOR')")
      if [[ $INSERT_MAJOR_RESULT == "INSERT 0 1" ]]
      then
        echo "Inserted into majors, $MAJOR"
      fi
      # get new major_id
      MAJOR_ID=$($PSQL "SELECT major_id FROM majors WHERE major='$MAJOR'")
    fi
    # get course_id
    COURSE_ID=$($PSQL "SELECT course_id FROM courses WHERE course='$COURSE'")

    # if not found
    if [[ -z $COURSE_ID ]]
    then
    # insert course
    INSERT_COURSE_RESULT=$($PSQL "INSERT INTO courses(course) VALUES('$COURSE')")
    if [[ $INSERT_COURSE_RESULT == "INSERT 0 1" ]]
    then
    echo "Inserted into courses, $COURSE"
    # get new course_id
    fi
    # insert into majors_courses
  fi
done
 ```

### Paso 39: Eliminar los datos en la tablas de forma automática
En la parte superior del archivo debajo de su variable PSQL, use **_`echo`_** para consultar la base de datos. En la consulta, trunque sus cuatro tablas en este orden: **_`students, majors, courses, majors_courses`_**.
```sh
  echo $($PSQL "TRUNCATE students, majors, courses, majors_courses")
 ```

### Paso 40: Añadir COURSE_ID, INSERT_MAJORS_COURSES_RESULT
1. Debajo de su comentario **_`# get new course_id`_**, establezca **_`COURSE_ID `_** en el **_`id_courses`_** recién insertado.
2.  Se crea una variable **_`INSERT_MAJORS_COURSES_RESULT`_** que se utiliza con las variables **_`MAJOR_ID y COURSE_ID`_**.
3. Se añade una condición **_`if`_** que compruebe si es igual a INSERT 0 1.
```sh
  do
  if [[ $MAJOR != major ]]
  then
    # get major_id
    MAJOR_ID=$($PSQL "SELECT major_id FROM majors WHERE major='$MAJOR'")
    # if not found
    if [[ -z $MAJOR_ID ]]
    then
      # insert major
      INSERT_MAJOR_RESULT=$($PSQL "INSERT INTO majors(major) VALUES('$MAJOR')")
      if [[ $INSERT_MAJOR_RESULT == "INSERT 0 1" ]]
      then
        echo "Inserted into majors, $MAJOR"
      fi
      # get new major_id
      MAJOR_ID=$($PSQL "SELECT major_id FROM majors WHERE major='$MAJOR'")
    fi
    # get course_id
    COURSE_ID=$($PSQL "SELECT course_id FROM courses WHERE course='$COURSE'")

    # if not found
    if [[ -z $COURSE_ID ]]
    then
    # insert course
    INSERT_COURSE_RESULT=$($PSQL "INSERT INTO courses(course) VALUES('$COURSE')")
    if [[ $INSERT_COURSE_RESULT == "INSERT 0 1" ]]
    then
    echo "Inserted into courses, $COURSE"

    # get new course_id
    COURSE_ID=$($PSQL "SELECT course_id FROM courses WHERE course='$COURSE'")
    fi

    # insert into majors_courses
    INSERT_MAJORS_COURSES_RESULT=$($PSQL "INSERT INTO majors_courses(major_id, course_id) VALUES($MAJOR_ID, $COURSE_ID)")
     if [[ $INSERT_MAJORS_COURSES_RESULT == "INSERT 0 1" ]]
    then
      echo "Inserted into majors_courses, $MAJOR : $COURSE"
    fi
  fi
done
 ```
Cuando se ejecuta el script, las tablas se truncan y luego pasar por el bucle y se agregan todos los datos de **_`cursos_test.csv`_** a las tres tablas de la base de datos.

### Paso 41: Copiar el archivo students.csv
Se debe agregar todo el contenido del archivo **_`students.csv`_**. En la terminal, se usa el **_`comando cp`_** para copiar el archivo **_`students.csv`_** en un archivo llamado **_`students_test.csv`_**.
```sh
camper: /project$ cp students.csv students_test.csv
```
En el archivo **_`students_test.csv`_**, se elimina todo menos las primeras cinco líneas.

### Paso 42: Imprimir el contenido del archivo de prueba `students_test.csv`
Se usa el **_`comando cat`_** para imprimir el nuevo archivo de prueba. Se canalice los resultados en un bucle **_`while`_**, se establece **_`IFS`_** en una coma nuevamente y se usa **_`read`_** para crear las variables **_`FIRST, LAST, MAJOR y GPA`_** a partir de los datos. En el bucle, se usa **_`echo`_** para imprimir la variable **_`FIRST`_**.

```sh
  cat students_test.csv | while IFS="," read FIRST LAST MAJOR GPA
  do
    echo $FIRST
  done
 ```

### Paso 43: Agregar IF y comentarios
1. Se agrega una condición if al bucle que verifica si la variable **_`FIRST`_** no es igual a **_`first_name`_**.
2. Se agrega cuatro comentarios de una sola línea en su bucle: **_`get major_id, if not found, set to null and insert student`_**
```sh
  cat students_test.csv | while IFS="," read FIRST LAST MAJOR GPA
  do
    if [[ $FIRST != "first_name" ]]
    then
    # get major_id
   
    # if not found
   
    # set to null
   
    # insert student
  
  fi
  done
 ```

### Paso 44: Agregar MAJOR_ID, INSERT_STUDENT_RESULT, IF para comprobar si la variable está vacía
1. Se establece la variable **_`MAJOR_ID`_** en una consulta que obtenga el **_`major_id`_** para la major (especialidad) actual de los estudiantes. Y se usa **_`echo`_** para imprimir la variable para que pueda ver si está funcionando.
2. Se agrega un **_`if`_** que verifique si la variable está vacía.
3. Se establece la variable **_`MAJOR_ID`_** en nulo para poder usarla para insertar los datos.
4. Se crea una variable **_`INSERT_STUDENT_RESULT`_** que agrega al estudiante a la base de datos. Se agrega las columnas en el orden en que aparecen en los datos y asegúrese de poner solo las dos columnas VARCHAR entre comillas simples.
5. Debajo de la variable **_`INSERT_STUDENT_RESULT`_**, agrega una declaración **_`if`_** que verifique si es igual a **_`INSERT 0 1`_**.
6. 
```sh
  cat students_test.csv | while IFS="," read FIRST LAST MAJOR GPA
  do
    if [[ $FIRST != "first_name" ]]
    then
    # get major_id
    MAJOR_ID=$($PSQL "SELECT major_id FROM majors WHERE major='$MAJOR'")
    echo $MAJOR_ID
   
    # if not found
     if [[ -z $MAJOR_ID ]]
    then
      # set to null
      MAJOR_ID=null
    fi
   
    # insert student
    INSERT_STUDENT_RESULT=$($PSQL "INSERT INTO students(first_name, last_name, major_id, gpa) VALUES('$FIRST', '$LAST', $MAJOR_ID, $GPA)")
    if [[ $INSERT_STUDENT_RESULT == "INSERT 0 1" ]]
    then
      echo "Inserted into students, $FIRST $LAST"
    fi
  fi
  done
 ```

### Paso 45: Cambiar el script a los archivos originales
1. Se cambia la línea **_`cat cursos_test.csv`_** para usar el archivo original nuevamente.
 ```sh
  cat courses.csv | while IFS="," read MAJOR COURSE
  ```
2. Se cambia la línea **_`students_test.csv `_** para usar el archivo original.
 ```sh
  cat students.csv | while IFS="," read FIRST LAST MAJOR GPA
  ```

### Paso 46: Ejecutar el script
En la terminal bash se ejecuta **_`./insert_data.sh`_**  
 ```sh
  camper: /project$ ./insert_data.sh
  ```
Mediante la consulta SELECT se visualiza los datos de cada una de nuestras tablas
1. Tabla **_`students`_** tiene 31 filas.
 ```sh
  SELECT * FROM students;
  ```
![Imagen8](https://github.com/user-attachments/assets/5cb059bf-5f51-4c85-9a21-7a8d59ba713f)

2. Tabla **_`majors`_** tiene 7 filas.
 ```sh
  SELECT * FROM majors;
  ```
![Imagen9](https://github.com/user-attachments/assets/12e3c65a-1611-4e33-a9c8-2765ba597066)

3. Tabla **_`courses`_** tiene 17 filas.
 ```sh
  SELECT * FROM courses;
  ```
![Imagen10](https://github.com/user-attachments/assets/7ececd3a-b069-43fd-a29a-2e8a5f5a2dc0)

4. Tabla **_`majors_courses`_** tiene 28 filas.
 ```sh
  SELECT * FROM majors_courses;
  ```
![Imagen11](https://github.com/user-attachments/assets/28ffad95-db5f-4b31-b4dd-09ae01401526)

### Paso 47: Eliminar los archivos de prueba
En la terminal, se usa el comando de lista **_`ls`_** para verificar qué archivos hay en la carpeta de su proyecto. Se utiliza el **_`comando eliminar rm`_** para eliminar los archivos de prueba **_`students_test.csv y courses_test.csv`_**.
 ```sh
  camper: /project$ rm students_test.csv
  camper: /project$ rm courses_test.csv
  ```

### Paso 48: Exportar el contenido de la base de datos
La base de datos está terminada y se exportar su contenido a un archivo sql. Se utiliza el **_`comando pg_dump --clean --create --inserts --username=freecodecamp students > students.sql`_** en el terminal para exportar la base de datos en un archivo **_`students.sql`_**. En este se guardará todos los comandos necesarios para reconstruirla. 
 ```sh
  camper: /project$ pg_dump --clean --create --inserts --username=freecodecamp students > students.sql
  ```
El archivo **_`students.sql`_** se encuentra en la rama main de este repositorio donde podemos visualizar su contenido.









