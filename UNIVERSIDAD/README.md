1. Devuelve un listado con el primer apellido, segundo apellido y el nombre de todos los alumnos. El listado deberá estar ordenado alfabéticamente de menor a mayor por el primer apellido, segundo apellido y nombre.

    ```sql
      ~~~
      SELECT  CONCAT_WS(' ',nombre,apellido1,apellido2) AS alumnos FROM persona WHERE tipo='alumno' ORDER BY nombre,apellido1,apellido2 ASC;

        +-----------------------------+
        | alumnos                     |
        +-----------------------------+
        | Antonio Domínguez Guerrero  |
        | Daniel Herman Pacocha       |
        | Inma Lakin Yundt            |
        | Irene Hernández Martínez    |
        | Ismael Strosin Turcotte     |
        | José Koss Bayer             |
        | Juan Gutiérrez López        |
        | Juan Saez Vega              |
        | Pedro Heller Pagac          |
        | Ramón Herzog Tremblay       |
        | Salvador Sánchez Pérez      |
        | Sonia Gea Ruiz              |
        +-----------------------------+
        12 rows in set (0,00 sec)

      ~~~
    ```

2. Averigua el nombre y los dos apellidos de los alumnos que **no** han dado de alta su número de teléfono en la base de datos.

    ```sql
      ~~~
      SELECT nombre,apellido1,apellido2 FROM persona WHERE tipo='alumno' AND telefono IS NULL OR telefono=' ';
        +--------+-----------+-----------+
        | nombre | apellido1 | apellido2 |
        +--------+-----------+-----------+
        | Pedro  | Heller    | Pagac     |
        | Ismael | Strosin   | Turcotte  |
        +--------+-----------+-----------+
        2 rows in set (0,00 sec)

      ~~~
    ```

3. Devuelve el listado de los alumnos que nacieron en `1999`.

    ```sql
    ~~~
      SELECT CONCAT_WS(' ',nombre,apellido1,apellido2) AS alumnos FROM persona WHERE fecha_nacimiento LIKE '%1999%';
        +-----------------------------+
        | alumnos                     |
        +-----------------------------+
        | Ismael Strosin Turcotte     |
        | Antonio Domínguez Guerrero  |
        +-----------------------------+
        2 rows in set (0,00 sec)

    ~~~
    ```

4. Devuelve el listado de `profesores` que **no** han dado de alta su número de teléfono en la base de datos y además su nif termina en `K`.

    ```sql
    ~~~
      SELECT nombre,apellido1,apellido2,nif FROM persona WHERE tipo='profesor' AND telefono IS NULL  AND nif LIKE '%k';
        +-----------+-----------+-----------+-----------+
        | nombre    | apellido1 | apellido2 | nif       |
        +-----------+-----------+-----------+-----------+
        | Antonio   | Fahey     | Considine | 10485008K |
        | Guillermo | Ruecker   | Upton     | 85869555K |
        +-----------+-----------+-----------+-----------+
        2 rows in set (0,00 sec)
    ~~~

    ```

5. Devuelve el listado de las asignaturas que se imparten en el primer cuatrimestre, en el tercer curso del grado que tiene el identificador `7`.

    ```sql
        ~~~
        SELECT nombre,curso,cuatrimestre,id_grado FROM asignatura WHERE cuatrimestre=1 AND curso=3 AND id_grado=7;
            +---------------------------------------------+-------+--------------+----------+
            | nombre                                      | curso | cuatrimestre | id_grado |
            +---------------------------------------------+-------+--------------+----------+
            | Bases moleculares del desarrollo vegetal    |     3 |            1 |        7 |
            | Fisiología animal                           |     3 |            1 |        7 |
            | Metabolismo y biosíntesis de biomoléculas   |     3 |            1 |        7 |
            | Operaciones de separación                   |     3 |            1 |        7 |
            | Patología molecular de plantas              |     3 |            1 |        7 |
            | Técnicas instrumentales básicas             |     3 |            1 |        7 |
            +---------------------------------------------+-------+--------------+----------+
            6 rows in set (0,00 sec)
        ~~~
    ```

6. Devuelve un listado con los datos de todas las **alumnas** que se han matriculado alguna vez en el `Grado en Ingeniería Informática (Plan 2015)`.

    ```sql
    ~~~
      SELECT DISTINCT CONCAT_WS(' ',P.nombre,P.apellido1,P.apellido2) AS Alumnas,G.id
        FROM persona P
        JOIN 
            alumno_se_matricula_asignatura AMA ON AMA.id_alumno = P.id
        JOIN 
            asignatura A ON A.id = AMA.id_asignatura
        JOIN    
            grado G ON G.id  = A.id_grado
        WHERE 
            P.sexo= 'M' AND P.tipo='alumno' AND G.id=4;

            +----------------------------+----+
            | Alumnas                    | id |
            +----------------------------+----+
            | Inma Lakin Yundt           |  4 |
            | Irene Hernández Martínez   |  4 |
            | Sonia Gea Ruiz             |  4 |
            +----------------------------+----+
            3 rows in set (0,01 sec)
    ~~~
    ```

7. Devuelve un listado con todas las asignaturas ofertadas en el `Grado en Ingeniería Informática (Plan 2015)`.

    ```sql
    ~~~
      SELECT DISTINCT nombre,id_grado FROM asignatura WHERE id_grado=4;
        +---------------------------------------------------------------------------+----------+
        | nombre                                                                    | id_grado |
        +---------------------------------------------------------------------------+----------+
        | Álgegra lineal y matemática discreta                                      |        4 |
        | Cálculo                                                                   |        4 |
        | Física para informática                                                   |        4 |
        | Introducción a la programación                                            |        4 |
        | Organización y gestión de empresas                                        |        4 |
        | Estadística                                                               |        4 |
        | Estructura y tecnología de computadores                                   |        4 |
        | Fundamentos de electrónica                                                |        4 |
        | Lógica y algorítmica                                                      |        4 |
        | Metodología de la programación                                            |        4 |
        | Arquitectura de Computadores                                              |        4 |
        | Estructura de Datos y Algoritmos I                                        |        4 |
        | Ingeniería del Software                                                   |        4 |
        | Sistemas Inteligentes                                                     |        4 |
        | Sistemas Operativos                                                       |        4 |
        | Bases de Datos                                                            |        4 |
        | Estructura de Datos y Algoritmos II                                       |        4 |
        | Fundamentos de Redes de Computadores                                      |        4 |
        | Planificación y Gestión de Proyectos Informáticos                         |        4 |
        | Programación de Servicios Software                                        |        4 |
        | Desarrollo de interfaces de usuario                                       |        4 |
        | Ingeniería de Requisitos                                                  |        4 |
        | Integración de las Tecnologías de la Información en las Organizaciones    |        4 |
        | Modelado y Diseño del Software 1                                          |        4 |
        | Multiprocesadores                                                         |        4 |
        | Seguridad y cumplimiento normativo                                        |        4 |
        | Sistema de Información para las Organizaciones                            |        4 |
        | Tecnologías web                                                           |        4 |
        | Teoría de códigos y criptografía                                          |        4 |
        | Administración de bases de datos                                          |        4 |
        | Herramientas y Métodos de Ingeniería del Software                         |        4 |
        | Informática industrial y robótica                                         |        4 |
        | Ingeniería de Sistemas de Información                                     |        4 |
        | Modelado y Diseño del Software 2                                          |        4 |
        | Negocio Electrónico                                                       |        4 |
        | Periféricos e interfaces                                                  |        4 |
        | Sistemas de tiempo real                                                   |        4 |
        | Tecnologías de acceso a red                                               |        4 |
        | Tratamiento digital de imágenes                                           |        4 |
        | Administración de redes y sistemas operativos                             |        4 |
        | Almacenes de Datos                                                        |        4 |
        | Fiabilidad y Gestión de Riesgos                                           |        4 |
        | Líneas de Productos Software                                              |        4 |
        | Procesos de Ingeniería del Software 1                                     |        4 |
        | Tecnologías multimedia                                                    |        4 |
        | Análisis y planificación de las TI                                        |        4 |
        | Desarrollo Rápido de Aplicaciones                                         |        4 |
        | Gestión de la Calidad y de la Innovación Tecnológica                      |        4 |
        | Inteligencia del Negocio                                                  |        4 |
        | Seguridad Informática                                                     |        4 |
        +---------------------------------------------------------------------------+----------+
        50 rows in set (0,00 sec)
    ~~~
    ```

8. Devuelve un listado de los `profesores` junto con el nombre del `departamento` al que están vinculados. El listado debe devolver cuatro columnas, `primer apellido, segundo apellido, nombre y nombre del departamento.` El resultado estará ordenado alfabéticamente de menor a mayor por los `apellidos y el nombre.`
    ~~~
        SELECT P.nombre, P.apellido1, P.apellido2, D.nombre 
        FROM 
            persona P
        JOIN 
            profesor Pr ON P.id = Pr.id_profesor
        JOIN 
            departamento D ON Pr.id_departamento = D.id
        WHERE 
            P.tipo = 'profesor'
        ORDER BY P.nombre, P.apellido1, P.apellido2 ASC;

        +-----------+------------+------------+---------------------+
        | nombre    | apellido1  | apellido2  | nombre              |
        +-----------+------------+------------+---------------------+
        | Alejandro | Kohler     | Schoen     | Matemáticas         |
        | Alfredo   | Stiedemann | Morissette | Química y Física    |
        | Antonio   | Fahey      | Considine  | Economía y Empresa  |
        | Carmen    | Streich    | Hirthe     | Educación           |
        | Cristina  | Lemke      | Rutherford | Economía y Empresa  |
        | David     | Schmidt    | Fisher     | Matemáticas         |
        | Esther    | Spencer    | Lakin      | Educación           |
        | Francesca | Schowalter | Muller     | Química y Física    |
        | Guillermo | Ruecker    | Upton      | Educación           |
        | Manolo    | Hamill     | Kozey      | Informática         |
        | Micaela   | Monahan    | Murray     | Agronomía           |
        | Zoe       | Ramirez    | Gea        | Informática         |
        +-----------+------------+------------+---------------------+
        12 rows in set (0,00 sec)
    ~~~

9. Devuelve un listado con el nombre de las asignaturas, año de inicio y año de fin del curso escolar del alumno con nif `26902806M`.

    ```sql
      ~~~
        SELECT A.nombre,CE.anyo_inicio,CE.anyo_fin
        FROM persona P 
        INNER JOIN
            alumno_se_matricula_asignatura AMA ON AMA.id_alumno = P.id
        INNER JOIN
            asignatura A ON A.id = AMA.id_asignatura
        INNER JOIN
            curso_escolar CE ON CE.id = AMA.id_curso_escolar
        WHERE P.nif='26902806M' AND P.tipo='alumno';

        +----------------------------------------+-------------+----------+
        | nombre                                 | anyo_inicio | anyo_fin |
        +----------------------------------------+-------------+----------+
        | Álgegra lineal y matemática discreta   |        2014 |     2015 |
        | Cálculo                                |        2014 |     2015 |
        | Física para informática                |        2014 |     2015 |
        +----------------------------------------+-------------+----------+
        3 rows in set (0,00 sec)

      ~~~
    ```

10. Devuelve un listado con el nombre de todos los departamentos que tienen profesores que imparten alguna asignatura en el `Grado en Ingeniería Informática (Plan 2015)`.

     ```sql
    ~~~
        SELECT DISTINCT D.nombre,A.id_grado
        FROM departamento D
        INNER JOIN
            profesor Pr ON Pr.id_departamento = D.id
        INNER JOIN
            asignatura A ON A.id_profesor = Pr.id_profesor
        WHERE  A.id_grado =4; 

        +--------------+----------+
        | nombre       | id_grado |
        +--------------+----------+
        | Informática  |        4 |
        +--------------+----------+
        1 row in set (0,00 sec)
     ~~~
     ```

11. Devuelve un listado con todos los alumnos que se han matriculado en alguna asignatura durante el curso escolar 2018/2019.

     ```sql
        SELECT DISTINCT CONCAT_WS(' ',P.nombre,P.apellido1,P.apellido2) AS alumnos_2018_2019
        FROM persona P
        INNER JOIN alumno_se_matricula_asignatura AMA ON AMA.id_alumno = P.id
        INNER JOIN curso_escolar CE ON CE.id = AMA.id_curso_escolar
        WHERE CE.anyo_inicio = 2018 AND CE.anyo_fin = 2019; 

        +----------------------------+
        | alumnos_2018_2019          |
        +----------------------------+
        | Inma Lakin Yundt           |
        | Irene Hernández Martínez   |
        | Sonia Gea Ruiz             |
        +----------------------------+
        3 rows in set (0,00 sec)    
     ```

12. Devuelve un listado con los nombres de **todos** los profesores y los departamentos que tienen vinculados. El listado también debe mostrar aquellos profesores que no tienen ningún departamento asociado. El listado debe devolver cuatro columnas, nombre del departamento, primer apellido, segundo apellido y nombre del profesor. El resultado estará ordenado alfabéticamente de menor a mayor por el nombre del departamento, apellidos y el nombre.

     ```sql
        SELECT P.nombre,P.apellido1,P.apellido2,D.nombre
        FROM persona P
        INNER JOIN profesor PR ON PR.id_profesor = P.id
        INNER JOIN departamento D ON D.id = PR.id_departamento 
        WHERE P.tipo = 'profesor' ORDER BY D.nombre,P.nombre,P.apellido1,P.apellido2;

        +-----------+------------+------------+--------------------+
        | nombre    | apellido1  | apellido2  | nombre             |
        +-----------+------------+------------+--------------------+
        | Micaela   | Monahan    | Murray     | Agronomía          |
        | Antonio   | Fahey      | Considine  | Economía y Empresa |
        | Cristina  | Lemke      | Rutherford | Economía y Empresa |
        | Carmen    | Streich    | Hirthe     | Educación          |
        | Esther    | Spencer    | Lakin      | Educación          |
        | Guillermo | Ruecker    | Upton      | Educación          |
        | Manolo    | Hamill     | Kozey      | Informática        |
        | Zoe       | Ramirez    | Gea        | Informática        |
        | Alejandro | Kohler     | Schoen     | Matemáticas        |
        | David     | Schmidt    | Fisher     | Matemáticas        |
        | Alfredo   | Stiedemann | Morissette | Química y Física   |
        | Francesca | Schowalter | Muller     | Química y Física   |
        +-----------+------------+------------+--------------------+
        12 rows in set (0.00 sec)
     ```

13. Devuelve un listado con los profesores que no están asociados a un departamento.Devuelve un listado con los departamentos que no tienen profesores asociados.

     ```sql
       +-----------+------------+------------+---------------------+
        | nombre    | apellido1  | apellido2  | nombre              |
        +-----------+------------+------------+---------------------+
        | Micaela   | Monahan    | Murray     | Agronomía           |
        | Antonio   | Fahey      | Considine  | Economía y Empresa  |
        | Cristina  | Lemke      | Rutherford | Economía y Empresa  |
        | Carmen    | Streich    | Hirthe     | Educación           |
        | Esther    | Spencer    | Lakin      | Educación           |
        | Guillermo | Ruecker    | Upton      | Educación           |
        | Manolo    | Hamill     | Kozey      | Informática         |
        | Zoe       | Ramirez    | Gea        | Informática         |
        | Alejandro | Kohler     | Schoen     | Matemáticas         |
        | David     | Schmidt    | Fisher     | Matemáticas         |
        | Alfredo   | Stiedemann | Morissette | Química y Física    |
        | Francesca | Schowalter | Muller     | Química y Física    |
        +-----------+------------+------------+---------------------+
        12 rows in set (0,00 sec)

     ```

14. Devuelve un listado con los profesores que no imparten ninguna asignatura.

     ```sql
        SELECT P.nombre,P.apellido1,P.apellido2
        FROM persona P
        INNER JOIN profesor PR ON PR.id_profesor = P.id
        LEFT JOIN asignatura A ON A.id_profesor = PR.id_profesor
        WHERE P.tipo='profesor' AND A.id_profesor IS NULL;

        +-----------+------------+------------+
        | nombre    | apellido1  | apellido2  |
        +-----------+------------+------------+
        | David     | Schmidt    | Fisher     |
        | Alejandro | Kohler     | Schoen     |
        | Cristina  | Lemke      | Rutherford |
        | Antonio   | Fahey      | Considine  |
        | Esther    | Spencer    | Lakin      |
        | Carmen    | Streich    | Hirthe     |
        | Guillermo | Ruecker    | Upton      |
        | Micaela   | Monahan    | Murray     |
        | Alfredo   | Stiedemann | Morissette |
        | Francesca | Schowalter | Muller     |
        +-----------+------------+------------+
        10 rows in set (0.00 sec)
        
     ```

15. Devuelve un listado con las asignaturas que no tienen un profesor asignado.

     ```sql    
        SELECT A.nombre
        FROM asignatura A
        WHERE A.id_profesor IS NULL;

        +------------------------------------------------------------------------+
        | nombre                                                                 |
        +------------------------------------------------------------------------+
        | Ingeniería de Requisitos                                               |
        | Integración de las Tecnologías de la Información en las Organizaciones |
        | Modelado y Diseño del Software 1                                       |
        | Multiprocesadores                                                      |
        | Seguridad y cumplimiento normativo                                     |
        | Sistema de Información para las Organizaciones                         |
        | Tecnologías web                                                        |
        | Teoría de códigos y criptografía                                       |
        | Administración de bases de datos                                       |
        | Herramientas y Métodos de Ingeniería del Software                      |
        | Informática industrial y robótica                                      |
        | Ingeniería de Sistemas de Información                                  |
        | Modelado y Diseño del Software 2                                       |
        | Negocio Electrónico                                                    |
        | Periféricos e interfaces                                               |
        | Sistemas de tiempo real                                                |
        | Tecnologías de acceso a red                                            |
        | Tratamiento digital de imágenes                                        |
        | Administración de redes y sistemas operativos                          |
        | Almacenes de Datos                                                     |
        | Fiabilidad y Gestión de Riesgos                                        |
        | Líneas de Productos Software                                           |
        | Procesos de Ingeniería del Software 1                                  |
        | Tecnologías multimedia                                                 |
        | Análisis y planificación de las TI                                     |
        | Desarrollo Rápido de Aplicaciones                                      |
        | Gestión de la Calidad y de la Innovación Tecnológica                   |
        | Inteligencia del Negocio                                               |
        | Procesos de Ingeniería del Software 2                                  |
        | Seguridad Informática                                                  |
        | Biologia celular                                                       |
        | Física                                                                 |
        | Matemáticas I                                                          |
        | Química general                                                        |
        | Química orgánica                                                       |
        | Biología vegetal y animal                                              |
        | Bioquímica                                                             |
        | Genética                                                               |
        | Matemáticas II                                                         |
        | Microbiología                                                          |
        | Botánica agrícola                                                      |
        | Fisiología vegetal                                                     |
        | Genética molecular                                                     |
        | Ingeniería bioquímica                                                  |
        | Termodinámica y cinética química aplicada                              |
        | Biorreactores                                                          |
        | Biotecnología microbiana                                               |
        | Ingeniería genética                                                    |
        | Inmunología                                                            |
        | Virología                                                              |
        | Bases moleculares del desarrollo vegetal                               |
        | Fisiología animal                                                      |
        | Metabolismo y biosíntesis de biomoléculas                              |
        | Operaciones de separación                                              |
        | Patología molecular de plantas                                         |
        | Técnicas instrumentales básicas                                        |
        | Bioinformática                                                         |
        | Biotecnología de los productos hortofrutículas                         |
        | Biotecnología vegetal                                                  |
        | Genómica y proteómica                                                  |
        | Procesos biotecnológicos                                               |
        | Técnicas instrumentales avanzadas                                      |
        +------------------------------------------------------------------------+
        62 rows in set (0.00 sec)
     ```

16. Devuelve un listado con todos los departamentos que tienen alguna asignatura que no se haya impartido en ningún curso escolar. El resultado debe mostrar el nombre del departamento y el nombre de la asignatura que no se haya impartido nunca.

     ```sql
      SELECT D.nombre AS nombre_departamento, A.nombre AS nombre_asignatura
      FROM departamento D
      JOIN profesor P ON P.id_departamento = D.id
      JOIN asignatura A ON A.id_profesor = P.id_profesor
      LEFT JOIN alumno_se_matricula_asignatura AMA ON AMA.id_asignatura = A.id
      WHERE AMA.id_asignatura IS NULL;

      +---------------------+---------------------------------------------------+
      | nombre_departamento | nombre_asignatura                                 |
      +---------------------+---------------------------------------------------+
      | Informática         | Arquitectura de Computadores                      |
      | Informática         | Estructura de Datos y Algoritmos I                |
      | Informática         | Ingeniería del Software                           |
      | Informática         | Sistemas Inteligentes                             |
      | Informática         | Sistemas Operativos                               |
      | Informática         | Bases de Datos                                    |
      | Informática         | Estructura de Datos y Algoritmos II               |
      | Informática         | Fundamentos de Redes de Computadores              |
      | Informática         | Planificación y Gestión de Proyectos Informáticos |
      | Informática         | Programación de Servicios Software                |
      | Informática         | Desarrollo de interfaces de usuario               |
      +---------------------+---------------------------------------------------+
      11 rows in set (0.00 sec)
     ```

17. Devuelve el número total de **alumnas** que hay.

     ```sql
    SELECT COUNT(sexo) AS total_alumnas
    FROM persona P
    WHERE P.sexo = 'M' AND P.tipo ='alumno';
     ```

18. Calcula cuántos alumnos nacieron en `1999`.

     ```sql
      SELECT COUNT(fecha_nacimiento)
      FROM persona
      WHERE tipo='alumno' AND fecha_nacimiento LIKE '%1999%'
     ```

19. Calcula cuántos profesores hay en cada departamento. El resultado sólo debe mostrar dos columnas, una con el nombre del departamento y otra con el número de profesores que hay en ese departamento. El resultado sólo debe incluir los departamentos que tienen profesores asociados y deberá estar ordenado de mayor a menor por el número de profesores.

     ```sql
        SELECT D.nombre,COUNT(P.id_profesor) as TOTAL_PROFESORES
        FROM profesor P
        LEFT JOIN departamento D ON D.id = P.id_departamento GROUP BY D.nombre
     ```

20. Devuelve un listado con todos los departamentos y el número de profesores que hay en cada uno de ellos. Tenga en cuenta que pueden existir departamentos que no tienen profesores asociados. Estos departamentos también tienen que aparecer en el listado.

     ```
       # Consulta Aqui
     ```

21. Devuelve un listado con el nombre de todos los grados existentes en la base de datos y el número de asignaturas que tiene cada uno. Tenga en cuenta que pueden existir grados que no tienen asignaturas asociadas. Estos grados también tienen que aparecer en el listado. El resultado deberá estar ordenado de mayor a menor por el número de asignaturas.

     ```sql
       # Consulta Aqui
     ```

22. Devuelve un listado con el nombre de todos los grados existentes en la base de datos y el número de asignaturas que tiene cada uno, de los grados que tengan más de `40` asignaturas asociadas.

     ```sql
       # Consulta Aqui
     ```

23. Devuelve un listado que muestre el nombre de los grados y la suma del número total de créditos que hay para cada tipo de asignatura. El resultado debe tener tres columnas: nombre del grado, tipo de asignatura y la suma de los créditos de todas las asignaturas que hay de ese tipo. Ordene el resultado de mayor a menor por el número total de crédidos.

     ```sql
       # Consulta Aqui
     ```

24. Devuelve un listado que muestre cuántos alumnos se han matriculado de alguna asignatura en cada uno de los cursos escolares. El resultado deberá mostrar dos columnas, una columna con el año de inicio del curso escolar y otra con el número de alumnos matriculados.

     ```sql
       # Consulta Aqui
     ```

25. Devuelve un listado con el número de asignaturas que imparte cada profesor. El listado debe tener en cuenta aquellos profesores que no imparten ninguna asignatura. El resultado mostrará cinco columnas: id, nombre, primer apellido, segundo apellido y número de asignaturas. El resultado estará ordenado de mayor a menor por el número de asignaturas.

     ```sql
       # Consulta Aqui
     ```

26. Devuelve todos los datos del alumno más joven.

     ```sql
       # Consulta Aqui
     ```

27. Devuelve un listado con los profesores que no están asociados a un departamento.

     ```sql
       # Consulta Aqui
     ```

28. Devuelve un listado con los departamentos que no tienen profesores asociados.

     ```sql
       # Consulta Aqui
     ```

29. Devuelve un listado con los profesores que tienen un departamento asociado y que no imparten ninguna asignatura.

     ```sql
       # Consulta Aqui
     ```

30. Devuelve un listado con las asignaturas que no tienen un profesor asignado.

     ```sql
       # Consulta Aqui
     ```

31. Devuelve un listado con todos los departamentos que no han impartido asignaturas en ningún curso escolar.

     ```sql
       # Consulta Aqui
     ```