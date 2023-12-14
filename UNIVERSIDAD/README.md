1. Devuelve un listado con el primer apellido, segundo apellido y el nombre de todos los alumnos. El listado deberá estar ordenado alfabéticamente de menor a mayor por el primer apellido, segundo apellido y nombre.

    ```sql
      ~~~
      SELECT  CONCAT_WS(' ',nombre,apellido1,apellido2) AS alumnos FROM persona WHERE tipo='alumno' ORDER BY nombre,apellido1,apellido2 ASC;

      ~~~
    ```

2. Averigua el nombre y los dos apellidos de los alumnos que **no** han dado de alta su número de teléfono en la base de datos.

    ```sql
      ~~~
      SELECT nombre,apellido1,apellido2 FROM persona WHERE tipo='alumno' AND telefono IS NULL OR telefono=' ';

      ~~~
    ```

3. Devuelve el listado de los alumnos que nacieron en `1999`.

    ```sql
    ~~~
      SELECT CONCAT_WS(' ',nombre,apellido1,apellido2) AS alumnos FROM persona WHERE fecha_nacimiento LIKE '%1999%';

    ~~~
    ```

4. Devuelve el listado de `profesores` que **no** han dado de alta su número de teléfono en la base de datos y además su nif termina en `K`.

    ```sql
    ~~~
      SELECT nombre,apellido1,apellido2,nif FROM persona WHERE tipo='profesor' AND telefono IS NULL  AND nif LIKE '%k';
    ~~~

    ```

5. Devuelve el listado de las asignaturas que se imparten en el primer cuatrimestre, en el tercer curso del grado que tiene el identificador `7`.

    ```sql
        ~~~
        SELECT nombre,curso,cuatrimestre,id_grado FROM asignatura WHERE cuatrimestre=1 AND curso=3 AND id_grado=7;
    ~~~
    ```

8. Devuelve un listado de los `profesores` junto con el nombre del `departamento` al que están vinculados. El listado debe devolver cuatro columnas, `primer apellido, segundo apellido, nombre y nombre del departamento.` El resultado estará ordenado alfabéticamente de menor a mayor por los `apellidos y el nombre.`
    ~~~sql
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

     ~~~
     ```

11. Devuelve un listado con todos los alumnos que se han matriculado en alguna asignatura durante el curso escolar 2018/2019.

     ```sql
        SELECT DISTINCT CONCAT_WS(' ',P.nombre,P.apellido1,P.apellido2) AS alumnos_2018_2019
        FROM persona P
        INNER JOIN alumno_se_matricula_asignatura AMA ON AMA.id_alumno = P.id
        INNER JOIN curso_escolar CE ON CE.id = AMA.id_curso_escolar
        WHERE CE.anyo_inicio = 2018 AND CE.anyo_fin = 2019; 

     ```

12. Devuelve un listado con los nombres de **todos** los profesores y los departamentos que tienen vinculados. El listado también debe mostrar aquellos profesores que no tienen ningún departamento asociado. El listado debe devolver cuatro columnas, nombre del departamento, primer apellido, segundo apellido y nombre del profesor. El resultado estará ordenado alfabéticamente de menor a mayor por el nombre del departamento, apellidos y el nombre.

     ```sql
        SELECT P.nombre,P.apellido1,P.apellido2,D.nombre
        FROM persona P
        INNER JOIN profesor PR ON PR.id_profesor = P.id
        INNER JOIN departamento D ON D.id = PR.id_departamento 
        WHERE P.tipo = 'profesor' ORDER BY D.nombre,P.nombre,P.apellido1,P.apellido2;

     ```

13. Devuelve un listado con los profesores que no están asociados a un departamento.Devuelve un listado con los departamentos que no tienen profesores asociados.

     ```sql
      SELECT P.nombre,P.apellido1,P.apellido2,D.nombre
      FROM persona P
      INNER JOIN profesor PR ON PR.id_profesor = P.id
      INNER JOIN departamento D ON D.id = PR.id_departamento 
      WHERE P.tipo = 'profesor' ORDER BY D.nombre,P.nombre,P.apellido1,P.apellido2;

     ```

14. Devuelve un listado con los profesores que no imparten ninguna asignatura.

     ```sql
        SELECT P.nombre,P.apellido1,P.apellido2
        FROM persona P
        INNER JOIN profesor PR ON PR.id_profesor = P.id
        LEFT JOIN asignatura A ON A.id_profesor = PR.id_profesor
        WHERE P.tipo='profesor' AND A.id_profesor IS NULL;
        
     ```

15. Devuelve un listado con las asignaturas que no tienen un profesor asignado.

     ```sql    
        SELECT A.nombre
        FROM asignatura A
        WHERE A.id_profesor IS NULL;

     ```

16. Devuelve un listado con todos los departamentos que tienen alguna asignatura que no se haya impartido en ningún curso escolar. El resultado debe mostrar el nombre del departamento y el nombre de la asignatura que no se haya impartido nunca.

     ```sql
      SELECT D.nombre AS nombre_departamento, A.nombre AS nombre_asignatura
      FROM departamento D
      JOIN profesor P ON P.id_departamento = D.id
      JOIN asignatura A ON A.id_profesor = P.id_profesor
      LEFT JOIN alumno_se_matricula_asignatura AMA ON AMA.id_asignatura = A.id
      WHERE AMA.id_asignatura IS NULL;
     ```

17. Devuelve el número total de **alumnas** que hay.

     ```sql
    SELECT COUNT(sexo) AS total_alumnas
    FROM persona P
    WHERE P.sexo = 'M' AND P.tipo ='alumno';
     ```

18. Calcula cuántos alumnos nacieron en `1999`.

     ```sql
    SELECT COUNT(fecha_nacimiento) AS alumnos1999
    FROM persona 
    WHERE tipo='alumno' AND fecha_nacimiento LIKE '%1999%' 
    ORDER BY alumnos1999 ASC;
     ```

19. Calcula cuántos profesores hay en cada departamento. El resultado sólo debe mostrar dos columnas, una con el nombre del departamento y otra con el número de profesores que hay en ese departamento. El resultado sólo debe incluir los departamentos que tienen profesores asociados y deberá estar ordenado de mayor a menor por el número de profesores.

     ```sql
      SELECT D.nombre, COUNT(P.id_profesor) as TOTAL_PROFESORES
      FROM profesor P
      LEFT JOIN departamento D ON D.id = P.id_departamento 
      GROUP BY D.nombre
      ORDER BY TOTAL_PROFESORES DESC;
     ```

20. Devuelve un listado con todos los departamentos y el número de profesores que hay en cada uno de ellos. Tenga en cuenta que pueden existir departamentos que no tienen profesores asociados. Estos departamentos también tienen que aparecer en el listado.

     ```sql
        SELECT D.nombre, COUNT(P.id_profesor) as TOTAL_PROFESORES
        FROM profesor P
        RIGHT JOIN departamento D ON D.id = P.id_departamento 
        GROUP BY D.nombre
        ORDER BY TOTAL_PROFESORES DESC;
     ```

21. Devuelve un listado con el nombre de todos los grados existentes en la base de datos y el número de asignaturas que tiene cada uno. Tenga en cuenta que pueden existir grados que no tienen asignaturas asociadas. Estos grados también tienen que aparecer en el listado. El resultado deberá estar ordenado de mayor a menor por el número de asignaturas.

     ```sql
       SELECT G.nombre,COUNT(A.id) AS total_asignaturas
        FROM grado G
        LEFT JOIN asignatura A ON A.id_grado = G.id
        GROUP BY G.nombre
        ORDER BY total_asignaturas DESC;
     ```

22. Devuelve un listado con el nombre de todos los grados existentes en la base de datos y el número de asignaturas que tiene cada uno, de los grados que tengan más de `40` asignaturas asociadas.

     ```sql
       SELECT G.nombre,COUNT(A.id) AS total_asignaturas
        FROM grado G
        LEFT JOIN asignatura A ON A.id_grado = G.id
        GROUP BY G.nombre 
        HAVING total_asignaturas > 40
        ORDER BY total_asignaturas DESC;
     ```

23. Devuelve un listado que muestre el nombre de los grados y la suma del número total de créditos que hay para cada tipo de asignatura. El resultado debe tener tres columnas: nombre del grado, tipo de asignatura y la suma de los créditos de todas las asignaturas que hay de ese tipo. Ordene el resultado de mayor a menor por el número total de crédidos.

     ```sql
      SELECT G.nombre,SUM(A.creditos) AS total_creditos, A.tipo
      FROM asignatura A
      RIGHT JOIN grado G ON G.id = A.id_grado
      GROUP BY G.nombre,A.tipo
      ORDER BY total_creditos DESC;
     ```

24. Devuelve un listado que muestre cuántos alumnos se han matriculado de alguna asignatura en cada uno de los cursos escolares. El resultado deberá mostrar dos columnas, una columna con el año de inicio del curso escolar y otra con el número de alumnos matriculados.

     ```sql
       SELECT CE.anyo_inicio, COUNT(AMA.id_alumno) AS alumnos
      FROM alumno_se_matricula_asignatura AMA
      INNER JOIN curso_escolar CE ON CE.id = AMA.id_curso_escolar
      GROUP BY CE.anyo_inicio;
     ```

25. Devuelve un listado con el número de asignaturas que imparte cada profesor. El listado debe tener en cuenta aquellos profesores que no imparten ninguna asignatura. El resultado mostrará cinco columnas: id, nombre, primer apellido, segundo apellido y número de asignaturas. El resultado estará ordenado de mayor a menor por el número de asignaturas.

     ```sql
       SELECT P.id, CONCAT_WS(' ', P.nombre, P.apellido1, P.apellido2) AS nombre_profesor, COUNT(A.id) AS num_asignaturas
        FROM asignatura A
        INNER JOIN profesor PR ON PR.id_profesor = A.id_profesor
        RIGHT JOIN persona P ON P.id = PR.id_profesor
        WHERE P.tipo = 'profesor'
        GROUP BY CONCAT_WS(' ', P.nombre, P.apellido1, P.apellido2), P.id
        ORDER BY num_asignaturas DESC;

     ```

26. Devuelve todos los datos del alumno más joven.

     ```sql
       SELECT * FROM persona
        WHERE tipo='alumno'
        ORDER BY fecha_nacimiento DESC LIMIT 1 
     ```

27. Devuelve un listado con los profesores que no están asociados a un departamento.

     ```sql
        SELECT P.nombre,P.apellido1,P.apellido2
        FROM persona P
        INNER JOIN profesor PR ON PR.id_profesor = P.id
        LEFT JOIN departamento D ON D.id = PR.id_departamento
        WHERE P.tipo='profesor' AND PR.id_departamento IS NULL
     ```

28. Devuelve un listado con los departamentos que no tienen profesores asociados.

     ```sql
        SELECT D.nombre
        FROM departamento D
        LEFT JOIN profesor P ON P.id_departamento = D.id
        WHERE P.id_profesor IS NULL;
     ```

29. Devuelve un listado con los profesores que tienen un departamento asociado y que no imparten ninguna asignatura.

     ```sql
    SELECT DISTINCT P.nombre,P.apellido1,P.apellido2
    FROM persona P
    INNER JOIN profesor PR ON PR.id_profesor = P.id
    LEFT JOIN departamento D ON D.id = PR.id_departamento
    LEFT JOIN asignatura A ON A.id_profesor = PR.id_profesor
    WHERE P.tipo ='profesor' AND A.id_profesor IS NULL

     ```

30. Devuelve un listado con las asignaturas que no tienen un profesor asignado.

     ```sql
        SELECT A.nombre
        FROM asignatura A 
        WHERE id_profesor IS NULL
     ```

31. Devuelve un listado con todos los departamentos que no han impartido asignaturas en ningún curso escolar.

     ```sql
       SELECT DISTINCT D.nombre
        FROM departamento D
        LEFT JOIN profesor P ON P.id_departamento = D.id
        LEFT JOIN asignatura A ON A.id_profesor = P.id_profesor
        LEFT JOIN alumno_se_matricula_asignatura AMA ON AMA.id_asignatura = A.id
        WHERE AMA.id_curso_escolar IS NULL AND A.id IS NULL