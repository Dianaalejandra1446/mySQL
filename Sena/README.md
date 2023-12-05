# Proyecto Base de Datos Sena
![drawSQL-sena-export-2023-12-05](https://github.com/Dianaalejandra1446/mySQL/assets/139186201/e0d6e908-4707-4d90-8cd7-7616916a7eb3)

## Creacion y Uso de Base de Datos

~~~
CREATE DATABASE Sena;

USE Sena;
~~~

## Crear tablas 

###### Tabla Aprendiz
~~~
create table Aprendiz (id_aprendiz INT auto_increment NOT NULL PRIMARY KEY ,
primer_nombre VARCHAR(20) , segundo_nombre VARCHAR(20),
primer_apellido VARCHAR(20),segundo_apellido VARCHAR(30),
id_carrera INT ,id_ruta INT,id_matricula INT );
~~~

###### Tabla Carrera
~~~
create table Carrera ( id_carerra INT auto_increment NOT NULL PRIMARY KEY,
nombre_carrera VARCHAR(50) NOT NULL);
~~~

###### Tabla Ruta
~~~
create table Ruta (id_ruta INT auto_increment NOT NULL PRIMARY KEY ,id_carrera INT NOT NULL ,
enfasis_ruta varchar(100) NOT NULL);
~~~

###### Tabla cursoXruta
~~~
create table cursoXruta (id_curso INT,id_ruta INT );
~~~

###### Tabla Cursos
~~~
create table Cursos (id_curso INT NOT NULL PRIMARY KEY auto_increment,nombre_curso VARCHAR(100) NOT NULL);
~~~

###### Tabla cursoXinstructor
~~~
create table cursoXinstructor (id_curso INT NOT NULL PRIMARY KEY,id_instructor INT );
~~~

###### Tabla Instructor
~~~
create table Instructor (id_instructor INT NOT NULL PRIMARY KEY auto_increment,
id_especialidad INT NOT NULL,primer_nombre VARCHAR(30),segundo_nombre VARCHAR(30),
primer_apellido VARCHAR(30),segundo_apellido VARCHAR(30));
~~~

###### Tabla Especialidad
~~~
create table Especialidad (id_especialidad INT NOT NULL PRIMARY KEY auto_increment,
nombre_especialidad VARCHAR(100) NOT NULL);
~~~

###### Tabla aprendizXcurso
~~~
create table aprendizXcurso (id_curso INT,id_aprendiz INT );
~~~

## INSERTAR DATOS
~~~
INSERT INTO Matriculas (estado_matricula) VALUES 
('Activo'),
('Activo'),
('Cancelado'),
('Activo'),
('Activo'),
('Terminado'),
('Terminado'),
('Terminado'),
('Cancelado'),
('Terminado'),
('Terminado');

INSERT INTO Aprendiz (primer_nombre,segundo_nombre,primer_apellido,segundo_apellido,id_carrera,id_ruta,id_matricula) VALUES
('Carlos', 'Saúl', 'Gómez', NULL, 1,1,1),
('Leyla', 'María', 'Delgado', 'Vargas', 1,1,2),
('Juan', 'José', 'Cardona', NULL, 1,2,3),
('Sergio' ,'Augusto', 'Contreras' ,'Navas', 1,2,4),
('Ana', 'María','Velázquez','Parra', 1,3,5),
('Gustavo' , 'Noriega' ,'Alzate',NULL,2,4,6),
('Pedro','Nell','Gómez' ,'Díaz', 2,4,7),
('Jairo' ,'Augusto','Castro' ,'Camargo',2,5,8),
('Henry' , 'Soler','Vega', NULL, 2,5,9),
('Antonio' , 'Cañate', 'Cortés',NULL,5,11,10),
('Daniel' ,'Simancas','Junior',NULL,5,10,11); 

INSERT INTO Carrera (nombre_carrera) VALUES 
('Desarrollo de Software'),
('Electrónica'),
('Macánica Automotriz'),
('Seguridad y Salud Ocupacional'),
('Soldadura');

INSERT INTO Ruta (enfasis_ruta,id_carrera) VALUES
('Sistemas de Información Empresariales', 1),
('Videojuegos', 1),
('Machine Learning', 1),
('Microcontroladores',2),
('Robótica',2),
('Dispositivos Bio-médicos',2),
('Motores Híbridos',3),
('Vehículos de Uso Agrícola',3),
('Sistemas de Gestión en Seguridad Ocupacional',4),
('Soldadura Autógena Industrial',5),
('Soldadura Eléctrica Industrial',5),
('Soldadura Submarina',5);

INSERT INTO Cursos (nombre_curso) VALUES 
('Matemáticas Básicas'),
('Álgebra Computacional'),
('Programación Básica'),
('Inglés'),
('Electrónica Básica'),
('Motor de Cuatro Tiempos'),
('Enfermedades Laborales'),
('Higiene Postural en el Trabajo'),
('Ergonomía'),
('Legislación Laboral en Colombia'),
('Materiales de Soldadura'),
('Métodos de Soldadura'),
('Fusión de Metales'),
('Buceo 1'),
('Buceo 2'),
('Riesgo Eléctrico'),
('Bases de Datos Relacionales'),
('Bases de Datos NO Relacionales'),
('Electrónica Digital'),
('Microprocesadores');

INSERT INTO Instructor (primer_nombre,segundo_nombre,primer_apellido,segundo_apellido,id_especialidad) VALUES
('Ricardo', 'Vicente', 'Jaimes', NULL, 1),
('Marinela' , NULL, 'Narvaez', NULL, 2),
('Agustín ' , 'Parra', 'Granados', NULL, 3),
('Nelson ' , 'Raúl', 'Buitrago', NULL, 4),
('Roy' , 'Hernando', 'Llamas', NULL, 5),
('Maria' , 'Jimena', 'Monsalve', NULL, 6),
('Juan' , 'Carlos', 'Cobos', NULL, 6),
('Pedro ' , NUll ,'Santamaría', NULL, 1),
('Andrea' , NULL ,'González', NULL, 1),
('Marisela', NULL, 'Sevilla', NULL, 2);

INSERT INTO Especialidad (nombre_especialidad) VALUES
('Sistemas'),
('Salud Ocupacional'),
('Soldadura'),
('Mecánica'),
('Inglés'),
('Electrónica');

INSERT INTO aprendizXcurso (id_aprendiz,id_curso) VALUES
(1,	17),
(1,	2),
(1,	3),
(1,	18),
(1,	1),
(1,	4),
(2,	1),
(2,	2),
(2,	3),
(2,	4),
(3,	3),
(3,	4),
(3,	17),
(4,	5),
(4,	19),
(4,	20),
(5,	5),
(5,	19),
(5,	20),
(11,	11),
(11,	13),
(10,	11),
(10,	14),
(6,	NULL),
(7,	NULL),
(8,	NULL),
(9,	NULL);

~~~

## Agregar llave foranea
~~~
ALTER TABLE Aprendiz 
ADD foreign key (id_matricula) references atriculas(id_matricula);

ALTER TABLE Aprendiz
ADD foreign key (id_carrera) references Carrera (id_carerra);

ALTER TABLE Aprendiz
ADD foreign key (id_ruta) references Ruta (id_ruta);

ALTER TABLE Ruta
ADD foreign key (id_carrera) references Carrera (id_carerra);

ALTER TABLE Instructor
ADD foreign key (id_especialidad) references Especialidad (id_especialidad);
~~~

## Agregue un campo Estado_Matrícula a la tabla Matrícula que indique si el estudiante se encuentra “En Ejecución”, “Terminado” o “Cancelado”
###### Tabla Matriculas
~~~
create table Matriculas( id_matricula INT auto_increment NOT NULL PRIMARY KEY ,
estado_matricula VARCHAR(30) NOT NULL);
~~~

## Agregue a el campo edad a la tabla de Aprendices.
~~~
ALTER TABLE Aprendiz 
ADD COLUMN edad INT NOT NULL;

UPDATE `Sena`.`Aprendiz` SET `edad` = '19' WHERE (`id_aprendiz` = '1');
UPDATE `Sena`.`Aprendiz` SET `edad` = '20' WHERE (`id_aprendiz` = '2');
UPDATE `Sena`.`Aprendiz` SET `edad` = '22' WHERE (`id_aprendiz` = '3');
UPDATE `Sena`.`Aprendiz` SET `edad` = '22' WHERE (`id_aprendiz` = '4');
UPDATE `Sena`.`Aprendiz` SET `edad` = '25' WHERE (`id_aprendiz` = '5');
UPDATE `Sena`.`Aprendiz` SET `edad` = '23' WHERE (`id_aprendiz` = '6');
UPDATE `Sena`.`Aprendiz` SET `edad` = '24' WHERE (`id_aprendiz` = '7');
UPDATE `Sena`.`Aprendiz` SET `edad` = '18' WHERE (`id_aprendiz` = '8');
UPDATE `Sena`.`Aprendiz` SET `edad` = '18' WHERE (`id_aprendiz` = '9');
UPDATE `Sena`.`Aprendiz` SET `edad` = '17' WHERE (`id_aprendiz` = '10');
UPDATE `Sena`.`Aprendiz` SET `edad` = '28' WHERE (`id_aprendiz` = '11');
~~~

## Si suponemos que los cursos tienen una duración diferentedependiendo de la ruta que lo contenga ¿qué modificación haría a la estructura de datos ya planteada?
~~~
ALTER TABLE cursoXruta 
ADD COLUMN duracion VARCHAR(50) NOT NULL;

INSERT INTO cursoXruta (id_ruta,id_curso,duracion) VALUES 
(1, 17,'1200 horas'),
(1, 2,'120 horas'),
(1, 3,'360 horas'),
(1, 18,'3600 horas'),
(1, 1,'1200 horas'),
(1, 4,'48 horas'),
(2, 1,'1200 horas'),
(2, 2,'120 horas'),
(2, 3,'360 horas'),
(2, 4,'48 horas'),
(3, 3,'360 horas'),
(3, 4,'48 horas'),
(3, 17,'1200 horas'),
(4, 5,'24 horas'),
(4, 19,'24 horas'),
(4, 20,'6000 horas'),
(5, 5,'24 horas'),
(5, 19,'24 horas'),
(5, 20,'1200 horas'),
(11, 11,'1600 horas'),
(11, 13,'1600 horas'),
(10, 11,'3000 horas'),
(10, 14,'2800 horas'),
(6, NULL,'300 horas'),
(7, NULL,'100 horas'),
(8, NULL,'1200 horas'),
(9, NULL,'2500 horas'),
(12, NULL,'2000 horas');
~~~

## Seleccionar los nombres y edades de aprendices que están cursando la carrera de electrónica.

~~~
SELECT primer_nombre, edad
FROM Aprendiz
WHERE id_carrera = (SELECT id_carerra FROM Carrera WHERE nombre_carrera = 'Electrónica');
~~~
### Resultado
+---------------+------+
| primer_nombre | edad |
+---------------+------+
| Gustavo       |   23 |
| Pedro         |   24 |
| Jairo         |   18 |
| Henry         |   18 |
+---------------+------+
4 rows in set (0,00 sec)

## Seleccionar Nombres de Aprendices junto al nombre de la ruta de aprendizaje que cancelaron.
~~~
SELECT
A.primer_nombre,
A.segundo_nombre,
A.primer_apellido,
A.segundo_apellido,
R.enfasis_ruta AS ruta_cancelada
FROM
Aprendiz A
JOIN
Matriculas M ON M.id_matricula = A.id_matricula
JOIN
Ruta R ON A.id_ruta = R.id_ruta
WHERE
M.estado_matricula = 'Cancelado';
~~~
### Resultado:

+---------------+----------------+-----------------+------------------+----------------+
| primer_nombre | segundo_nombre | primer_apellido | segundo_apellido | ruta_cancelada |
+---------------+----------------+-----------------+------------------+----------------+
| Juan          | José           | Cardona         | NULL             | Videojuegos    |
| Henry         | Soler          | Vega            | NULL             | Robótica       |
+---------------+----------------+-----------------+------------------+----------------+


## Seleccionar Nombre de los cursos que no tienen un instructor asignado

~~~
SELECT Cursos.nombre_curso AS CursoSinInstructor
FROM cursoXinstructor
INNER JOIN Cursos ON cursoXinstructor.id_curso = Cursos.id_curso
WHERE id_instructor IS NULL;
~~~

### Resultado 
+----------------------------------+
| CursoSinInstructor               |
+----------------------------------+
| Motor de Cuatro Tiempos          |
| Enfermedades Laborales           |
| Higiene Postural en el Trabajo   |
| Ergonomía                        |
| Legislación Laboral en Colombia  |
| Métodos de Soldadura             |
| Buceo 1                          |
| Buceo 2                          |
| Riesgo Eléctrico                 |
+----------------------------------+

## Seleccionar Nombres de los instructores que dictan cursos en la ruta de aprendizaje “Sistemas de Información Empresariales”.
~~~
SELECT I.primer_nombre, I.segundo_nombre, I.primer_apellido, I.segundo_apellido
FROM Instructor I
JOIN cursoXinstructor CI ON I.id_instructor = CI.id_instructor
JOIN cursoXruta CR ON CI.id_curso = CR.id_curso
JOIN Ruta R ON CR.id_ruta = R.id_ruta
WHERE R.enfasis_ruta = 'Sistemas de Información Empresariales';
~~~

### Resultado 

+---------------+----------------+-----------------+------------------+
| primer_nombre | segundo_nombre | primer_apellido | segundo_apellido |
+---------------+----------------+-----------------+------------------+
| Marinela      | NULL           | Narvaez         | NULL             |
| Ricardo       | Vicente        | Jaimes          | NULL             |
| Agustín       | Parra          | Granados        | NULL             |
| Nelson        | Raúl           | Buitrago        | NULL             |
| Roy           | Hernando       | Llamas          | NULL             |
+---------------+----------------+-----------------+------------------+
5 rows in set (0,01 sec)





## Genere un listado de todos los aprendices que terminaron una Carrera mostrando el nombre del profesional, el nombre de la carrera y el énfasis de la carrera (Nombre de la Ruta de aprendizaje)
~~~
SELECT
CONCAT_WS(' ',A.primer_nombre,
    A.segundo_nombre,
    A.primer_apellido,
    A.segundo_apellido)
    AS Nombre_Profesional,C.nombre_carrera,R.enfasis_ruta
FROM 
    Aprendiz A
JOIN
    Matriculas M ON M.id_matricula = A.id_matricula
JOIN 
    Ruta R  ON R.id_ruta = A.id_ruta
JOIN 
    Carrera C ON C.id_carerra = R.id_carrera
WHERE   
    M.estado_matricula = 'Terminado'
~~~

### Resultado

+------------------------------+----------------+---------------------------------+
| Nombre_Profesional           | nombre_carrera | enfasis_ruta                    |
+------------------------------+----------------+---------------------------------+
| Gustavo Noriega Alzate       | Electrónica    | Microcontroladores              |
| Pedro Nell Gómez Díaz        | Electrónica    | Microcontroladores              |
| Jairo Augusto Castro Camargo | Electrónica    | Robótica                        |
| Antonio Cañate Cortés        | Soldadura      | Soldadura Eléctrica Industrial  |
| Daniel Simancas Junior       | Soldadura      | Soldadura Autógena Industrial   |
+------------------------------+----------------+---------------------------------+


## Genere un listado de los aprendices matriculados en el curso “Bases de Datos Relacionales”.
~~~
SELECT
CONCAT_WS(' ',A.primer_nombre,
    A.segundo_nombre,
    A.primer_apellido,
    A.segundo_apellido)
    AS Aprendiz_BDR
FROM 
    Aprendiz A
JOIN 
    aprendizXcurso ON A.id_aprendiz = aprendizXcurso.id_aprendiz
WHERE
    aprendizXcurso.id_curso = 17;
~~~
### Resultado

+---------------------+
| Aprendiz_BDR        |
+---------------------+
| Carlos Saúl Gómez   |
| Juan José Cardona   |
+---------------------+
2 rows in set (0,00 sec)


## Nombres de Instructores que no tienen curso asignado.
~~~
SELECT
CONCAT_WS(' ',I.primer_nombre	,I.segundo_nombre	,I.primer_apellido	,I.segundo_apellido) AS 'Instructor sin curso'
FROM
    Instructor I
LEFT JOIN
    cursoXinstructor ON cursoXinstructor.id_instructor = I.id_instructor
WHERE
    cursoXinstructor.id_instructor IS NULL OR cursoXinstructor.id_instructor = 0;
~~~

### Resultado
+----------------------+
| Instructor sin curso |
+----------------------+
| Pedro  Santamaría    |
| Andrea González      |
| Marisela Sevilla     |
+----------------------+
3 rows in set (0,00 sec)

### Preguntas Seleccion Multiple 

1. Con que instruccion puedo cambiar o modificar un dato existente en la tabla 
A. INSERT
B. UPDATE
C. ALTER 
D. SELECT

2. Como puedo agregar una llave foranea a una tabla  

A. ALTER TABLE nombre_tabla ADD FOREIGN KEY (nombre_columna) REFRENCES nombre_tabla_primaria (nombre_columna);

B. ALTER TABLE nombre_tabla 
ADD CHECK (nombre_columna) REFRENCES nombre_tabla_primaria (nombre_columna);  

C.  ALTER TABLE nombre_tabla ;
ADD CONSTRAINT (nombre_columna) ; D. ALTER TABLE nombre_table DROP TABLE nombre_table;

3. Que operador logico evalua dos condiciones y devuelve verdadero si una es verdadera 
A. AND
B. NOT 
C. OR 
D. IS NULL

4. Que funcion devuelve la fecha y hora actual 
A. ROUND( ) 
B. NOW( ) 
C. TRIM( ) 
D. SUBSTRING( )
